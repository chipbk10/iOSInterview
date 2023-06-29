# Concurrency

- Concurrency is the fact that two or more events or circumstances happening or existing at the same time.
- [Concurrency vs Parallelism](https://www.youtube.com/watch?v=X9H2M7xMi9E&ab_channel=iCode)

## Grand Central Dispatch (GCD)

- `GCD` is an abstraction that helps developers write multi-threaded code without manually creating and managing the threads themselves
- `GCD` will add chunks of code to a queue, and will execute one by one in fifo rule. It means first in, first out.

## Synchronous vs Asynchronous

- Synchronous code will block the current thread until the code execution is finish
- Asynchronous code will not block the current thread. The code might be executed on other thread.

## Serial Queue vs Concurrent Queue

- Serial Queue means one task at the time. All tasks are put in the queue will be executed only on 1 thread
- Concurrent Queue means multiple tasks can run at a time on different threads.
- UI code is executed on the main queue. The main queue is a serial queue.
- Global concurrent queue is created by the system. Priorities are decided through QoS.

## QoS - Quality of Service, where should you use which one?

- Quality of service helps us categorise the task in our DispatchQueue with priority. The task with higher priority will be executed earlier.
- For example, when we want to design a Facebook News Feed. We want to fetch the information like News Feed text content as soon as possible and show them on the screen. We can use QoS - `user-critical`
- Then we want to fetch the low-resolution images. We should use `UI-critical` QoS
- Then we can fetch the high-resolution images. We can cancel the operation if the user is scrolling too fast.
- Other tasks that is not UI critical task, we can do with `background` QoS, like updating database, sync data with server.

## DispatchGroup

- With `DispatchGroup`, we can group multiple tasks together, and dispatchGroup will notify us when all of them complete. Tasks can be run of different queues.
- For example, we can make multiple API calls together, and proceed only on the completion of all. We should use DispatchGroup in this case.

## DispatchBarrier

- Is used in scenario where we want to control the access or where we want to avoid the race condition.
- `DispatchBarrier` ensures that there is only one task in the queue to execute, and access to the resource

## Operation Queue

- GCD is generally preferred where tasks are not that complex, we are not interested in the state of execution. Kind of fire and forget, we don’t need pause, resume, kind of functionality, basically less control over the task.
- Operation Queue is built on top of `GCD`, is generally preferred where we need more control like we want to add dependencies between operations, reusable operation, pause, and resume operation, etc.
- GCD can also cancel the task using DispatchWorkItem. However, like Operation Queue, it’s not automatically done. We have to check like `if workItem.isCancelled?` condition to decide to continue our task or not.
- [Async Operation](https://nsprogrammer.github.io/jekyll/update/2021/07/02/nsoperation.html)
- Sync Operation can handle all values (like `isCancelled`, `isReady`, `isExecuted`, `isFinished`)
- Async Operation, we have to handle ourselves (using KVO, KVC)

