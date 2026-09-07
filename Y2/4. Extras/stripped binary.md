#Theory 

# nonstripped
A non-stripped binary retains full debugging information and symbol tables, making it invaluable for troubleshooting and development.


A non-stripped binary is an executable file that retains its full **symbol table** and **debugging information** after compilation. These components are added during the build process and are critical for mapping the binary's machine code back to human-readable source code.

Key Components
1. **Symbol Table**
	A symbol table is a data structure within the binary that maps:
	- **Function names** (e.g., `main()`, `calculate_sum()` ) to their memory addresses.
	- **Variable names** (e.g. `global_counter`, `user_input`) to their storage locations.
	- **Global vs. local symbols**: Global symbols (visible across the binary) and local symbols (only visible within a function or module).

Example: In a non-stripped binary, tools like `nm` (list symbols) will display function and variable names.

2. Debugging Information
Debugging information (typically stored in formats like **DWARF** or **STABS**) provides granular details to debuggers (e.g. `gdb`) to:
- Map binary instructions to specific lines of source code
- Reconstruct variable types, scopes, and values at runtime
- Identify [[stack]] traces with function names and line numbers.

Debug info is added during compilation with flags `-g` (GCC/Clang) or `-debug` (Rust)

**Example: Non-Stripped Binary in Action**
Compile a simple C program with debug info to generate a non-stripped binary:

```
//hello.c
#include <stdio.h>

int main() {
	int x = 42;
	printf("Hello, World! x = %d\n", x);
	return 0;
}
```


## stripped
A stripped binary has this extra data removed, resulting in **smaller file sizes**, and **reduced exposure** of internal details. 

A stripped binary is a non-stripped binary with tis symbol table and debugging information removed. This process, called 'stripping' is performed using tools like the `strip` command.

Stripping typically removes:
- **Non-essential symbols**: Local symbols function names, and variable names not required for execution.
- **Debug sections**: Entire sections like `.debug_info`, ` `.debug_line, and `symtab, `symbol table)

Some symbols may remain if they are critical for dynamic linking (e.g. symbols needed to load shared libraries like `libc.so`).

Why Strip Binaries?
- Smaller File Size: Stripping removes megabytes of unnecessary data. For example, a non-stripped binary might be 2MB, while its stripped version is 300KB.
- Security: Stripping hides internal function/variable names, making reverse engineering harder.
- Performance: Smaller binaries load faster and consume less disk/memory

#### Stripping Levels
The `strip` command supports partial stripping:
- `strip --strip-debug`: Removes only debug sections (keeps symbol table)
- `strip --strip-all`: Removes all symbols (most aggressive, default behaviour for `strip`).

Common Tools

| **Tool**     | **Purpose**                                     | **Non-stripped e.g.**                                | **Stripped e.g.**                                     |
| ------------ | ----------------------------------------------- | ---------------------------------------------------- | ----------------------------------------------------- |
| `file`       | Check if binary is stripped                     | `file hello_non_stripped` --> not stripped           | `file hello_stripped` --> "stripped"                  |
| `nm`         | List symbols in a binary                        | `rm hello_non_stripped` --> Shows `main`, `x`        | `rm hello_Stripped` --> "no symbols"                  |
| `objdump -t` | Dump symbol table                               | `objdump -t hello_non_stripped` --> Full symbol list | `objdump -t hello_stripped` --> Empty or minimal list |
| `readelf -S` | List sections (check for debug/symbol sections) | `.symtab`, `.debug_info` sections exist              | `'symtab`, `.debug_info` sections removed             |
| `strip`      | Strip symbols/ debug info from binaries         | `strip --strip-debug hello_non_stripped`             | N/A already stripped                                  |
