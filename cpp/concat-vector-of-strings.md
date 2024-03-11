# Concatenate a vector of strings

```c++

std::vector<std::string> strings;
const std::string combiner = ", ";
auto concatString = std::accumulate(std::begin(strings), std::end(strings), std::string{""}, [combiner](auto && lhs, auto &&rhs) { return lhs.empty() ? rhs : lhs + combiner + rhs; });
```

#cpp #containers 