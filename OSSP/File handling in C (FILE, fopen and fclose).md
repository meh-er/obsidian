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