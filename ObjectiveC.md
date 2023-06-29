# Objective-C

## category

- Like extension: to add functions (not data)

## attribute

- `readonly`:  it means only getter method
- `readwrite`: it means we have both getter and setter methods
- `atomic`: it means the compiler will generate additional code that prevents concurrent access to the object by multiple threads
- `nonatomic`: it means no guarantee about the access from multiple threads, but the access will be faster than `atomic` (of course because there is no additional code to be added by the compiler)
- `strong | retain`: hold a strong reference on the instance of the property
- `weak`: hold a weak reference on the instance of the property
- `assign`: it means assign a new value to the property. Mostly used with primitive data like int, float, NSInteger
- `copy`: the value of the object will be copied when assigning to the property

## KVC

- Todo

## KVO

- Todo
