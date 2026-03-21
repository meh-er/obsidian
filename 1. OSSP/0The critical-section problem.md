---
tags:
  - OSSP
---
## Background
- Concurrent access to shared data may result in data inconsistency
- Maintaining data consistency requires mechanisms to ensure the orderly execution of cooperating processes
Classic Problem: Finite buffer shared by producer and consumer
- Producer produces a stream of items and puts them into buffer
- Consumer takes out stream of items.

Have to deal with producers waiting for consumers when buffer is full, and consumers waiting for producers when buffer is empty.

### Producer
```
while (true) {
	/* produce an item and put in nextProduced */
	while (count == BUFFER_SIZE); // wait if buffer full
	buffer [in] = nextProduced; //store new item
	in = (in + 1) % BUFFER_SIZE; // increment IN pointer
	count++; //Increment counter
	}
```


### Consumer
```
while (true) {
	while (count == 0) ; //do nothing
	nextConsumed = buffer[out];
	out = (out + 1) % BUFFER_SIZE;
	count--;
	/*consume the item in nextConsumed*/
	}
```

Something wrong with this code!  
=

- `count++` could be compiled as a sequence of CPU instructions:
	- `register1 = count`
	- `register1 = register1 + 1`
	- `count = register1`
- `count--` could be compiled likewise:
	- `register2 = count`
	- `register2 = register2 - 1`
	- `count = register2`
Consider that the producer and consumer execute the `count++` and `count--` around the same time, such that the CPU instructions are interleaved as follows (with `count = 5` initially)
	- Prod: `register1 = count {register1 -> 5}`
	- Prod: `register1 = register1 + 1 {register1 -> 6}`
	- Cons: `register2 = count {register2 -> 5}`
	- Cons: `register2 = register2 - 1{register2 -> 4}`
	- Prod: `count = register1{count->6}`
	- Cons: `count = register2{count->4}`
- With an increment and a decrement, in whatever order, we would expect no change to the original value (5), but here we have ended up with 4?!


## Solution Criteria to Critical-Section Problem
- Solution to protect against concurrent modification of data in the *critical section* with the following criteria:
	- **Mutual Exclusion** - If process, $P_i$, is in its critical section (i.e. where shared variables could be altered inconsistently), then no other processes can be in this critical section
	- **Progress** - no process outside of the critical section (i.e. in the *remainder* section) should block a process waiting to enter.
	- **Bounded Waiting** - A bound must exist on the number of times that other processes are allowed to enter the critical section after a process has made a request to enter its critical section and before that request is granted (i.e. it must be fair, so one poor process is not always waiting behind the others)
- Assume that each process executes at a nonzero speed
- No assumption concerning relative speed of the *N* processes


### Peterson's Solution
- Two process solution
- Assume that the CPU's register LOAD and STORE instructions are atomic (*not realistic* on modern CPUs, educational example)
- The two processes share two variables:
	- `int turn;`
	- `Boolean wants_in[2]`
- The variable `turn` indicates whose turn it is to enter the critical section
- The `wants_in` array is used to indicate if a process is ready to enter the critical section. `wants_in[i] = true` implies that process $P_i$ is ready.

```
do {
	wants_in[i] = TRUE; // I want access
	turn = j; // but, please you go first
	while (wants_in[j] && turn == j); //if you're waiting and its your turn, i will wait
	[critical_section]
	wants_in[i] = FALSE; //I no longer want access
	[remainder section]
	} while (TRUE);
```

While both processes are interested, they achieve fairness through the `turn` variable, which causes their access to alternate.

Interesting, but:
- Aside from the question of CPU instruction atomicity, how can we support more than two competing processes?
- Also, if we were being pedantic, we could argue that a process may be left to wait unnecessarily if a context switch occurs only after another process leaves the remainder section but before it politely offers the turn to our first waiting process.

### Synchronisation Hardware
- Many systems provide hardware support for critical section
- Uniprocessors - could disable interrupts
	- Currently running code would execute without preemption
	- Generally too inefficient on multiprocessor systems
	- Delay in one processor telling others to disable their interrupts.
- Modern machines provide the special atomic hardware instructions (Atomic = non-interruptible) `TestAndSet` or `Swap` which achieve the same goal:
	- `TestAndSet`: Test memory address (i.e. read it) and set it in one instruction
	- `Swap`: Swap contents of two memory address in one instruction
- We can use these to implement simple locks to realise mutual exclusion.

#### Solution using locks:
- The general pattern for using locks is:
```
do {
	[acquire lock]
		[critical section]
	[release lock]
		[remainder section]
	} while (TRUE);
```


#### TestAndSet Instruction
- High-level definition of the atomic CPU instruction:
```
boolean TestAndSet (boolean *target) {
	boolean original = *target; // store og value
	*target = TRUE; // set var to TRUE
	return original; // return og value
}
```

- In a nutshell: This single CPU instruction sets a variable to TRUE and returns the original value
- This is useful because, if it returns FALSE, we know that only our thread has changed the value from FALSE to TRUE; if it returns TRUE, we know we haven't changed the value.
##### Solution using TestAndSet
- Shared boolean variable `lock`, initialized to false.
- Solution:
```
do {
	while (TestAndSet(&lock); // wait until lock changed to true
		[critical section]
	lock = FALSE; // release lock
		[remainder section]
	} while (TRUE);
```
- Note, though, that this achieves mutual exclusion but not *bounded waiting* - one process could potentially wait forever due to the unpredictability of context switching

#### Bounded-waiting Mutual Exclusion with TestAndSet()
- All data structures are initialised to FALSE.
- `wanits_in[]` is an array of waiting flags, one of each process
- `lock` is a boolean variable used to lock the critical section.

![[Pasted image 20260321220346.png]]

### Inefficient Spinning
- Consider the simple mutual exclusion mechanism we just saw (TestAndSet solution)
- This guarantees mutual exclusion but with a high cost: that while loop spins constantly (using up CPU cycles) until manages to enter the critical section.
- This is a huge waste of CPU cycles and is not acceptable, particularly for user processes where the critical section may be occupied for some time.

#### Sleep and Wakeup
- Rather than having a process spin around and around, checking if it can proceed into the critical section, suppose we implement some mechanism whereby it sends itself to sleep and then is awoken only when there is a chance it can proceed.
- Functions such as `sleep()` and `wakeup()` are often available via a threading library or as kernel service calls

- Somehow, we need to make sure that when a process decides that it will go to sleep (if it failed to get the lock) it actually goes to sleep without interruption, so the wake-up signal is not missed by the not-yet-sleeping process