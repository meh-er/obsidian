#Theory 

Stack canaries or security cookies are tell-tale values added to binaries during compilation to protect critical stack values like the Return Pointer against [[buffer overflow]]  attacks. If an incorrect canary is detected during certain stages of the execution flow, such as right before a return, the program will be terminated. Their presence makes exploitation of such vulnerabilities more difficult but not impossible.

Below is a schematic implementation of a canary implemented to stop a stack-based [[buffer overflow]].

![[Pasted image 20260221215350.png]]
Stack canaries will be checked for their value just before the return to the calling function, which is the moment at which the attacker will gain control over the [[instruction pointer]] as their overwritten value for the [[return pointer]] is loaded into the [[instruction pointer]].


![[Pasted image 20260221215531.png]]

The null canary would be the simplest for the compiler to implement. It places 4 NULL bytes just before the SFP and RP. As this is a predictable value, an attacker may still be able to bypass the canary. The `read()` function, which is vulnerable to buffer overflows, does allow NULL bytes to be written.

The terminator canary introduces two more hex values that attempt to terminate string operations, 0x0a and 0xff. These values are again predictable, and can be bypassed with relative ease under the right conditions.

A random canary will offer better protection. Is usually consists of a NULL byte followed by 3 random bytes.  The NULL byte would attempt to terminate string operations, while the 3 random bytes will make the canary less predictable to the attacker.

The random XOR canary will be like the random canary, except it will be XOR'ed against a nonstatic value in the program (usually the [[base pointer]] EBP). As operating systems nowadays run with [[ASLR]] activated, EBP will not be static across runs of the program. This adds an extra layer of randomization to the cookie, making it hard to predict this value.