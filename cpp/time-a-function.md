# Time a function

```C++
#include <iostream>
#include <cmath>
#include <iomanip>
#include <chrono>

int fun (const int a, const int b, const int c) 
{
  return a * b * c;
}

int main(int argc, const char * argv[]) 
{
    for (int i = 0; i < 101; i++) 
    {
        float x = static_cast<float> (i) / 100.f;
        auto start = std::chrono::steady_clock::now ();
        auto t1    = fun (i, i * 5, i * 10);
        auto end   = std::chrono::steady_clock::now ();

        std::cout << "T1 -> " << std::chrono::duration <double, std::nano> (end - start).count();
    }
}
```

#cpp 