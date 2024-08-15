**Introduction to Multithreading**.

### 1. Introduction of Multithreading

**1.1 Definition of Multithreading:**
Multithreading is the ability of a CPU or a single process to execute multiple threads concurrently.
Threads - Threads are the smallest unit of processing that can be scheduled by an operating system. Multithreading aims to maximize the utilization of CPU by sharing its resources among multiple threads.

**1.2 Benefits and Challenges of Multithreading:**

**Benefits:**
- **Increased Responsiveness:** In a multithreaded environment, a program can still be responsive even if part of it is blocked or performing a lengthy operation.
- **Resource Sharing:** Threads within the same process share the same memory and resources, which can lead to more efficient use of resources.
- **Improved Performance:** On multiprocessor systems, multithreading can lead to better utilization of CPU cores, improving the overall performance of the application.
- **Scalability:** Multithreading can make an application more scalable as it can perform multiple operations simultaneously.

**Challenges:**
- **Complexity:** Writing, debugging, and maintaining multithreaded applications is more complex due to the need for proper synchronization between threads.
- **Concurrency Issues:** Issues like deadlocks, race conditions, and thread starvation can occur in multithreaded environments.
- **Overhead:** Context switching between threads can introduce overhead, reducing the performance gains from multithreading.

**1.3 Processes vs. Threads:**

- **Process:** A process is an independent executing environment that contains its own memory space, file handles, and other resources. Processes do not share memory space with other processes.
- **Thread:** A thread is a lightweight process that shares the same memory space with other threads in the same process. Each thread has its own stack and execution context, but shares the heap and global variables with other threads.

**1.4 Multithreading in Java:**
Java provides built-in support for multithreading through the `java.lang.Thread` class and the `java.lang.Runnable` interface. The Java Virtual Machine (JVM) supports native threads, allowing Java programs to take full advantage of the underlying operating system's threading capabilities.


### 2. Basics of Threads

**2.1 Creating Threads:**
In Java, there are two main ways to create a thread:

- **Extending the Thread Class:** You can create a new class that extends the `Thread` class and override its `run()` method. This method contains the code that will execute when the thread is started.
  
  ```java
  class MyThread extends Thread {
      public void run() {
          System.out.println("Thread is running...");
      }
  }
  
  public class Main {
      public static void main(String[] args) {
          MyThread t1 = new MyThread();
          t1.start(); // Starts the thread and calls the run() method
      }
  }
  ```

- **Implementing the Runnable Interface:** Alternatively, you can implement the `Runnable` interface and pass an instance of the class to a `Thread` object.
  
  ```java
  class MyRunnable implements Runnable {
      public void run() {
          System.out.println("Thread is running...");
      }
  }
  
  public class Main {
      public static void main(String[] args) {
          MyRunnable myRunnable = new MyRunnable();
          Thread t1 = new Thread(myRunnable);
          t1.start(); // Starts the thread and calls the run() method
      }
  }
  ```

**2.2 Thread Lifecycle:**
A thread in Java can be in one of several states during its lifecycle:

- **New:** When a thread is created but not yet started, it is in the "New" state.
  
- **Runnable:** After the `start()` method is called, the thread moves to the "Runnable" state. The thread is ready to run and is waiting for the CPU to schedule its execution.
  
- **Blocked:** A thread is in the "Blocked" state when it is waiting for a monitor lock to enter a synchronized block/method.
  
- **Waiting:** The thread is in the "Waiting" state if it is waiting indefinitely for another thread to perform a particular action (e.g., waiting for a notification).
  
- **Timed Waiting:** Similar to "Waiting," but the thread is waiting for a specified amount of time (e.g., `sleep()`, `join()` with a timeout).
  
- **Terminated:** The thread has finished its execution either by completing its `run()` method or by being terminated by an exception.

**2.3 Thread Priority:**
Each thread in Java has a priority, which helps the thread scheduler decide the order of thread execution. Java provides constants for setting priority:

- `Thread.MIN_PRIORITY` (value 1)
- `Thread.NORM_PRIORITY` (value 5, the default)
- `Thread.MAX_PRIORITY` (value 10)

Threads with higher priority are more likely to be selected for execution, though this is platform-dependent and doesn't guarantee execution order.

**2.4 Synchronization & Thread Safety:**
In a multithreaded environment, multiple threads may try to access shared resources concurrently, which can lead to inconsistent data. Synchronization is used to control access to shared resources to ensure thread safety.

- **Synchronized Methods:** A synchronized method locks the object for any thread that calls it. No other thread can call any other synchronized method on the same object until the lock is released.

  ```java
  public synchronized void increment() {
      count++;
  }
  ```

- **Synchronized Blocks:** Instead of synchronizing an entire method, you can use synchronized blocks to lock only a part of the code.

  ```java
  public void increment() {
      synchronized(this) {
          count++;
      }
  }
  ```

**2.5 Volatile Keyword:**
The `volatile` keyword is used in multithreading to ensure visibility of changes to variables across threads. When a variable is declared as volatile, the JVM ensures that every thread reads its current value from the main memory.

```java
private volatile boolean running = true;
```