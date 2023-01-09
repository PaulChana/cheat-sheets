# Playing with individual bits

## Macros

```C++
#define BitVal (data,y)     ((data>>y) & 1)        /** Return Data.Y value  **/
#define SetBit (data,y)     (data |= (1 << y))     /** Set Data.Y to 1      **/
#define ClearBit (data,y)   (data &= ~(1 << y))    /** Clear Data.Y to 0    **/
#define ToggleBit (data,y)  (data ^=BitVal(y))     /** Toggle Data.Y value  **/
#define Toggle (data)       (data =~data )         /** Toggle Data value    **/
```

## Get a specific bit value

```C++
int get_bit (int data, int bit) 
{
	return ((data >> bit) & 1);
}
```

## Set a specific bit value

```C++
void set_bit (int & data, int bit)
{
	data |= (1 << bit);
}
```

## Clear a specific bit

```C++
void clear_bit (int & data, int bit)
{
	data &= ~(1 << bit);
}
```

## Toggle a specific bit

```C++
void toggle_bit (int & data, int bit)
{
	data ^= get_bit (data, bit);
}
```

## Invert all bits

```C++
int invert_all_bits (int data)
{
	return ~data;
}
```

#cpp 