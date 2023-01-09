# Convert string to memory block

```C++
juce::String juceString (“This is my string”);
juce::MemoryBlock memoryBlock (myString.toUTF8 (), myString.length ());
```

#juce