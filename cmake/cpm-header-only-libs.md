# CPM Header only libs

```cmake
CPMAddPackage(
NAME fast-poly2tri
VERSION 1.76.0
URL https://github.com/MetricPanda/fast-poly2tri/archive/c04c633.zip
DOWNLOAD_ONLY True
)

add_library(fast-poly2tri INTERFACE IMPORTED GLOBAL)
target_include_directories(fast-poly2tri SYSTEM INTERFACE ${fast-poly2tri_SOURCE_DIR})
```

#cmake 