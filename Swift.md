# Swift


## Struct & Class & Actor & Enum

- [Struct vs Class vs Actor](https://www.youtube.com/watch?v=4GJBxkkql6o&ab_channel=iCode)

### Enum

- We use enum when we want to define a common type for a group of related values.

### Struct

- Value type
- No `deinit()`, no inheritance

### Class

- Reference type
- Can `deinit()`, inheritance

### Actor

- Like class, but cannot inheritance, and automatically take care of concurrency related issues 
- We don’t need to write the code for dealing with concurrency like `dispatch_barrier`, `lock`, `semaphore`, `mutex`. All of these are handled by Actor implicitly.

### Questions

- When struct contains a property of class type, its value will be copied, or it will refer to the same object? —> to the same object, because object is a class type
- Copy on write: `var array1 = [1,2]; array2 = array1` are there 2 objects in the memory? —> no, still point to the same memory address, because array2 is still not mutated yet. Until we apply some operation on array2, the second copy will be created 
- When should you use class?
    - If you have to deal with some code that is written in Objective-C, you will have to use class. Because Objective-C doesn’t have struct, it only have class. Everything is subclass from NSObject
    - Copying doesn’t make sense. When you want to hold the same reference for different instances, then you should go for a class. Or where you want to share mutable state that I should be able to change the value from this point, and also I want to change the value of the same variable from some other point too.
    - When you need inheritance
- Struct don’t support inheritance. How can you achieve something similar to inheritance with struct.
    - [struct inheritance](https://bit.ly/43XHgpB)
    - use protocol & extension

## Memory Management

- Swift uses ARC (Automatic Reference Counting) to track and manage the application’s memory usage. ARC automatically frees up the memory used by class instances when those instances are no longe needed. Reference counting applies only to instances of classes. The value type like enum, or struct we don’t take into consideration here. Basically, when we create new instance of a class, ARC will allocate memory for this instance, and the counter’s value now is 1. Whenever we assign the instance of this class to a new variable, the counter will be increased by one. And we say this new variable make a strong reference to the instance of the class. The ARC will deallocate the instance when the last strong reference on the instance is removed.
- [Automatic Reference Counting](https://docs.swift.org/swift-book/documentation/the-swift-programming-language/automaticreferencecounting/)

### Strong references reference cycles

- This happens when 2 class instances hold a strong reference to each other.
- To resolve this issue, we have to define some of the relationship between 2 classes as `weak` or `unowned`
- [retain cycle between struct & class](https://stackoverflow.com/questions/42632122/retain-cycle-between-class-and-struct)

### Weak reference

- is a reference that doesn’t keep a strong hold on the instance it refers to. So if the instance is going to be deallocated, the ARC will automatically set the weak reference to nil value, and deallocate the instance.

### Unowned reference

- Like weak reference, the unowned reference doesn’t hold a strong hold on the instance it refers to. Unowned reference is used when the other instance has the same lifetime or longer lifetime.
- Unowned reference always has value. We cannot define an unowned reference as optional type
- We can make unowned reference as optional if it point to the same type of the instance ???

### Strong reference cycles for Closures

- A strong reference cycle happens when we assign a closure to a property of a class instance, then inside the body of the closure, we access to a property or method of that instance. In this case, the instance of the class holds a strong reference on the closure, and the closure holds a strong reference on the instance of the class.
- To solve this issue, we have to define the instance of the class or the properties that we use in the closure as `unowned` or `weak`

### What is `@escaping` in closure?

- It means the closure might execute after the function returns


## Access Control

- Open: to expose a type outside of the module
- Public: like open, but the public class can no longer be sub-classed from outside. If you want to sub-class an `open` class inside the module, but don’t want to be sub-classed from outside, we should use `public`
- Internal (default): expose properties or methods outside but within the module
- Private: only access to properties and methods within a class, struct, enum. Cannot access to this in sub-class or extension
- File-private: like private, but allows access in a subclass on the same file

## iOS Application Lifecycle

- Not Running: the app has not yet been launched on the device
- Inactive: the app is in launch time, or the app is interrupted by an incoming phone call, text, or other interruptions.
- Active: the app is running in the foreground
- Background: the app moves into the background, and continues executing background code.
- Suspended: if the app does not have any code to run in the background, or if all code has completed, the app will be suspended by OS. When the app is suspended, the app is unable to execute any code in this state. The OS keeps the suspended in the memory. During a low memory condition, the OS might clean up all suspended apps.

### Events

- onActivated - this is called the first time the app is launched or every time the app comes back into foreground
- onResignActivation - this is called when the app is interrupted by an incoming phone call, text or other interruptions
- didEnterBackground - this is called when the app moves into background, this method give an application about 5 seconds to do some things before putting in the background. We can use this time to save user data, or do some other useful tasks
- willEnterForeground - this is called when the app resume to the foreground
- willTerminate - this is called when the app is going to shutdown

### Run tasks in background

- We can configure our app to run tasks in background to take advantage of the time when the device is not used.
- To schedule a task to run in the background, we have to enable the background mode in Xcode, and specify a task that suits our need (for example, playing audio, location updates, background fetch to download a file, or sync data, etc.)
- 

## ViewController Lifecycle

- viewDidLoad (1 time)
- viewWillAppear (many times when the ViewController is active and shown on the screen)
- viewWillLayoutSubviews
- viewDidLayoutSubviews
- viewDidAppear
- viewWillDisappear
- viewDidDisappear
