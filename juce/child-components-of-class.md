# Get the child components of a given class

```C++
template <class ComponentClass>
static std::vector <ComponentClass *> getChildComponentsOfClass (Component * parent)
{
    std::vector <ComponentClass *> children;
    for (int i = 0; i < parent->getNumChildComponents (); ++i)
    {
        auto * childComp = parent->getChildComponent (i);
        if (auto c = dynamic_cast <ComponentClass *> (childComp))
            if (c->isVisible ())
                children.push_back (c);

        auto subChildren = getChildComponentsOfClass <ComponentClass> (childComp);
        children.insert (children.end (), subChildren.begin (), subChildren.end ());
    }
    return children;
}
```

#juce