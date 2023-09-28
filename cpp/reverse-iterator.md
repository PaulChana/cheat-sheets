#  Reverse iterator

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

#cpp #containers