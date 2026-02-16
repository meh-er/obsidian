---
tags:
  - OSSP
---
# Concurrent Programming
![[Pasted image 20260215192950.png]]


![[Pasted image 20260215193005.png]]

![[Pasted image 20260215193418.png]]

All clients get served by the server.
Even if one client causes blocking, the other clients do not have to wait.
- Parallel tasks are always concurrent.
- Concurrent tasks may not be parallel 

### Concurrency using Threads
- In a serial system, we see this program as a **sequence of instructions** executed one-by-one.
- We look at our program (our big task) as a collection of subtasks.
- If it is possible to execute some of these subtasks at the same time with no change in final result (i.e. correctness), then we can **reduce overall time** by executing these subtasks **concurrently**.
- Co-operation between concurrent threads leads to the sharing of \Global data objects, Heap objects, Files etc.
- Lack of synchronization leads to chaos and wrong calculations.

##### What is a thread?
A **thread** of execution is the smallest sequence of programmed instructions that can be managed independently by a scheduler, which is typically a part of the operating system.
![[Pasted image 20260215193844.png]]

#### Pthreads library in C
- In your C program you need `#include <pthread.h>
- There are many functions related to pthreads.
- On a UNIX-based system, a list of these fucntions can typically be obtained with `man -k pthread`
- To know about a specific function see the man page.
- When linking, you must link to the pthread library using compilation flag `-lpthread: gcc -lpthread file.c`
Pthreads provides three synchronization mechanisms:
- Joins
- Mutual exclusions ("Mutex")
- Condition variables

#### Spawning a thread using pthread_create()
- A thread is created using pthread_create()
```
int pthread_create(
	pthread_t *thread_id // ID number for thread
	const pthread_attr_t *attr, // controls thread attributes
	void *(*function)(void*), // function to be executed
	void *arg // argument of function
);
```
- Returns - if thread creation is successful
- Otherwise returns a non-zero value to indicate an error
- We will use default attributes set by the system
- So, *attr gets replaced by NULL
**Note***
Consider the function with multiple arguments
` T *foo (T (, T *);`
where T represents any data type.
**Solution**: Pack arguments into a struct and create a wrapper, which takes the compound argument and unpacks before passing the unpacked arguments to `foo()`

pthread_join() is a blocking function
```
int pthread_join(
	pthread_t thread_id, //ID of thread to 'join'
	void **value_pntr // address of function's return value
);
```

#### Race condition and prevention
- A race condition occurs when two or more threads perform operations on the same data, but the results depend on the order in which these operations are performed.
- The problem can be solved if we can enforce **mutual exclusion** threads get exclusive access to the shared resource in turn
- Pthreads offers **'mutex'** to enforce exclusive access by a thread to a variable or a set of variables.

#### Mutual exclusion in Pthread: mutex
- Syntax for declaration and initialization of a mutex is
` pthread_mutex_t mutex1 = PTHREAD_MUTEX_INITIALIZER;`
- Creates a mutex 'mutex1' and initializes it with the default characteristics.
- generally, mutexes are declared as global.
- Use of mutex for serializing access to a shared resource:
	```
	...
	pthread_mutex_lock(&mutex1);
	counter++;
	pthread_mutex_unlock(&mutex1);
	...
	```
- Threads access 'counter' serially one after another.

##### pthread_mutex_trylock()
`int pthread_mutex_trylock(pthread_mutex_t *mutex);`
- Tries to lock a mutex object
- If the mutex object is available, then it is locked adn 0 is returned.
- Otherwise, teh function call returns nonzero. It will not wait for the object to be frees.

###### Avoiding mutex deadlock
Thread tries to acquire mutex2 and if it fails, then it releases mutex1 to avoid deadlock.

##### Condition Variables
- A **condition variable** is used to synchronize threads based on the value of data (i.e. a condition).
- One thread waits until data reaches a particular value or until a certain event occurs.
- Then, another thread sends a signal when the event occurs.
- Receiving the signal, the waiting thread wakes up

![[Pasted image 20260215200056.png]]

- A condition variable is a variable of type pthread_cond_t
`pthread_cond_t condition_cond = PTHREAD_COND_INITIALIZER;`
- A thread goes to waiting state based on 'condition to happen' by:
`pthread_cond_wait(&condition_cond, &condition_mutex);`

Function tales two arguments: the condition variable and a mutex variable associated with the condition variable.
- Waking thread based on condition
`pthread_cond_signal(&condition_cond);`

###### Why do we need a mutex with a condition variable?
![[Pasted image 20260215201234.png]]
- Presence of a signal is checked only in the 'waiting' state.
- If the signal arrives before moves to the 'waiting' state, then the Thread1 will miss that
	- Consequence: Thread1 will wait indefinitely
Condition mutex to 'serialize' the access of the condition variable in a proper way.

**Application: Concurrent operations on a shared Linked List**
Consider a sorted linked list of integers with the following operations:
- Insert: inserts a new node maintaining the sorted order.
- Delete: deletes an existing node.
- Member: returns true/false depending on node present/absent.
![[Pasted image 20260215201757.png]]

![[Pasted image 20260215201825.png]]

![[Pasted image 20260215201953.png]]

Two concurrent operations:
- Thread0 wants to insert node value 8 in the list.
- Thread1 wants to insert node value 9 in the list.
Multiple threads **cannot write** concurrently.

**Solutions**
- The first solution only allows 1 thread to access the entire list at any instant --> defeats the purpose of multithreading.
- The second only allows one thread to access any given node at any instant --> performance problem and complicated code.
Pthreads provides another kind of lock known as 'read-write lock'

##### Read-write locks
- A read-write lock is declared and initialized as
	`pthread_rwlock_t lock = PTHREAD_RWLOCK_INITIALIZER;`
- A read-write lock is like a mutex except that it provides two lock functions.
	- for just Reading
		`pthread_rwlock_rdlock(&lock);`
	- for Read-write access
		`pthread_rwlock_wrlock(&lock);`
	- There is only one unlock function
		`pthread_rwlock_unlock(&lock);`

**Rules**
```
pthread_rwlock_rdlock(){
	If no other thread holds the lock, get the lock.
	Else if other threads hold the read-lock, get the lock.
	Else if another thread holds the write-lock, then wait.
}
```

```
pthread_rwlock_wrlock(){
	If no other threads hold the read or write locl, get the lock.
	Else, wait for the lock.
}
```

Multiple concurrent threads perform operations on the linked list.
- Read lock is used for functions that do not modify the list.
- Write lock is used for functions that modify the list.
![[Pasted image 20260215203337.png]]
