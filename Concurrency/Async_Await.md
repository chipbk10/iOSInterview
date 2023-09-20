# Async Await

## Sendable

- is data that can safely be transferred to another thread.
- Source: @Todo

## @preconcurrency

- Adding @preconcurrency makes it a non-breaking change for the app integrating the module.
- It means the compiler will not check by default if the type is actually used on the main thread. It would only check if we enable the strict concurrency checking build settings at the app (integration) level.
- If we don't use @preconcurrency, there's a risk that the app (integration point) will not compile anymore with your module, in case these types are not called on the main thread.
- So in short, we use @preconcurrency during the transition. 
- In the future, we will remove this annotation (once all projects are migrated to modern concurrency, or at least strict concurrency checking).
- Source: [@preconcurrency](https://www.hackingwithswift.com/swift/5.6/preconcurrency)
