#OSSP 
## General structure of a C program


```
#include <stdio.h>
int main(int argc, char** argv) {
		// Declaration of variables
		// Arithmetic and Logical expressions
		fool(); // function call
		// More arithmetic and Logical expressions
		}
void fool() { // User-defined function
		// Declaration of variables
		// Arithmetic and Logical expressions
	}
```

- Program execution starts from main()
- Header file contains pre-defined library functions

### Built-in data types in C

When we deal with **positive numbers only**, we can add **unsigned** before the type and get the range doubled.

```
int a;
// Range is -2, 147, 483, 648 to 2,147,483,647

unsigned int b;
// Range is 0 to 4,294,967,295
```

#### Immediate initialization of built-in variable

```
int i = 5, j = 6;
char c = 'A', d;
float f = 2.33333333;
unsigned int n = 4294967295;
```
All variables except ‘d’ have been initialised during declaration.

Un-initialised variable a ‘garbage’ value initially.

### Constant data

- Constants can be declared as **const**

`const float PI = 3.14159265359;`

- A constant is stored in the read-only segment of the memory
- Any effort to change a **const** variable will result in compilation error

```
const float PI = 3.141159265359;
// ... Some code ...
PI = PI + 1; // THis will be a compilation error.
```



|                        |                                                              |                                                              |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| **C Basic Data Types** | **32-bit CPU**                                               | **64-bit CPU**                                               |
|                        | **Size (bytes) \| Range**                                    | Size (bytes) \| Range                                        |
| char                   | 1 \| -128 to 127                                             | 1 \| -128 to 127                                             |
| short                  | 2 \| -32,768 to 32,767                                       | 2 \| -32,768 to 32,767                                       |
| int                    | 4 \| -2,147,483,648 to 2,147,483,647                         | 4 \| -2,147,483,648 to 2,147,483,647                         |
| long                   | 4 \| -2,147,483,648 to 2,147,483,647                         | 8 \| -9,223,372,036,854,775,808 to 9,223,273,036,854,775,806 |
| long long              | 8 \| -9,223,372,036,854,775,808 to 9,223,273,036,854,775,806 | 8 \| -9,223,372,036,854,775,808 to 9,223,273,036,854,775,806 |
| float                  | 4 \| 3.4E +/- 38                                             | 4 \| 3.4E +/- 38                                             |
| double                 | 8 \| 1.7E +/- 308                                            | 8 \| 1.7E +/- 308                                            |

Helpful types with defined bit width
```
#include <stdint.h>
...

uint32_t c = 0x12345678;
uint8_t f = 0xAB;
uint16_t n = 0xC0FE;
```


## Control flow

**if statement,** used for conditional computation

```c
if (value < 0) {
				sign = '-';
		}
```

**if-else statements,** used for multiple branching

```c
if (testscore >= 90) {
		grade = 'A';
		}
else if (testscore >= 90) {
		grade = 'A';
		}
else if (testscore >= 90) {
		grade = 'A';
		}
else if (testscore >= 90) {
		grade = 'A';
		}
else {
		grade = 'F';
		}
```

**switch statement,** if it matches any one, then all statements inside that case are executed.

```c
switch(expression) {
	case constant-expression1:
		Code Block1;
		break;
	case constant-expression2:
		Code Block2;
		break;
	// ... More case blocks
	case constant-expressionN:
		Code BlockN;
		break;
	default:
		Code BlockDefault;
		break;
	}
```

**for loop**

```c
for(init; condition test; increment or decrement)
{
	// Statements to be executed in loop
}
e.g.

int sum = 0, i;
for (i = 1; i <= N; i++){
		sum = sum + i;
	}
```

**while loop**

```c
while (condition test)
{
		// Statements to be executed in loop
		// Update 'condition'
}
```

**do-while loop**

```c
do
{
		// Statements to be executed in loop
		// Update 'condition'
} while (condition test);

e.g.
int sum=0, i=1;

do{
		sum = sum + i;
		i++;
	} while(i < N);
```

**continue statement** used inside a loop, control skips the statement inside the loop for the current iteration and jumps to beginning of next iteration.

```c
sum = 0;
for (i = 1; i <= 5; i++){
		if(i==3) {
			continue;
		}
		sum = sum + i;
}
```

**break statement**, used to come out of the loop instantly, loop gets terminated

```c
sum = 0;
for(i = 1; i<= 5; i++){
		if(i == 3) {
				break;
		}
		sum = sum + i;
}
```

### Arrays

Array is a data structure

1. stores a fixed-size
2. sequential collection of elements
3. of the same type

```c
int a[4] = {2, 5, 3, 7};
float b[3] = {2.34, 11.2, 0.12};
char c[8] = {'h', 'e', 'l', 'l', 'o'};
```

- Array `a []` is of length 4 and contains only `int`
- Index of an array starts from 0, and then increments by 1
    - `a [0]` is the first element in `a [ ]` and it is 2
    - `a [3]` is the last element in `a [ ]` and it is 7

![[Pasted image 20260120142625.png]]

### Common mistakes

- C compiler/runtime does not check array limits
- If memory protection is violated, then the program crashes due to segmentation fault
- Array size should normally be a constant

**Undefined behaviour (UB)**

- A wide range of things in C cause UB, for example
    - Out of bounds access
    - Signed int overflow
    - Divide by zero
    - …
- When hitting UB, the program can (theoretically) do anything

### Functions

- A function is a block of statements that together perform a task.
- Function definition in C has
    - A name
    - A list of arguments (optional)
    - Type of value it returns (if any)
    - Local variable declarations (if any)
    - A sequence of statements (if any)

```c
return_type function_name (argument list)
{
		// Local variables
		// Statements
}
```

**Example of function call**

```c
// max() function computes the maximum of two
// input integers and returns the maximum
int max(int num1, int num2) {
		int temp;
		if(num1 > num2)
			temp = num1;
		else
			temp = num2;
		return temp;
}

int main() {
		int a = 5, b = 11, c;
		c = max(a, b); // c gets the maximum of a and b
		return 0;
}
```

### Standard library (libc): I/O

**printf() function**

printf() function can be used to print outputs.

It is defined in `stdio.h` library and prototype is:

`printf("%format", variable_name);`

**format** is a place holder which depends on data-type

```c
Examples
printf("%d", var1); // var1 is an int
printf("The value is = %d", var1);

// To print multiple variables together:
printf("%d %c %f", var1, var2, var3);
```

**scanf() function**

scanf() function can be used to receive inputs from keyboard

It is defined in `stdio.h` library and prototype is:

`scanf("%format", &variable_name);`

**format** is a place holder which depends on data=type

```c
Examples
scanf("%d", &var1); //var1 is an int
scanf("%c", &var2); //var2 is a char
scanf("%f", &var3); //var3 is a float

```

**Data types and formats**

![[Pasted image 20260120142646.png]]

**Factorial program in Java**

```c
class Factorial {
	static int factorial(int n){
		if (n == 0)
			return 1;
		else
			return(n*factorial(n-1));
		}
		public static void main(String args[]){
			int fact = 1;
			int number = 4;
			fact = factorial(number);
			System.out.println("Factorial is: "+fact);
			}
		}
```