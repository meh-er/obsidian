#Theory 

The methods to overcome PIEs and ASLR are similar. When a binary ELF is position independent, all of the sections will be dynamically-addressed.  The sections of the ELF will start with some ofset - this can be seen by using the same `size` command specified above on a PIE ELF binary.

A PIE ELF binary will be loaded into a different base address in virtual memory each time it is executed. This behaviours increases the difficulty for an attacker to utilise the resources identified earlier, and it also removes the attacker's ability to use statically addressed ROP gadgets.

A sensitive information leak must be conducted in order to determine the base address of the ELF in virtual memory. This can be done by leaking a return address from the stack, a pointer to some location in `.data` and so on.

Some conditions could exist in which the attacker could use a heap based vulnerability to gain code execution, these include:
- A write-what-where condition
- Use After Free
- Double Free