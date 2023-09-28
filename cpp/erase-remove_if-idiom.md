# Erase / remove_if idiom

```C++
vector.erase (std::remove_if (std::begin (vector), std::end (vector), [](auto && element) {return <reason_here>; }), std::end (vector));
```

#cpp #containers