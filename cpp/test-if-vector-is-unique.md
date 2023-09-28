# Test if vector is unique (#1)

```C++
template <typename T>
bool is_unique (std::vector<T> vector)
{
    std::sort (std::begin (vector), std::end (vector));
    return std::unique (std::begin (vector), std::end (vector)) == std::end (vector);
}
```

# Test if vector is unique (#2)

```C++
template <typename T>
bool is_unique (const std::vector<T> & vec)
{
	return std::set (std::begin (vector), std::end (vector)).size () == vec.size ();
}
```

#cpp #containers 