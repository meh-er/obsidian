#Theory 

A non-stripped binary retains full debugging information and symbol tables, making it invaluable for troubleshooting and development.

A stripped binary has this extra data removed, resulting in **smaller file sizes**, and **reduced exposure** of internal details. 

A non-stripped binary is an executable file that retains its full **symbol table** and **debugging information** after compilation. These components are added during the build process and are critical for mapping the binary's machine code back to human-readable source code.

Key Components
1. **Symbol Table**
	A symbol table is a data structure within the binary that maps:
	- **Function names** (e.g., `main()`, `calculate_sum()` ) to their memory addresses.
	- **Variable names** (e.g. `global_counter`, `user_input`) to their storage locations.
	- **Global vs. local symbols**: Global symbols (visible across the binary) and local symbols (only visible within a function or module).

Example: In a non-stripped binary, tools like `nm` (list symbols) will display function and variable names.

2. Debugging Information
