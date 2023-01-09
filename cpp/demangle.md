# Demangle C++ function name 

Note - This will only run on 'nix style operating systems

```C++
#include <memory>
#include <string>
#include <cxxabi.h>

class Demangler
{
public:

    template <class T>
    static std::string compute_object_name (T & obj)
    {
        const std::string mangled_name = typeid (obj).name ();
        
        int status = -1;
        std::unique_ptr<char, void(*)(void *)> res 
        { 
            abi::__cxa_demangle (mangled_name.c_str (), 
                                 nullptr, 
                                 nullptr, 
                                 &status), 
            std::free 
        };
        
        return (status == 0) ? res.get() : mangled_name;
    }
};
```

#cpp