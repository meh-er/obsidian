NOTE:
if `matrix` is `NULL`, `malloc` failed to give you memory. There is nothing to free.

# Issues
1. Infinite Loops
```

```

2. Missing Null Guard

```

```

3. Edge Case Failures
* Failing to update the Head Pointer
* When appending/deleting, last node's next pointer should be NULL
* Code that breaks if it has one element

4. Pointer Assignment Order
```
// Intention: Insert 'newNode' after 'current'
current->next = newNode; 
newNode->next = current->next; // ERROR: You just pointed newNode to ITSELF!


newNode->next = current->next
current->next = newNode // CORRECT
```

5. Dummy Node
- Code that accidentally treats the sentinel node as a data node
- Code that deletes the data nodes but forgets to preserve sentinel node

6. Short-Circuit Evaluation Violations

```
// CRASH: If current is NULL, current->data is evaluated first and causes a segfault!
while (current->data != target && current != NULL) 

// CORRECT: The left side fails if NULL, stopping the right side from executing.
while (current != NULL && current->data != target)
```


7. Loop Termination Errors

- `while(current != NULL)` used when you want to look at or process **every single node**
- `while(currrent->next != NULL)`: used when you want to stop exactly **at the last node** . If the list is empty, this line immediately crashes because `current` is `NULL`.
















# Memory Management Issues
 
1. Memory Leaks
```
void process_data() {
    char *buffer = malloc(1024);
    // ... do some work ...
    if (error_occurred) {
        return; // ERROR: Leaks 'buffer' because free() is skipped!
    }
    free(buffer);
}
```

2. Dangling Pointers & Use-After-Free
``` 
int *ptr = malloc(sizeof(int));
*ptr = 42;
free(ptr); 
// ptr is now a dangling pointer

printf("%d\n", *ptr); // ERROR: Use-after-free!
```

3. Buffer Overflows
```
char buffer[10];
strcpy(buffer, "This string is way too long!"); // ERROR: Buffer overflow
```

4. Double Free
```
free(ptr);
// ... some code ...
free(ptr); // ERROR: Double free!
```

5. Uninitialized Pointer Dereferencing (Wild Pointers)
```
int *ptr; // Wild pointer (uninitialized)
*ptr = 100; // ERROR: Writing to a random memory location!
```

6. Returning Pointers to Local Stack Variables

```
int* get_matrix() {
    int local_array[4] = {1, 2, 3, 4};
    return local_array; // ERROR: local_array will not exist outside this function
}
```


e.g. pointer
```
int target = 42;    // A normal integer
int *ptr;           // POINTER DECLARATION: The '*' means ptr will hold an address
ptr = &target;      // Use '&' to get the memory address of target and store it
```

e.g. dereference
```
// Assume 'ptr' already points to 'target' (which equals 42)

printf("%d", *ptr); // DEREFERENCING: Reads the value at ptr's address. Prints 42.

*ptr = 99;          // DEREFERENCING: Writes to the address. 
                    // 'target' is now changed to 99!
```


| Feature            | Pointer Declaration                           | Dereferencing                                 |
| ------------------ | --------------------------------------------- | --------------------------------------------- |
| Where              | Next to a data type (e.g. `int *`. `char *`). | Next to active variable name in a statement   |
| What does `*` mean | This variable **stores an address**           | Go **inside the address** this variable holds |
| Example            | `int *p`                                      | `*p = 5`                                      |

logic for deleting a node in a linked list:
Preserve the next address in a temporary pointer first:

```
struct list_t *nextItem = items->next;
free(items);
items = nextItem;
```

Fix for returning local variables:
allocate dynamically on heap using malloc so it persists
```
struct list_t *newItem = malloc(sizeof(struct list_t));
// Then use arrow syntax instead of dots:
strncpy(newItem->entry.title, newTitle, BUFFERLENGTH - 1);
```

Fix for not taking in size:
Manually limit copy size to buffer and ensure null termination:

```
strncpy(newItem.entry.title, newTitle, BUFFERLENGTH - 1);
newItem.entry.title[BUFFERLENGTH - 1] = '\0';
```
# C Crash Course
## 1. Basic Variables and Pointers
A pointer holds **an address** - points to where something lives in memory. 
```
int x = 5;      // x holds the value 5
int *p = &x;    // p holds the ADDRESS of x
                // & means "give me the address of"
                // * means "go to that address and get the value"

printf("%d", x);   // prints 5
printf("%d", *p);  // also prints 5 — "go to address p, get value"
```

## 2. Structs
A struct is just a way to **group related variables together** under one name.
```
struct List_t {
    char *elem;           // a pointer to some text
    struct List_t *next;  // a pointer to ANOTHER List_t
};
```
This is a **linked** **list**.
If NULL - marks end of list

## 3. Malloc
Malloc reserves a chunk of memory and gives you its address.
```
// WRONG — arg points to garbage, writing to it will crash
char *arg;
sprintf(arg, "hello");

// RIGHT — malloc gives arg a real place to write to
char *arg = malloc(256 * sizeof(char));
sprintf(arg, "hello");   // now safe — we have 256 bytes reserved
```

## 4. Arrow operator `->`
When you have a **pointer to a struct**, you use `->` to access its fields instead of `.`
```
struct List_t *node = malloc(sizeof(struct List_t));

node->elem = "hello";   // set the elem field of the struct node points to
node->next = NULL;      // set the next field
```
`node->elem` is just shorthand for `(*node).elem` - go to struct, get field elem


# REMEMBER
- **Can't dereference NULL**

# RED FLAGS
```
// Red flag 1 — pointer declared but never malloc'd
char *p;              // ← no malloc anywhere after this?  BUG

// Red flag 2 — using pointer before checking if NULL
head->elem = x;       // ← is head ever checked for NULL?  BUG

// Red flag 3 — returning address of local variable
return &x;            // ← x dies when function returns     BUG

// Red flag 4 — malloc but no free anywhere
malloc(256);          // ← grep for free() — not there?     BUG

// Red flag 5 — off by one in array
char buf[5];
buf[5] = 'x';         // ← valid indices are 0-4 only       BUG
```

Ask every pointer:
```
1. Was it malloc'd (or assigned) before use?
2. Could it be NULL when it's dereferenced?
3. Does it point to something that's still alive?
4. Is it freed exactly once?
5. Is the malloc the right size?
```

Linked list checks
```
□ Is head initialised before being dereferenced?
□ Is a new node malloc'd each iteration (not reusing the same one)?
□ Does node->next get set before head moves?
□ Is the last node's next set to NULL?
□ Are both elem AND the node itself malloc'd separately?
```

# Linked Lists
