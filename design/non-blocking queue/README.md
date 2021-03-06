## [How do we implement a π§π¨π§-ππ₯π¨ππ€π’π§π  queue?](https://twitter.com/alexxubyte/status/1542882527110541312)

> What are the differences between blocking and non-blocking algorithms?
> 
> The terms we use when discussing blocking and non-blocking algorithms can be confusing, so letβs start by reviewing the terminology in the concurrency area with a diagram.

![non-blocking_queue](non-blocking_queue.jpeg)

πΉblocking

The blocking algorithm uses locks. Thread A acquires the lock first, and Thread B might wait for arbitrary lengthy periods if Thread A gets suspended while holding the lock. This algorithm may cause Thread B to starve.

πΉnon-blocking:

The non-blocking algorithm allows Thread A to access the queue, but Thread A must complete a task in a certain number of steps. Other threads like Thread B may still starve due to the rejections.

> This is the main ππ’ππππ«ππ§ππ between blocking and non-blocking algorithms: The blocking algorithm blocks Thread B until the lock is released. A non-blocking algorithm notifies Thread B that access is rejected.

πΉstarvation-free:

Thread Starvation means a thread cannot acquire access to certain shared resources and cannot proceed. Starvation-free means this situation does not occur.

πΉwait-free:

All threads can complete the tasks within a finite number of steps.

ππ’πͺπ΅-π§π³π¦π¦ = ππ°π―-ππ­π°π€π¬πͺπ―π¨ + ππ΅π’π³π·π’π΅πͺπ°π―-π§π³π¦π¦

β‘οΈ Non-Blocking Queue ππ¦π©π₯ππ¦ππ§π­ππ­π’π¨π§

We can use Compare and Swap (CAS) to implement a non-blocking queue. The diagram below illustrates the algorithm.

β‘οΈ πππ§πππ’π­π¬

1. No thread suspension. Thread B can get a response immediately and then decide what to do next. In this way, the thread latency is greatly reduced.
2. No deadlocks. Threads A and B do not wait for the lock to release, meaning that there is no possibility of a deadlock occurring.