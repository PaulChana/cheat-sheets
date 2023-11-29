# Format CMake files in CLion

Comes from [here](https://medium.com/@amitiitm2009/cmake-formatter-in-clion-7c1917763b34)

Integration steps for Clion are described here.

1. Install [cmake-format](https://github.com/cheshirekow/cmake_format) using pip `pip install — user cmake_format`
2. Create External tool in CLion
3. Add below properties in respective fields:-

```txt
Name = CMake Format 
Description = Formatting Cmake files  
Program = cmake-format
Argument = -i $FileName$
Working directory = $FileDir$
```

4. And save the settings.
5. Use this from **_Menu->Tools->External Tools->CMake Format