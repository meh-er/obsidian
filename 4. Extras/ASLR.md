#Theory 

The goal of ASLR is to introduce randomness into memory locations used by a given task. This will make a class of exploit techniques fail with a quantifiable probability and also allow their detection since failed attempts will most likely crash the attacked task.

ASLR randomizes the **base addresses** of the heap, shared objects, and stack when these segments are mapped into process memory, attempting to introduce enough entropy to prevent an attacker from successfully brute forcing their locations. 

e.g. Without knowledge of the base address of `lib` within a target's memory, attackers conducting the `red2libc` exploit technique have to guess the `system()` symbol address and the `/bin/sh` string's address.