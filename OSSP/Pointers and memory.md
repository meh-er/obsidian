---
tags:
  - OSSP
---
Definition: A pointer is a variable that contains the **address** of a variable.
If 'p' is a pointer to a variable 'c', then the situation will be like this.
A pointer variable is also stored in the memory.

##### Unary operator &
The unary operator '&' is the **'address-of'** operator.
It gives the address of an object.
so,
	**p = &c;**
assigns the address of c to p, and p is said to 'point to' c/.

##### Unary operator *
The unary operator * is called **indirection** or **dereferencing** operator. It is applied to a pointer to accesses the object the pointer points to.
E.g.
If p is a pointer to an integer object, say c = 5, then
 \ * p
 will give the value of x, i.e. 5
 So,
	 p = &c;
	 c = *p;

#### Declaration of a Pointer variable
- A pointer variable is declared as follows.
	- T *p;
	where **T** is a placeholder for an appropriate data-type.
- p can point to a variable of type **T**

```
Example:

int *p; // p points to int variable
```
--> This means, the expression '*p' is an **int**

##### Pointer to an item of different type
- A pointer should point to an object of the same type.
- There are implications if a pointer points to a different type.
- e.g. **int** pointer 'thinks' the object it is pointing to is **int** and is of 4 bytes size
```
int i;
char c;
int *p; //p can point to int
p = &i; // Correct
p = &c; // Can result in problems
```

#### Use of pointer in expressions
- Pointer variables can appear in expressions
- If 'p' points to the object 'x', then *p can occur in any context where x could.

```
int x;
...
x = x + 10;
```

is equivalent to

```
int x;
int *p = &x;
...
*p = *p + 10;
```

- Unary operators '*' and '&' have higher precedence than arithmetic operators.
	`*p = *p + 10;`
	is
	`(*p) = (*p) + 10;`

![[Pasted image 20260125220212.png]]

- A pointer variable can be assigned to another pointer variable of the same type.

```
int x;
int *p1 = &x;
int *p2;
int *p3 = p1;
p2 = p1;
```

##### Scale factor in pointer expression
- if **p** is a pointer then **p**++ or **p**+1
	- Points to the next object of the same type.
	- Value of p increments by 4 when p is an int pointer or a float pointer
	- Value of p increments by 1 when p is a char pointer.
- scale factor is the number of bytes used by a data-type
- To know scale factor for a data-type, use the sizeof() function
- syntax is: `sizeof(data_type)`

### Pointers and Arrays
- Array is a **sequential** collection of elements of the same type.
- If p points to the first element at a[0], then
	- p+1 points to a[1]
	- p+i points to a[i]

**Computing sum of integer array using pointer**
```
int *p = &a[0];
int sum=0, i;
for(i=0; i<5; i++)
	sum = sum + *(p+i);
```

is equal to

```
int sum = 0, i;
for(i=0; i<5; i++)
	sum = sum + a[i];
```

#### Array 'name' is an address
Array-name is a synonym for the location of the initial element.
So,
	`int *p = &a[0];` 
	can also be written as
	`int *p = a;`
You can think of array-name 'a' as pointer to the array a[]

**Pointer and string of characters**
- A string of characters is a 1D array of characters
- ASCIi code (1 byte) of each character element is stored in consecutive memory locations
- String is terminated by the null character '\0' (ASCII value 0).
- The null string (length zero) is the null character only.


#### Void pointers
Sometimes you don't know what type you point to.

```
int a = 0x12345678;
void *any = &a;
printf("%d", *((int*)any));
```
You *must* cast it to the correct type before using the underlying values.
Pointer arithmetic on void* is illegal in C
You *must* cast it to the correct pointer type before doing ptr arithmetic.

#### Function pointers
Sometimes you want to point to functions:

```
int (*func)(float, int);
```
This example means: func is a pointer to a function that returns an int and takes a float and an int as parameters
* This is useful for callbacks from library code e,g.
### Memory Layout of a C Program
Typical memory layout of C program has the following sections:
1. **Text or code segment** - contains the program i.e. the executable instructions
2. **Data segments** - Two data segments contain initialised and unitialised global and static variables respectively
3. **Stack segment** - Stack segment is used to store all local or automatic variables. When we pass arguments to a function, they are kept in stack. 
4. **Heap segment** - Heap segment is used to store dynamically allocated variables are stored.

![[Pasted image 20260125222115.png]]

#### Function call: low-level view
- For each function call, a stack frame (portion of stack) is allocated
- Stack grows from high address to low address

1. Before foo2() is called: Stack has data of foo1()
2. When foo2() is called: New stack frame for foo2() created
3. Function arguments are copied
4. The address of the instruction that will be executed from foo1() just after foo2() finishes, is copied. This is called 'Return address'
5. Variables within foo2(), which are called 'local variables' are stored
6. After foo2() finishes, local variable d is copied into c of foo1()
7. Following the return address, control-flow returns to foo1()
8. Stack frame for foo2() is released, Hence all local variables die.

##### Stack during function call: Scope
- Scope: part of the program where a variable can be used (or seen)
- Local variables within a function: scope is the function.
	They are allocated in the stack-frame of the function. After the function call, the stack-frame is released.
##### Static variables
- Static variables are stored in the data segment, **not in the stack**.
- The data segment is active during the entire life-time of program
- So, static variables preserve their values even after they are out of their scope.

##### Global variables
- A global variable is declared outside all functions.
- It can be read or updated by all functions.
- Careful:  Do not name any local var in the name of a global var.

```
int A_g = 5; // Global variable

int foo(int b){
	int a=0; // Local variable
	a = a+b+A_g;
	return a;
}

main(){
	int a, b=1; // Local variable
	a=foo(1);
}

```


#### Memory layout of two-dimensional array
C compiler stores 2D array in **row-major** order
- All elements of Row #0 are stored
- then all elements of Row#1 are stored
- etc
![[Pasted image 20260213142706.png]]


![[Pasted image 20260213142635.png]]

**Remember: Array names of 1D and 2D arrays**
* For an 1D array a[]
	* The array name `a` is a constant expression whose value is the address of `a[0]`
	* `a+i` is the address of `a[i]`
* For a 2D array `a[][]`
	* The array name `a` is a constant expression whose value is the address of the oth row
	* `a+i` is the address of the ith row

