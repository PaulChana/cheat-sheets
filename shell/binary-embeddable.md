# Binary files

The following routines allow you to convert binary files to an embeddable C++ header file, or take a previously generated header file and go back to a binary file

## Convert binary to embeddable

```sh
xxd -i binary_file > binary_file.h
```

## Convert embedded to binary

```C++
std::fstream input_file (input_path);

if (! input_file.is_open ())
    return false;

std::stringstream input_stream;
input_stream << input_file.rdbuf ();

auto entireFile = input_stream.str ();
if (entireFile.empty ())
    return false;

entireFile.erase (std::remove (entireFile.begin (), entireFile.end (), '\n'),
                  entireFile.end ());

const auto first = entireFile.find ('{') + 1;
const auto last = entireFile.find ('}') + 1;
auto read_file = entireFile.substr (first, last - first);

if (read_file.empty ())
    return false;

std::regex regex (", ");
std::sregex_token_iterator token_iterator (read_file.begin (), read_file.end (), regex, -1);
std::sregex_token_iterator end;

std::vector<unsigned char> chars_from_file;
for (auto & byte : std::vector<std::string> (token_iterator, end))
    chars_from_file.push_back ((unsigned char) strtol (byte.c_str (), nullptr, 16));

std::ofstream output (output_path, std::ios::out | std::ios::binary);

if (! output.is_open ())
    return false;

output.write ((char *) chars_from_file.data (), chars_from_file.size () * sizeof (unsigned char));
output.close ();
```

# shell
