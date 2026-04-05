#SaN 

Reverse engineering:
- Executable code can be written and edited, just like any othre document.
- Ultimately, an attacker/analyst can do **anything** they want with a program

**Definition**: The process of analysing software to understand its functionality, often without access to source code.
	By Examining low-level code, protections can be removed and the funciton of programs altered. Good protection tends to slow down this process, not stop it.
Goals:
- Security Research (e.g. vulnerability discovery, malware analysis)
- Debugging and performance optimisation

### Binaries
- Systems have different **binary formats**
- A C programme is transformed into an executable binary using a **compiler**
- A binary contains **machine code instructions**
- CPUs can support different **instruction sets**
	- A M! MacBook cannot run a binary that was compiled for IntelvmacOS!
	- (However can translate them on the fly, interprets the first time and saves the results)
	- (Apple does this for PowerPC-to-Intel)

### Tools
- [[Debugger]]
	- gdb
- [[Disassembler]]
	- ghidra
- [[Decompiler]]
	- ghidra
- Fuzzing
	- American fuzzy lock??????????

Other tools: 
- strings

**Common techniques**
- Look for strings
- Identify key tests and check the values in the register using a debugger
- Swap *je* and *jne* etc
- Replace the instructions that perform checks with a *nop*

### Defenses
- Dynamically construct the code
	- But attacker can run the code!
- Encrypt the binary
	- The program must include the key for it to be executable
- Obfuscation (e.g. mix data and code so its not clear which is which)
	- Can slow down attacks by months or years
- Online activation
	- Can be completely disabled (patched out) by an attacker
- Require online content
- Require  a hardware dongle
- Hardware-based protection: store and *run* part of the code in tamper-resistant hardware