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