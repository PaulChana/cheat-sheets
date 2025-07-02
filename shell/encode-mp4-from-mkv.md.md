# Encode an MP4 from an MKV

```sh

#!/bin/bash

set -e
set -o pipefail

# Set the directory to search
directory="${1:-.}"

# Helper to cleanly get the output filename
convert_filename() {
    local input="$1"
    echo "${input%.mkv}.mp4"
}

# Always work with absolute paths
find "$(realpath "$directory")" -type f -name "*.mkv" -exec realpath {} \; | while IFS= read -r mkvfile; do
    mp4file="$(convert_filename "$mkvfile")"
    echo "Processing: $mkvfile -> $mp4file"

    ffmpeg_output=$(ffmpeg -hide_banner -i "$mkvfile" 2>&1 || true)

    vcodec="libx264"

    acodec="aac"
    if echo "$ffmpeg_output" | grep -qE 'Audio: aac'; then
        acodec="copy"
    fi

    scodec="none"
    if echo "$ffmpeg_output" | grep -q 'Subtitle: mov_text'; then
        scodec="copy"
    fi

    echo " - Video: reencode (H.264)"
    if [ "$acodec" = "copy" ]; then
        echo " - Audio: copy (AAC)"
    else
        echo " - Audio: reencode (AAC)"
    fi
    [ "$scodec" = "copy" ] && echo " - Subtitles: copy" || echo " - Subtitles: dropped"

    # Build ffmpeg command
    cmd=(ffmpeg -hide_banner -loglevel error -nostdin -y -i "$mkvfile")
    cmd+=(-map 0:v:0)
    cmd+=(-map 0:a:0)
    if [ "$scodec" = "copy" ]; then
        cmd+=(-map 0:s:0)
    fi

    # Force H.264
    cmd+=(-c:v "$vcodec" -preset medium -crf 23)

    # Audio: copy if already AAC, else reencode
    cmd+=(-c:a "$acodec")
    if [ "$acodec" = "aac" ]; then
        cmd+=(-b:a 192k)
    fi

    # Subtitles
    if [ "$scodec" = "copy" ]; then
        cmd+=(-c:s copy)
    else
        cmd+=(-sn)
    fi

    cmd+=("$mp4file")

    echo "${cmd[@]}"

    if ! "${cmd[@]}"; then
        echo "Error processing $mkvfile" >&2
        exit 1
    fi
done

echo "All done!"

```

#shell 