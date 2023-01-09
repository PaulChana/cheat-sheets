# Vectors cheatsheet

## Erase/remove_if idiom	

```C++
vector.erase (std::remove_if (std::begin (vector), std::end (vector), [](auto && element) {return <reason_here>; }), std::end (vector));
```

##  Reverse iterator

```C++
for (auto iter = vector.rbegin (); iter != vector.rend (); ++iter)
{
}

auto iter = std::end (vector);
while (iter != std::begin (vector))
{
     --iter;
    /*do stuff */ 
} 
```

## Test if vector is unique (#1)

```C++
template <typename T>
bool is_unique (std::vector<T> vector)
{
    std::sort (std::begin (vector), std::end (vector));
    return std::unique (std::begin (vector), std::end (vector)) == std::end (vector);
}
```

## Test if vector is unique (#2)

```C++
template <typename T>
bool is_unique (const std::vector<T> & vec)
{
	return std::set (std::begin (vector), std::end (vector)).size () == vec.size ();
}
```

## Append to vector (#1)

```C++
vector.insert (std::end (vector), std::begin (vector_to_copy), std::end (vector_to_copy));
```

## Append to vector (#2 - Less efficient)

```C++
std::copy (std::begin (vector_to_copy), std::end (vector_to_copy), std::back_inserter (vector));
```

#cpp