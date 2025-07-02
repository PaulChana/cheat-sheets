# Script a trello movie board

```sh

#!/bin/bash
TMDB_API_KEY=<ADD HERE>
TRELLO_KEY=<ADD HERE>
TRELLO_TOKEN=<ADD HERE>
WATCHMODE_API_KEY=<ADD HERE>

TRELLO_BOARD_NAME="Movies"
TRELLO_TO_WATCH_LIST_NAME="To watch"
TRELLO_QUICK_ADD_LIST_NAME="Quick add"
IMAGE_BASE_URL="https://image.tmdb.org/t/p/w500"
TMDB_BASE_URL="https://api.themoviedb.org/3"
TRELLO_API_BASE="https://api.trello.com/1"
AUTO_SELECT_FIRST_RESULT=false

NC='\033[0m'
RED='\033[0;31m'
GREEN='\033[0;32m'
CYAN='\033[0;36m'
ORANGE="\033[38;5;208m"
BOLD_RED='\033[1;31m'
BOLD_GREEN='\033[1;32m'
BOLD_CYAN='\033[1;36m'

print() {
    local colour="$1"
    local text="$2"
    echo -e "${colour}${text}${NC}"
}

get_ids() {
    BOARD_ID=$(curl -s "$TRELLO_API_BASE/members/me/boards?key=$TRELLO_KEY&token=$TRELLO_TOKEN" |
        jq -r --arg name "$TRELLO_BOARD_NAME" '.[] | select(.name==$name) | .id')

    TO_WATCH_LIST_ID=$(curl -s "$TRELLO_API_BASE/boards/$BOARD_ID/lists?key=$TRELLO_KEY&token=$TRELLO_TOKEN" |
        jq -r --arg listname "$TRELLO_TO_WATCH_LIST_NAME" '.[] | select(.name==$listname) | .id')

    QUICK_ADD_LIST_ID=$(curl -s "$TRELLO_API_BASE/boards/$BOARD_ID/lists?key=$TRELLO_KEY&token=$TRELLO_TOKEN" |
        jq -r --arg listname "$TRELLO_QUICK_ADD_LIST_NAME" '.[] | select(.name==$listname) | .id')

    NETFLIX_LABEL_ID=$(curl -s "$TRELLO_API_BASE/boards/$BOARD_ID/labels?key=$TRELLO_KEY&token=$TRELLO_TOKEN" |
        jq -r '.[] | select(.name == "Netflix") | .id')

    PRIME_LABEL_ID=$(curl -s "$TRELLO_API_BASE/boards/$BOARD_ID/labels?key=$TRELLO_KEY&token=$TRELLO_TOKEN" |
        jq -r '.[] | select(.name == "Prime") | .id')

    if [ -z "$PRIME_LABEL_ID" ] || [ -z "$NETFLIX_LABEL_ID" ] || [ -z "$BOARD_ID" ] || [ -z "$TO_WATCH_LIST_ID" ] || [ -z "$QUICK_ADD_LIST_ID" ]; then
        print "$BOLD_RED" "Failed to get IDs for board, lists, or labels. Please check your Trello configuration."
        print "$BOLD_RED" "Trello board name: $TRELLO_BOARD_NAME"
        print "$BOLD_RED" "Trello list names: $TRELLO_TO_WATCH_LIST_NAME, $TRELLO_QUICK_ADD_LIST_NAME"
        print "$BOLD_RED" "Netflix label ID: $NETFLIX_LABEL_ID"
        print "$BOLD_RED" "Prime label ID: $PRIME_LABEL_ID"
        print "$BOLD_RED" "Board ID: $BOARD_ID"
        print "$BOLD_RED" "To watch list ID: $TO_WATCH_LIST_ID"
        print "$BOLD_RED" "Quick add list ID: $QUICK_ADD_LIST_ID"
        exit 1
    fi
}

install_imagemagick() {
    if command -v convert >/dev/null 2>&1; then
        return 0
    fi

    print "$BOLD_CYAN" "ImageMagick not found, installing..."

    if [ "$(uname)" = "Linux" ]; then
        print "$CYAN" "  - Installing ImageMagick on Ubuntu/Debian..."
        sudo apt update && sudo apt install -y imagemagick
    elif [ "$(uname)" = "Darwin" ]; then
        print "$CYAN" "  - Installing ImageMagick via Homebrew..."
        brew install imagemagick
    else
        print "$BOLD_RED" "Unsupported operating system: $(uname)"
        exit 1
    fi

    if command -v convert >/dev/null 2>&1; then
        print "$BOLD_CYAN" "ImageMagick installed successfully."
    else
        print "$BOLD_RED" "ImageMagick installation failed."
        exit 1
    fi
}

print_help() {
    cat <<EOF
Usage:
  $0 [--help|-?] [--add-film "Movie Title (Year)"] [--update]

Options:
  --help, -?         Show this help message and exit
  --add-film         Add a movie by title (e.g. --add-film "Deep Cover 1992")
  --update           Scan Trello list 'Quick add', look up data, and post to 'To watch'
  (no argument)      Prompt for movie name and add manually
EOF
}

extract_title_and_year() {
    local raw_query="$1"
    local year
    local title

    year=$(echo "$raw_query" | grep -oE '\(?([0-9]{4})\)?' | grep -oE '[0-9]{4}' | head -n 1)
    title=$(echo "$raw_query" | sed -E 's/\(?[0-9]{4}\)?//g' | sed 's/  */ /g' | sed 's/^ *//;s/ *$//')
    echo "$title|$year"
}

get_tmdb_movie_json() {
    local query="$1"
    local year="$2"

    local encoded_query
    encoded_query=$(printf '%s' "$query" | jq -sRr @uri)

    local search_url
    if [ -n "$year" ]; then
        search_url="$TMDB_BASE_URL/search/movie?api_key=$TMDB_API_KEY&query=$encoded_query&year=$year"
    else
        search_url="$TMDB_BASE_URL/search/movie?api_key=$TMDB_API_KEY&query=$encoded_query"
    fi

    curl -s "$search_url"
}

select_tmdb_result() {
    local response="$1"
    local result_count
    result_count=$(echo "$response" | jq '.results | length')

    local movie_index
    local selected_index=0

    if [ "$result_count" -eq 0 ]; then
        print "$RED" "  No results found for \"$response\"" >&2
        return 1
    elif [ "$result_count" -eq 1 ] || [ "$AUTO_SELECT_FIRST_RESULT" = true ]; then
        movie_index=0
    else
        echo -e "\nMultiple results found:" >&2
        echo "$response" | jq -r '.results[] | "\(.title) (\(.release_date // "Unknown"))"' | nl >&2
        echo "" >&2
        read -p "Enter number (1-$result_count): " selected_index
        movie_index=$((selected_index - 1))
    fi

    echo "$response" | jq ".results[$movie_index]"
}

upload_scaled_and_full_image() {
    local image_url="$1"
    local card_id="$2"

    local full_image="poster_full.jpg"
    local small_image="poster_small.jpg"
    local cover_response
    local attachment_id

    curl -s "$image_url" -o "$full_image"
    if [ ! -f "$full_image" ]; then
        print "$RED" "  Failed to download image from $image_url"
        return 1
    fi

    convert "$full_image" -resize 20% "$small_image"
    if [ ! -f "$small_image" ]; then
        print "$RED" "  Failed to resize image"
        rm -f "$full_image"
        return 1
    fi

    cover_response=$(curl -s -X POST "$TRELLO_API_BASE/cards/$card_id/attachments" \
        -F "file=@$small_image" \
        -F "key=$TRELLO_KEY" \
        -F "token=$TRELLO_TOKEN")

    attachment_id=$(echo "$cover_response" | jq -r '.id')

    if [ -n "$attachment_id" ] && [ "$attachment_id" != "null" ]; then
        curl -s -X PUT "$TRELLO_API_BASE/cards/$card_id/idAttachmentCover" \
            -d "key=$TRELLO_KEY" \
            -d "token=$TRELLO_TOKEN" \
            -d "value=$attachment_id" >/dev/null
    else
        print "$ORANGE" "  Upload succeeded, but could not set cover."
    fi

    rm -f "$small_image" "$full_image"
}

add_movie_to_trello() {
    local movie_json="$1"
    local title
    local overview
    local poster_path
    local movie_id
    local tmdb_link
    local poster_url
    local watchmode_encoded_query
    local watchmode_id
    local watch_sources
    local netflix_link
    local prime_link
    local label_ids=()
    local description
    local create_card_response
    local card_id
    local label_args=()
    local release_date
    local release_year
    local details
    local runtime
    local genres

    title=$(echo "$movie_json" | jq -r '.title')

    if [ -z "$title" ] || [ "$title" = "null" ]; then
        print "$RED" "  Movie title is empty. Skipping."
        return 1
    fi

    release_date=$(echo "$movie_json" | jq -r '.release_date')
    release_year=${release_date:0:4}
    overview=$(echo "$movie_json" | jq -r '.overview')
    poster_path=$(echo "$movie_json" | jq -r '.poster_path')
    movie_id=$(echo "$movie_json" | jq -r '.id')
    details=$(curl -s "$TMDB_BASE_URL/movie/$movie_id?api_key=$TMDB_API_KEY")
    runtime=$(echo "$details" | jq -r '.runtime')
    genres=$(echo "$details" | jq -r '[.genres[].name | "`" + . + "`"] | join(" ")')
    tmdb_link="https://www.themoviedb.org/movie/$movie_id"
    poster_url="$IMAGE_BASE_URL$poster_path"

    watchmode_encoded_query=$(jq -rn --arg v "$title" '$v|@uri')
    watchmode_id=$(curl -s "https://api.watchmode.com/v1/search/?apiKey=$WATCHMODE_API_KEY&search_field=name&search_value=$watchmode_encoded_query" | jq '.title_results[0].id')

    if [ -n "$watchmode_id" ] && [ "$watchmode_id" != "null" ]; then
        watch_sources=$(curl -s "https://api.watchmode.com/v1/title/$watchmode_id/sources/?apiKey=$WATCHMODE_API_KEY&region=GB")
        netflix_link=$(echo "$watch_sources" | jq -r '.[] | select(.name == "Netflix" and .region == "GB") | .web_url' | head -n 1)
        prime_link=$(echo "$watch_sources" | jq -r '.[] | select(.name == "Amazon" and .region == "GB") | .web_url' | head -n 1)
    fi

    description="*$overview*


Runtime: $runtime minutes
Release date: $release_date


Genres: $genres


[Movie DB]($tmdb_link)"
    [ -n "$netflix_link" ] && description+="
[Netflix]($netflix_link)"
    [ -n "$prime_link" ] && description+="
[Prime]($prime_link)"

    if [ -n "$netflix_link" ]; then
        [ -n "$NETFLIX_LABEL_ID" ] && label_ids+=("$NETFLIX_LABEL_ID")
    fi
    if [ -n "$prime_link" ]; then
        [ -n "$PRIME_LABEL_ID" ] && label_ids+=("$PRIME_LABEL_ID")
    fi

    for id in "${label_ids[@]}"; do
        label_args+=("-d" "idLabels[]=$id")
    done

    create_card_response=$(curl -s -X POST "$TRELLO_API_BASE/cards" \
        -d "key=$TRELLO_KEY" \
        -d "token=$TRELLO_TOKEN" \
        -d "idList=$TO_WATCH_LIST_ID" \
        -d "name=$title ($release_year)" \
        --data-urlencode "desc=$description" \
        -d "urlSource=" \
        "${label_args[@]}")

    card_id=$(echo "$create_card_response" | jq -r '.id')
    if [ -z "$card_id" ]; then
        print "$RED" "  Failed to create Trello card."
        echo "$create_card_response"
        return 1
    fi

    if [ "$poster_path" != "null" ]; then
        upload_scaled_and_full_image "$poster_url" "$card_id"
        print "$GREEN" "  Added '$title' to Trello with poster"
    else
        print "$GREEN" "  Added '$title' to Trello"
    fi
}

process_film() {
    local result
    local movie_query
    local movie_year
    local movie_response
    local movie_json

    result=$(extract_title_and_year "$1")
    movie_query=${result%%|*}
    movie_year=${result##*|}
    movie_response=$(get_tmdb_movie_json "$movie_query" "$movie_year")
    movie_json=$(select_tmdb_result "$movie_response")
    add_movie_to_trello "$movie_json"
    return $?
}

update_watchlist() {
    local card_count
    local cards
    local card
    local title
    local source_card_id

    print "$BOLD_CYAN" "Fetching 'quick add' entries from Trello..."

    AUTO_SELECT_FIRST_RESULT=true

    cards=$(curl -s "$TRELLO_API_BASE/lists/$QUICK_ADD_LIST_ID/cards?key=$TRELLO_KEY&token=$TRELLO_TOKEN")

    card_count=$(echo "$cards" | jq 'length')
    for ((i = 0; i < card_count; i++)); do
        card=$(echo "$cards" | jq ".[$i]")
        title=$(echo "$card" | jq -r '.name')
        print "$BOLD_GREEN" "  Processing $title"
        source_card_id=$(echo "$card" | jq -r '.id')

        if ! process_film "$title"; then
            print "$BOLD_RED" "  Failed to process film $title"
        else
            curl -s -X DELETE "$TRELLO_API_BASE/cards/$source_card_id?key=$TRELLO_KEY&token=$TRELLO_TOKEN" >/dev/null
        fi
    done
}

prepare() {
    install_imagemagick
    get_ids
}

case "$1" in
--help | -?)
    print_help
    exit 0
    ;;
--update)
    prepare
    update_watchlist
    ;;
--add-film)
    shift
    prepare
    process_film "$*"
    ;;
*)
    prepare
    read -p "Enter movie name: " RAW_QUERY
    process_film "$RAW_QUERY"
    ;;
esac

```

#shell 