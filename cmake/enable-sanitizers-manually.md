# Enable sanitizers manually

To enable Clang sanitiser in a CMake project (e.g. in CLion), edit your CMakeCache.txt file (found in the build folder) with the following:  

- Add `-fsanitize=address`, `-fsanitize=thread`, or `-fsanitize=undefined` to `CMAKE_CXX_FLAGS` and `CMAKE_EXE_LINKER_FLAGS`
- Change linker to clang: `CMAKE_LINKER:FILEPATH=/usr/bin/clang++`  (this is what the docs recommend, I found it worked without this step)
- Re-build
- Debug
- Find a load of problems you didn’t know existed

Visual Studio also supports address sanitiser. It can be enabled by adding `/fsanitize=address` to `CMAKE_CXX_FLAGS`