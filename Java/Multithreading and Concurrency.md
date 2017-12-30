# Multithreading and Concurrency

## The Basics

- **Concurrency** is the broader term where more than a single set of operations can be run over a *period* of time - i.e. does not imply that the operations are happening at the same *instance* of time.
- **Parallelism** is one way of achieving **Concurrency** and it implies that more than one set of operations are being run at the same *instance* of time.


## Threading in Java - Two levels of Abstraction
In both cases, we have a class that performs the operation that we want to learn in the multithreaded manner to implement the **Runnable** interface. The `run()` method in the interface is not defined to throw any checked exceptions, therefore the class that implements the interface need to handle any checked exceptions within its implementation.


### The Thread class

The **Thread** class allows more direct control over the actual threads within the process, but requires more management and care - for instance you are left with your own decision making in terms of how many threads can be run at the same time without causing your process to break down.

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
The **ExecutorService** and **Executors** classes allow creation of thread pools which require less of the low level management on the individual threads. e.g. You can create a thread pool which you can control the maximum number of threads that will be craeted in that pool.

```java
ExecutorService executorService = Executors.newFixedThreadPool(3);
for (int i = 0; i < numberOfRunnables; i++) {

  executorService.submit(runnableImplementation);
}

// Runnables already submitted will run to completion but will disallow further tasks being submitted
executorService.shutdown();

try {
  executorService.awaitTermination(60, TimeUnit.SECONDS);
} catch (InterruptedException e) {
  // ..
}
```
