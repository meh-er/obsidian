---
tags:
  - OSSP
---
We have extensively used two input/output functions:
```
scanf("%format", &variable_name);
printf("%format", variable_name);

```
There are several other functions in C to perform input/output operations.

* `getchar()` gets a character from standard input
* `putchar()` writes a character to standard output.
* `getline()` reads an entire line.

 
Use of files in program
* Large data volumes
* e.g. data from statistics, experiments, human genome, population records etc

For opening a file, `fopen()` is used with requirred access modes
`fopen()` returns NULL if it is unable to open the specified file.
- File pointer fp points to the 'file' resource
	- contains all informaition about file
	- communication link between system and program
- An opened file is closed by passing the file pointer to `fclose()`

### Different modes
- Reading mode (r)
	- if the file already exists then it is opened as *read-only
	- sets up a pointer which points to the first character in it
	- else error occurs.
- Writing mode (w)
	- if the file already exists then it is *overwritten* by a new file
	- else a new file with specified name created
- Appending mode (a)
	- if the file already exists then it is opened
	- else new file created
Additional:
- r+ opens file for both reading/writing an *existing* file
	- doesn't delete the content of the *existing* file
- w+ opens file for reading and writing a *new *file
	- overwrites if the specified file already exists
- a+ open file for reading and writing from the last character in teh file

Functions:
- `getc()` - read a char from a file
- `putc()` - write a char to a file
- `fprintf()` and `fscanf()` - similat to `printf()` and `scanf()`, file pointer is also provided as an input

##### File Errors
Typically, errors happen when a program
- tries to read beyond end-of-file (EOF)
- tries to use a file that has not been opened
- performs operations on file not permitted by 'fopen' mode
- opens file with invalid filename
- writes to write-protected file
##### Error Handling
- `feof(fp)` returns a non-zero value when End-Of-File is reached, else it returns zero
	- ```
	  fp = fopen("somefile", "somemode");
	  ...
	  if(feof(fp)){
		  printf("End of file\n");
		}
	  ```
- `ferror(fp)` returns nonzero value if error detected else returns zero
	- ```
	  fp = fopen("somefile", "somemode");
	  ...
	  if(ferror(fp) !=0)
		  printf("An error has occured\n");
	  ```


#### Random access to a file
Data in a file is a collection of bytes.
We can ***directly*** jump to a target byte-number in a file without reading previous data using `fseek()`

- Syntax: `fseek(file-pointer, offset, position);`
- position: 0 (beginning), 1 (current), 2 (end)

- `ftell(fp)` returns current byte position in file
- `rewind(fp)` resets position to start of file

**Example**
```
int main() {
	FILE *fp;
	
	fp = fopen("file.txt,"w+");
	fprintf(fp,"%s","this is something");
	
	fseek(fp,7,0);
	fprintf(fp,"%s", " C language");
	fclose(fp)l
	
	return(0);
	}
```

The program
1. writes "This is something"
2. Then moves to 7 byte-positions after beginning (8th position)
3. writes "C language" (overwriting any existing data)
Thus, the final content is "This is C Language"

#### Command line arguments in C
We can modify a program to receive arguments from command line.
Syntax is 
```
int main(int argc, char *argv[]){
...
}
```
- argc (Argument Count) and *automatically* stores the number of command-line arguments passed by the user including name of program.
- argv(Argument Vector) is array of char pointers listing all the arguments
	argv[0] is the name of the program
	argv[1] is the first command-line argument etc

#### Large programs
Most programs consist of many C and H files.
Compiling manually is annoying, you need an automated **build** **system**. One such system is 
`make`
It looks for a Makefile in the folder where you call it that contains build commands

Makefiles contain rules:
`<target>: <file0> <file1> ... <command>`
Means: if target does not exist or any of the files has changed, execute the command

Typical file types in this
```
.c Sources
.h Headers
.o Objec files (compiled C)
```

Object files contain the compiled machine code. Do not commit them to version control. They are in the final step linked together for the full executable.

#### The preprocessor
Can define constant and macros:
```
#define CONSTANT 3.14159
#define MACRO(x) ((x) = (x) + 5)
```
macros are sometimes useful to avoid call overheads for small functions but to be used with care
