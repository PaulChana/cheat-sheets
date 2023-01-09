# Modulo index

For those times when you want a 1D array, but treat it as if it was a 2D array

## 1D to 2D

```C++
p.x = index / number_of_columns;
p.y = index % number_of_rows;
```

## 2D to 1D

```C++
index._row * number_of_rows + index.number_of_columns;
```

#cpp 