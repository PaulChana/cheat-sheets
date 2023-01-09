# Round up and down to nearest

## Round down to nearest multiple

```C++
int round_down (int round_this_down, int to_nearest_multiple_of) 
{
    return round_this_down >= 0 ? (round_this_down / to_nearest_multiple_of) * to_nearest_multiple_of : ((round_this_down - to_nearest_multiple_of + 1) / to_nearest_multiple_of) * to_nearest_multiple_of;
}
```

## Round up to nearest multiple

```C++
int round_up (int round_this_up, int to_nearest_multiple_of) 
{
    return round_this_up >= 0 ? ((round_this_up + to_nearest_multiple_of - 1) / to_nearest_multiple_of) * to_nearest_multiple_of : (round_this_up / to_nearest_multiple_of) * to_nearest_multiple_of;
}
```

#cpp 