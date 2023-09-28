# Append to vector (#1)

```C++
vector.insert (std::end (vector), std::begin (vector_to_copy), std::end (vector_to_copy));
```

# Append to vector (#2 - Less efficient)

```C++
std::copy (std::begin (vector_to_copy), std::end (vector_to_copy), std::back_inserter (vector));
```

#cpp #containers 