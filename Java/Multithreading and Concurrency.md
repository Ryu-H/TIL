# Multithreading and Concurrency

## The Basics

- **Concurrency** is the broader term where more than a single set of operations can be run over a *period* of time - i.e. does not imply that the operations are happening at the same *instance* of time.
- **Parallelism** is one way of achieving **Concurrency** and it implies that more than one set of operations are being run at the same *instance* of time.


## Threading in Java - Two levels of Abstraction
In both cases, we have a class that performs the operation that we want to run in the multithreaded manner to implement the `Runnable` interface. The `run()` method in the interface is not defined to throw any checked exceptions, therefore the class that implements the interface need to handle any checked exceptions within its implementation.


### The Thread class

The `Thread` class allows more direct control over the actual threads within the process, but requires more management and care - for instance you are left with your own decision making in terms of how many threads can be run at the same time without causing your process to break down.

To avoid the main thread from terminating the application, you may want to call `join()` on the other threads to have the main thread block its further execution.

```java
Thread thread = new Thread(runnableImplementation);

thread.start();

try {
  thread.join();  
} (InterruptedException e) {
  // ...
}
```


### The ExecutorService class
The `ExecutorService` and `Executors` classes allow creation of thread pools which require less of the low level management on the individual threads. e.g. You can create a thread pool which you can control the maximum number of threads that will be craeted in that pool.

```java
ExecutorService executorService = Executors.newFixedThreadPool(3);
for (int i = 0; i < numberOfRunnables; i++) {
  RunnableImplementation runnable = new RunnableImplementation();

  executorService.submit(runnable);
}

// Runnables already submitted will run to completion but will disallow further tasks being submitted
executorService.shutdown();

try {
  executorService.awaitTermination(60, TimeUnit.SECONDS);
} catch (InterruptedException e) {
  // ..
}
```

## The Callable and Future

We can have a class to implement `Callable` interface so that some 'task' can be run on a thread which will return some value or even raise exception during the process if anything goes wrong.

There is a overload of the `submit()` method on the `ExecutorService` class that will take the Callable interface instead of the Runnable, and will have a return type of `Future`. Calling of `get()` method on the `Future` object will block the calling thread until the `call()` method either returns the value or raises and exception. If an exception is thrown however, the `get()` will throw an exception of type `ExecutionException` which will have the original exception as the *cause* rather than throwing that original exception itself.

Both the `Callable` and the `Future` utilise generic to define what the return type of the `call()` will be.

```java
ExecutorService executorService = new ExecutorService(3);

Future<Integer> results = new Future[numberOfCallables];

for (int i = 0; i < numberOfCallables; i++) {
  CallableImplementation callable = new CallableImplementation();

  results[i] = executorService.submit(callable);
}

for (Future<Integer> result : results) {
  try {
    int value = result.get();
  } catch (ExecutionException e) {
    // e.getCause(); to get the inner-exception that the call() method would have thrown
  } catch (InterruptedException e) {
    // ...
  }
}
```

## Locks on object instances

A thread that acquired a 'lock' on an instance of a class will prevent any other threads from being able to enter the set of operations that also require its lock. This can be achieved in two ways:
1. Mark a method as `synchronized` to prevent other threads from doing any work on that object instance that require its lock.

2. Use a synchronised statement block. Useful for when you want to perform multiple set of operations that need to happen atomically.

```java
private BankAccount account;

synchronized(account) {
  // ...
}
```

## Other useful concurrency related stuff in Java

- `Collections` class provides static methods that return a thread safe proxy of collections. All the work occurs in the original collections
- Blocking Collections available for Producer / Consumer scenario - the Consumer will block if content is not available yet. e.g. `LinkedBlockingQueue`, `PriorityBlockingQueue`
- Semaphores and atomic operations
