- In order to achieve multitasking there are two types of multitasking : 
1. Thread Based 
2. Process Based 
- Process based multitasking is when u have two or more **programs** running concurrently, the smallest unit of code  is a program 
	- example runnign chrome or vscode simulatenously 
- Thread Based 
	- thread is the smallest unit of dispachtable code that can run 
	- single program can perform multiple tasks simultaneously 
	- Handles the finer details while Process based is looking at the big picture 
	- Threads are also lightweight, while programs are heavy weight and require their own address space, context switching and and **Interprocess** communication is also costly for process. But for threads it inexpensive and efficient.
	### Problems in Threads 
	- Interruption of a thread may lead to an object being in an inconsistent state *Safety problem* 
	- A thread may block the execution of other threads *Liveness Problem*

# MultiThreading 
- Goal is to make the maximum use of available processing power by reducing idle time 
- in a multicore system : multiple threads run simultaneously each taking a slice of the computers processing power while in single core system they make us of the idle time 
## Thread Priorities
- Determines how thread should be treated wrt to other threads 
- Thread priorities are integers that specify the relative priority of the thread
- Its used to determine when to switch from one running thread to the next : 
- **Context Switch**
	- *thread can voluntarily relinquish control*: when explicitly, yielding , sleeping or when blocked 
	all other threads are examined and the thread with the highest priority is ready to run 
	-  *Thread is preempted by higher priority thread* in this case the lower priority thread that does not yield the processor is simply pre-empted (no matter what its doing) by a higher priority thread 
	- called *Premptive Multitasking*
## Synchronisation
- How to deal with asynchronous behaviour brought about by threads 
- If multiple threads want to interact with the same datastructure like a linked list , we must ensure that there is no conflict between the different threads
- Java has **Monitor** 
	- think of it as control system, it holds only one thread
	- if one thread enters a monitor then all other threads must wait until that thread exits the monitor 
	- used to protect shared asset from being manipulated by more than one thread at a time 
	- Each obj has implicity monitor (no class monitor) ; automatically entered when an objects synchronised method is called 
##  Threads  in Use 
### Thread class and Runnable Interface
- In order to create a new thread we have to either extend **Thread** class or implement the **Runnable** interface 
- We can refer directly to the ethereal state of a running thread , we refer to its proxy the **Thread** class that spawned it 
- Some methods are t: 
- ![[Screenshot 2023-12-17 at 14.42.53.png]]
### Main Thread 
- When a Java program starts up, one thread begins running immediately. This is usually called the main thread of your program, because it is the one that is executed when your program begins. The main thread is important for two reasons:
-  It is the thread from which other “child” threads will be spawned.
- Often, it must be the last thread to finish execution because it performs various shutdown actions.
Although the main thread is created automatically when your program is started, it can be controlled through a Thread object. To do so, you must obtain a reference to it by calling the method currentThread( ), which is a public static member of Thread. Its general form is shown here:
```java 
public class CurrentThreadDemo {  
    public static void main(String[] args) {  
        Thread t  =Thread.currentThread();  
        System.out.println("currrent thread "+ t);  
        try{  
            for(int i=5;i>0;i--){  
                System.out.println(i);  
                Thread.sleep(100);  
            }  
        }catch (InterruptedException e){  
            System.out.println("Main thread interrupted");  
        }  
  
    }  
}
```
- **Main** is also the name of the group to which this thread belongs 
- **Thread Group** is a datastrcutre that controls the state of collections of threads as a whole
- *Sleep Method*  causes the thread to suspend execution of a specified time 
```java
static void sleep(long milliseconds) throws InterruptedException
//or 
static void sleep(long milliseconds, long nanoseconds) throws InterruptedException 
```
## Creating Thread
### Implementing Runnable 
- create class that implements the runnable interface ; this creates a runnable type object
- the class must implement the method **run( )**
- **RUN**
	- can call other methods, use other classes and declare variables in the main thread can 
	- Run( ): establishes the entry point for another concurrent thread of execution 
	- The thread ends when run returns 
- Instantiate object of type Thread using the Runnable object we defined using our constructor 
- Thread only starts running when a void start is called 
### Extending Thread 
- Extending class must override the run() function , which is the entry point for a thread

```java 
// Constructor 
Thread(Runnable threadOb, String ThreadName);
// start method 
void start()
// RUNNABLE METHOD
public class MyRunnable implements Runnable(){
	// implement run 
	public void run(){
	Sout("MyRunnable is running ");
	}
}
public static void main(String args[]){
	Thread thread = new Thread(new MyRunnable());
	thread.start();
}
// THREAD CLASS METHOD 
public class MyThread extends Thread{
	public void run(){
		Sout("MyRunnable is running ")
	}
}
// in the main or wherever 
MyThread mt = new MyThread();
myThread.start();
```

## Thread Class Methods and States of a Thread
### Methods in Thread Class
- getName() - Obtain thread’s name
- getPriority() - Obtain thread’s priority
- isAlive() - Determine if a thread is still running
- join() - Wait for a thread to terminate
	- It makes one thread wait until the specified thread is done executing 
	- ex : if a child thread is present in the main and then t1.join() is called then , the current thread (**Main**) waits for the called thread **t1 => the child thread** to complete its execution. 
- run() - Entry point for the thread
- sleep() - Suspend a thread for a period of time
- start() - Start a thread by calling its run method
#### Daemon Threads 
- Threads who have no other purpose but to serve other threads is called daemon thread 
- Example timer threads who send regular ticks to other threads 
### Thread States 
- `New` - When a new thread is created, it is in the new state. (new Thread();)
- `Runnable` - A thread that is ready to run is moved to runnable state. (t1.run();)
- `Blocked` - When a thread is temporarily inactive, e.g. (require a lock)
- `Waiting` - When a thread is temporarily inactive, e.g. (wait on a condition);
- `Timed Waiting` - A thread lies in timed waiting state when it calls a method with a time out parameter. (Thread.sleep(1000);)
- `Terminated` - A thread terminates because of either of the following reasons: Normally exits or interrupted.
### Life cycle of a thread 
![[Pasted image 20231217154905.png]]



## Synchronisation 
### Atomic Operations 
- Java guarantees that reading and assigning of primitive types (Except long and double) are atomic and cannot be interrupted 
- All other operations should be explicitly synchronised to ensure atomicity 
### Critical Region 
- A section of program code that should be executed by only one thread at a time 
- Synchronisation is applied to a method or block of statements
### Synchronised Method 
- **Race Condition** : multiple threads calling the same method of the same object at the same time , the threads are racing each other to complete the method , to fix this problem we serialise the access to the method by using synchronised 
```java 
class MyClass{
	synchronised void aMethod(){
		 //do something 
	}
}
// synchronised code block 
synchronised(exp){
// do soemthing 
}
```
### Locks 
- Synchronisation mechanism is implemented by associating each object with a lock 
- Thread obtains exclusive possession of lock before entering critical region 
	- for methods : for the lock associated with receiving object *this* is used 
	- for block : the expression **exp** is used 
- Lock is released when the thread leaves the critical region, it may be released temporarily ***wait*** method is used 
- If multiple methods are bounded by the same lock object then they both again only one thread can access either of the methods 
- At one time only on thread has access to all synchronised methods 
### Static Synchronised Methods 
 - thread acquiring the lock of static synchronised methods has no effect any thread trying to acquire the lock of any object of the class to access a *synchronised instance method*
 - Sync of static methods is class independent while that of the instance methods is on the object of the class 
### Inter thread Communication 
- Use of the synchronised method prevents polling , usually implemented by a loop meant to check a condition repeatedly, once condition is true then the action is taken. 
- If u had a consumer and producer in polling system , consumer would waste cpu cycles for the producer to finish then start polling it would wast cpu cycles waiting for consumer to finish 
### Guarded Suspension 
- A thread may be suspended until a certain condition becomes true , at which point its execution may continue
- Clearly we can optimise this with interprocess communication 
- using  wait(), notify(),notifyAll()
- they are all defined in the *Object* class but *can* only be called from synchronised context 
	- *wait( )* 
		- tells the calling thread to give up the monitor go to sleep, until some other thread enters the same monitor and calls notify() or notifyAll()
		- Can only be called in sync method or block 
		- releases lock associated with recieving object 
		- awakened  thread must reobtain the lock before it proceeds with its execution
	- *notify()*  
		- wakes up the thread that called wait on the same object 
		- 
	- *notifyAll()* wakes up all threads that called wait() on the same object and one of them is granted access
- The *wait* method should only be called in a loop testing the condition being waited upon **not with an if statment**
- when a sync object changes its state it should call *notify all* , such that all waiting threads get a chance to resume execution 
## Thread Priority 
- Integer values ranging from 1 to 10 (Thread.MIN_PRIORITY/ Thread.MAX_PRIORITY)
- Thread inherits priority of parent thread
- it has getters and setters 
- setPriority is just a hint to JVM which the JVM may or may not honour 
- 
## Problems with Concurrency 
### Starvation 
- Some threads don't make any progress 
- if there always exists some thread of higher priority , or if thread with same priority never releases the processor 
### Dormancy 
- a waiting thread is never awakened
- if a waiting thread is not notified 
- use notifyAll() if in doubt 
### Deadlock 
- Two or more threads are blocked waiting for resources held by the other thread
- May occur when two more threads each require exclusive possession of the lock simultaneously 
- the runtime system can neither detect nor prevent deadlocks, its programmers responsibility 
- to prevent deadlock we must use resource ordering 
```java
//DEALOCK SITUATION 
//region1 - thread 1 
synchronised(a){
	synchronised(b){
	
	}
}
//region 2  - thread 2 
synchronised(b){
	synchronised(a){
	
	}
}
// this situation can lead to deadlock
//NO DEADLOCK : Resource Ordering 
//region1 - thread 1 
synchronised(a){
	synchronised(b){
	
	}
}
//region 2  - thread 2 
synchronised(a){
	synchronised(b){
	
	}
}
```
## Executors 
- part of [[Executors and Synchronisers]]
- Thread pools with executor framework 
- **Executor** is defined as a collection of threads and a work queue of tasks waiting to get executed 
- threads constantly running and checking work queue for new work 
- An object that executes a *Runnable* task
```java
anExectuor.execute(aRunnable)
//instead of 
new Thread(aRunnable).start()
```
- CREATION OF EXECUTORS 
- ![[Screenshot 2023-12-18 at 10.31.09.png]]
#### Simple example : 
```java
public class Doubler implements Runnable{  
     int [] a;  
    int from,to;  
  
    public Doubler(int[] a, int from, int to) {  
        this.a = a;  
        this.from = from;  
        this.to = to;  
    }  
    public void run(){  
        System.out.println();  
        for(int i=from;i<=to;i++){  
            a[i]*=2;  
        }  
    }  
  
}
public class ExecutorExample {  
    public static void main(String[] args) {  
        int[] a = {1,4,5,6,8,7,4,3,2};  
        ExecutorService executorService =  
                Executors.newFixedThreadPool(3);  
        executorService.execute(new Doubler(a,0,2));  
        executorService.execute(new Doubler(a,3,5));  
        executorService.execute(new Doubler(a,6,8));  
        executorService.shutdown();  
        while (!executorService.isTerminated())  
            ;  
        for(int i=0;i<9;i++){  
            System.out.print(a[i]+" ");  
            System.out.println();  
        }  
    }  
}
```
## Callable and Future 
- incase u expect threads to return a result u can use the callable interface, uses generics to define the type of object returned 
- If u submit a *callable* object to the executor a *future* object is returned, use *get()* method to retrieve it 