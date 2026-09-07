# Q1
## (a) The code below is intended to launch ten threads with the integers 1 through 10 inclusive. However, when the code is executed, it does not print the anticipated results, can you explain why? (4)
![[Pasted image 20260603170749.png]]

- uses the address of i in the creation of thread as the function argument
- This means that every time pthread_create is called, the same memory address is being sent to is.
- It also does not have any wait condition for the previous iteration to run myfunc before moving onto the next, so it will only print the final number which is at the address of i.

## (b) Modify the code in a) to correct the inconsistency so that the intended results are displayed correctly. Briefly explain your logic (8)

Fix: make sure pthread takes in a new function each time and waits.

```
int main () {
	int i;
	pthread_t tidl
	for (i = 1; i < 11 i++) {
		arg = i
		pthread_create(&tid,NULL,myfunc,arg);
	}
```
Put it one by one instead of jsut running and running idk

## (c) The insert C function below inserts a new element into a singly link lists to the end of a list. Modify the insert() function to an enqueue() function, which inserts nodes into a priority queue by priority. Assume that each node has a priority field. Node: a priority queue is a (singly) linked list ordered by priority, with high priority values in front.  (8)
![[Pasted image 20260603171524.png]]

```
int enqueue (Node **queue, NODE *p)

void insert(NODE **list, NODE *p)
{
	NODE *q = *list;
	if (q == 0)
		*list = p;
	else{
		while (q->next)
			q = q->next;
		q->next = p;
		}
	p->next = 0;
}

void enqueue(NODE **list, Node *p)
{
	Node *q = *list;
	if (q == 0)
		*list = p;
	else {
		while (q->next)
			while (q.priority < p.priority){
				q = q->next;
			}
		}
		p->next = 0;
	}
```

# Q2
The following code represent thread-unsafe stack implementation
```
1 #define STACK˙SIZE 20
2 int count;
3 double values[STACK˙SIZE];
4 void push(double v) {}
	5 values[count++] = v;
6 }
7 double pop() {}
8 return values[--count];
9 }
10 int is˙empty() {}
11 return count == 0;
12 }
```
## (a) Based on your understanding of the above code, which function(s) in the above stack implementation are thread-unsafe and briefly explain why the data structure is an inconsistent state? Support your answer with one example. (5)
- Push and pop are unsafe because they could be vulnerable to a race condition where they both try to update values at the same time/ accessing at similar times.
- This data structure is an inconsistent state because there is no bounds on the variables, is DANGEROUS

## (b) A candidate 'solution' for the thread-unsafe stack implementation is shown below. However, the solution contains shortcoming(s), Identify and explain the error(s) may accord. (8)
```
1 #define STACK˙SIZE 20
2 int count;
3 double values[STACK˙SIZE];
4 pthread˙mutex˙t m1 = PTHREAD˙MUTEX˙INITIALIZER;
5 pthread˙mutex˙t m2 = PTHREAD˙MUTEX˙INITIALIZER;
6 void push(double v) {
	7 pthread˙mutex˙lock( & m1);
	8 values[count++] = v;
	9 pthread˙mutex˙unlock( & m1);
10 }
11 double pop() {
	12 pthread˙mutex˙lock( & m2);
	13 double v = values[--count];
	14 pthread˙mutex˙unlock( & m2);
	15 return v;
16 }
17 int is˙empty() {}
	18 pthread˙mutex˙lock( & m1);
	19 return count == 0;
	20 pthread˙mutex˙unlock( & m1);
21 }
```

- Uses two separate mutexes - doesn't actually stop a race condition in some scenarios because pop and push are still working separately.

## (c) Update the code in b) so the stack implementation will become thread-safe. Briefly explain your logic. (7)
- update so that both use mutex 1, thats all you need, get rid of mutex 2!

# Q3
## (a) What is a context switch? Why is it important for the operating system to minimise the number of context switches?
- Switches from one process to another - often triggered by an interrupt or trapping to the kernel or sys call or scheduler. 
- Saves context of previous one in PCB and loads up new one
- Context includes PC, pid, memory, registers etc

## (b) A multi-user system used to work well, with low response times and good throughput. Now many users use a package for automatic program verification, and as a result the response time is high, and throughput low. How would you distinguish between overloaded CPU, thrashing and overused disk as a possible reason? (4)
- Overloaded CPU: cpu has too many processes active at the moment, need to remove some, characterised by low throughput?
- Thrashing: swapping pages too much: characterised by no throughput?
- Overused disk: full disk, characterised by long disk head movement times

# Q4
## (a) Why is it important that critical sections in kernel code take as little time as possible? (6)
No other processes can enter their critical sections (or a limtied amt depending on the type) until a sectin is out of theirs.


## (b) Games programmers would like to issue commands to the graphics card directly, bypassing the Os. What are the effect o of this for stability and security? (6)
- If executing in kernel now:
- bad security wise because its in privileged mode and want to use that as little as possible 
- bad stability because if crashes then whole system crashes.

## (c) Consider the following kernel code fragment (8)
![[Pasted image 20260603174049.png]]

This code is part of a device driver for a character device. The intention is that the
driver stores a list of messages. The procedures removeMessage and addMessage
– 6 – Turn Over
Non-alpha only
are called as part of a system call whenever a message should be removed from and
added to this list, respectively.
This code compiles but does not work as intended. It contains errors not necessarily
limited to memory management and concurrency. Identify the errors and suggest
a remedy. Your solution should maximise the degree of concurrency. For critical
sections, it is enough to indicate the beginning and end of a critical section, and
whether you would use semaphores or spinlocks. 

```
1 struct messageList –
	2 char *message;
	3 struct messageList *next;
4 ˝;
5
6 struct messageList *msgList = NULL;
7 int msgSize = 0; // the total size of all messages
8
9 // Called as part of a system call.
10 // removes message from list and copies it into buffer.
11 int removeMessage (char *buffer, size˙t length) –
12 // buffer is pointer to user space
	13 memcpy(buffer, msgList-¿message, length);
	14 msgList = msgList-¿next;
	15 msgSize = msgSize - length;
	16 return length;
17 ˝
18
19 // Called as part of a system call.
20 // adds message from buffer to message list.
21 int addMessage (const char *buffer,
	22 // buffer is pointer to user space
	23 size˙t length, // size of the buffer
	24 loff˙t offset) –
25
	26 memcpy(msgList-¿message, buffer, length);
	27 msgSize = msgSize + length;
	28 return length;
29 ˝
```

I DONT KNOOOOW
