# Random number generation

## Uniform random (int)

```C++
#include <random>

int generate_random ()
{
    std::random_device random_device;
    std::mt19937 generator (random_device ());
    std::uniform_int_distribution <> distribution (min_element, max_element);
    return distribution (generator);
}
```

## Uniform random (float)

```C++
#include <random>

float generate_random ()
{
    std::random_device random_device;
    std::mt19937 generator (random_device ());
    std::uniform_real_distribution<> distribution (min_element, max_element);
    return distribution (generator);
}
```

## Normal random (double)

```C++
#include <random>

double generate_random ()
{
    std::mt19937 generator;
    double mean = 0.0;
    double std  = 1.0;
    std::normal_distribution<double> normal (mean, std);
    return normal (generator);
}
```

#cpp 