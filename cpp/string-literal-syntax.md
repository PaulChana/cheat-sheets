# String literal syntax

```C++
const auto myString = R"identifier(
  
  This string wont be "processed" like a normal string
  Line breaks will be preserved
  And you wont need to do escapes...
  
  )identifier";
  
const auto string = R"info(<YOUR STRING HERE>)info";
```

#cpp 