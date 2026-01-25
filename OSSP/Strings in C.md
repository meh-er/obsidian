---
tags:
  - OSSP
---
- A string of characters is a 1D array of characters
- ASCII code (1 byte) of each character element is stored in consecutive memory locations
- String is terminated by the null character `\0` (ASCII value 0)
- The null string (length zero) is the null character only

```
#include <stdio.h>
int main()
{
	char name[] = "comp Sc";
	printf("%s\n", name);
}
```

#### Reading and printing strings
- A string can be read using `scanf`
	- format conversation specifier for a sequence of non-white-space characters is `%s`
	- e.g. `scanf("%s,a)` will sore only "Comp" for user input "Comp Sc"
- A string can be printed using `printf()` with `%s`

#### Library string.h
- Library functions are available to manipulate strings
- A list of commonly used string manipulation functions:
	- `strcpy()` - copy a string
	- `strcat()` - concatenate two strings
	- `strlen()` - get string length
	- `strcmp()` - compare two strings

#### String problems
- Need to ensure that **sufficient** memory is allocated at runtime for storing the string - not automatically done by the compiler
- No checks at run-time (and compile-time), hence common source of errors
- Such "buffer overflows" have been exploited to achieve execution of code supplied by attackers
- Partial solution is to use "safe" functions
- (Different to Java: memory allocated by compiler, length of strings checked at runtime meaning buffer overflow is impossible)

#### Safe string functions
`strncmp()`, `strncpy()`, `strncat()` etc
Example:
`strncpy(char *dst, char * src, size_t num)`
"Copies the first `num` characters of `src` to `dst`. If the end of `src` (signalled by a null char) is found before `num` characters have been copied, `dst` is padded with zeros until a total of `num` characters have been written to it.
No null-character is implicitly appended at the end of `dst` if `src` is longer than `num`. Thus, in this case, `dst` shall not be considered a null terminated C string".
