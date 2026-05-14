fiestal network etc w2&3
https://www.freecodecamp.org/news/the-cryptography-handbook-rsa-algorithm/#heading-digital-signatures


# Buffer Overflow Practicality
In practice:  
- Compilers may push variables out of order due to optimsations or different standards  
- Compileres may pad variables for alignment purposes

# Buffer Overflow language defenses
- If using C use safe functions (strncpy, strnlen)  
- Use mem safe programming languages (rust)  
- Use hardware enhanced defenses (CHERI)

# ASLR
- Address Space Layout Randomisation  
- Randomises address space so that attacker has to guess  
- Adds random offset to stack each time program runs  
- Jumps are altered in accordance  
- Default in OS  
Counterattack:  
- Inject nopslide + shellcode = area of code with many nops then a shell execution   
- Return to an address and pray its on the nopslide  
- More nop = higher chance

# NX Bit
- Stack should never contain executable code  
- Hardware distinction between text and stack  
- Bit to mark non executable areas  
- Program crashes if IP points to NX marked address  
Counterattacks:  
- Jump to a prexisting function  
- Jump to libc  
- Frankenstein pieces of code together (return oriented programming)

# Stack canary
- Defense for buffer overflows  
- Works under premise that buffer overflow destroys a section of variables  
- Adds a random variable in between return address and stack frame  
- Can check if value has been altered and exit if so

# Buffer Overflow
- Attack when no proper bounds checking is done before input is parsed  
- Can overwrite return address to return to code elsewhere

# Memory management
 Dynamic or static  
Dynamic:  
- Interpreter/VM manages it   
- Example is Python/Java  
Static:  
- Programmer manages it  
- Attacker can exploit bugs  
- Example is C

# Reverse engineering defenses
- Dynamically construct code -> attacker can run code  
- Encrypt binary -> program now requires a key  
- Obfuscation (mix code and data) -> slows down attack  
- Online activation -> able to be disabled  
- Require online content  
- Require hardware donglee  
- Hardware protection (run in tamper resistant HW)

# Reverse engineering techniques
- Look for strings  
- Identify key tests and check registers  
- swap je and jne  
- replace instructions that perform checks with nop

# x86 stack frame
- stack frames created on func calls  
- func will save the previous base pointer (RBP)  
- on return it cleans up the stack and restores old RBP

# x86 linux parameters
void foo(p1, p2, p3, ... pn);  
- parameters p1-p6 are moved into registers  
- parameters p7-pn are pushed onto stack


# x86 stack
 stack starts at high address  
- stack pointer (RSP) always points to top of stack  
- push, pop automatically move the stcak pointer

# x86-64 instructions
mov dst, src - move data   
push src - push onto stack  
pop dst - pop from stack store in dst  
add dst, src  
sub dst, src  
imul dst, src  
ZF - zero flag (1 if res == 0)  
SF - sign flag (1 if res < 0)  
OF - overflow flag (1 if overflowed)  
jmp label - jump to label  
call fn - push IP onto stack, jump to fn  
ret - pop IP from stack and jump to address  
cmp a, b - calculates a-b and sets flags  
test a, b - calculates a&b and sets flags  
je label - jump to label if ZF set  
jne label - jump to label if ZF not set  
nop - no operation  
and dst, src - bitwise &  
or dst, src - bitwise |  
xor dst, src - bitwise ^  
[add] - access mem at add  
[reg] or [reg + offset] - access mem at reg or reg + offset


# Reverse Engineering Tools
- Debugger = allows to stop a program in execution, view values (GDB)  
- Disassembler = allows translating machine code to assembly (Ghidra)  
- Decompiler = allows translating machine code to programming language (Ghidra)


# Binary
- Executable program  
- Contains machine code  
- Unique to the instruction set and OS

# Open redirect vulnerability
- Users control the redirect link  
- Can send an open redirect to a user and steal their info  
- Preventing this is good practice

# Redirects and forwards
- Navigates to another resource  
Redirect:  
- Sends users off site  
Forward:  
- Sends users internally

# Security configuration
- Whole web app needs to be secured  
Best practices:  
- Requires an actual configuration  
- disable unnecessary features  
- Minimum privileges  
- Repeatable security config process  
- Automated checking process

# CORS
- Cross Origin Resource Sharing  
- Allows fetching of resources from different domains  
- Server specifies safe origins   
- Works by using a HTTP header

# Same origin policy
- Standard in browsers  
- Stops simultaneous web applications from accessing each other  
- Can only access DOM, API, cookies of a page with the same domain  
- Sandboxing also helps:  
- Sandboxing = running tabs in separate processes

# Double cookie trick (CSRF)
- Prevention for CSRF  
- Set a secure secret session id in a cookie  
- Submit in cookie and hidden field on form  
- Check server side to see if identical

# CSRF token
- Secure random number for each login  
- Sends with post and checks server side

# CSRF protection
- Don't use GET for sensitive info  
Frameworks with built in protection:  
- Use double cookie trick  
- Use CSRF token

# CSRF
- Request is embdded within some resource that performs an action on some target site  
Example:  
- Form with action and inputs on logged in target client  
- action=http://geemail.com/send_email.htm  
- input name="to"  
- Imbed that link into a different resource eg image  
- <img src="http://geemail.com/send_email.htm?to=hxor@gmail.com">

# Object Reference solutions
- Re-validate that a user has accesst to the object  
- Add data indirection = session specific server side array of account numbers (don't know mapping)  
- Pass lss information to the client  
- Use a MAC with a server side secret key for mssage authenticatio

# Object References

 References to objects within a web application   
- Example is path traversal with forced browsing to serve up an object

# XSS Defences
- Validate user input  
- Output filtering with html encoding and markd up output  
- HttpOnly cookies = not accessible via javascript  
- CSP (Content Security Policy) = a strict CSP prevents inline scripts that limit which domains are requested

# Stored XSS
- Malicious code is stored on the web server   
- Ran when someone accesses that resource

# XSS
- Cross Site Scripting  
- Attacker injects malicious code into website which is then compiled and run  
- Normally javascript or php  
- Stems from poor input validation

# Session hijacking defenses
SID linked to Ip address of client:  
- Can cause problms if behind NAT or transparent proxies  
- ISP proxy pools require use of subnet not IP  
- Subnet can then b stoln by an attacker  
SID linkd to HTTP Headers:  
- Can be faked, guessed or captured

# Session Hijacking
- Sessions tracked with a session ID  
- If you steal the SID you can hijack the session  
- Possible with XSS sniffing and intercption  
- Session fixation = SID from unauthenticated to loggd in SID is subsequently stolen

# Secure Cookie
- Cookie that can only be sent over secure channel (HTTPS)

# Cookie trasnfer
- Happens over HTTP  
- Sent in ASCII plain text  
- Sometimes have a limitd lifetime  
- Server will send cookie   
- User will cache cookie

# Cookie
  
- Saved state on the user end  
- Normally used for caching preferences or a user being logged in  
However:  
- May be shared betwn websites  
- Advertises network tracking IDs  
- Risk of theft and loss of privacy


# HTTP
  
- Hyper Text Transfer Protocol  
- Used for web browsing  
- Specifies message exchanging  
- Client server protocol  
- Works over TCP  
- Server can close a connection but never initiates one  
- Requests normally have a head and a body


# X.509 certificate
Contains:  
- Subject  
- Subject pub key  
- Issuers name  
- Verification done by computing a hash and checking the pub key

# SQLrand
- Dynamic prevention tool for preventing sqli  
- Creates a randomised sql language that changes  
- Attackers who do not know the language cant inject  
- Requires middleware betwen server and db

# Dynamic detection tool AMNESIA
- Use static analysis to create a tool  
- Find SQL query points  
- Build SQL model as NDFA to model the grammar  
- Application calls runtime monitor  
- If monitor detects violation of state machine trigger an error preventing SQL query

# Static Prevention
- Use static code analysis to warn programmers to fix their code  
- Detect common code patterns


# Stages to prevent SQLi
Before deployment:  
- Use programming support  
- manual code review or static code analysis  
Testing/deployment:  
- Pen testing tools  
- Instrumented code  
After deployment:  
- Manual investigate attacks  
- Dynamic remediation w/ alamrs

# DBMS injections
- SQLI injection where you use some feature of the DBMS to inject  
- Example is SELECT INTO file.ext

# Stored procedures
- Custom subroutines that can be called in an SQLI  
- Example is xp_cmdshll in Microsoft SQL Server  
- Allows for code injection

# Inference Pairs
- Infers based on response given  
Blind injection:  
- Exploits visible differences  
Timing attack:  
- Exploits variations in response time

# Piggy Backed queries
- Multiple queries in one input  
- SELECT * FROM users WHERE Login='balls'; drop table users --

# Union queries
- Inject multiple queries with union

# Illegal/incorrect queries
- Causes runtime error to try break the sql service  
- Read sql error to gain info

# Tautology
- SQLI form  
- Always evaluates to true  
- Quasi tautologies sometimes evaluate to true

# SQL Forms
- Tautologies  
- Illegal/incorrect queries  
- Union queris  
- Inference pairs  
- Stored procedures

# SQL Motives
Primary:  
- Extracting data  
- Adding or modifying data  
- Mounting DOS attack  
Auxiliary:  
- Finding injectable params  
- DB fingereing  
- Escalating privilege

# SQL Routes

- User input (GET or POST)  
- Cookies (used to build queries)  
- Server variables (logged by webapps)  
- Second-order injections = injection separat from attack

# SQLI classification
- Route = where injection happens  
- Motive = aims of injection  
- SQL Code = form of SQL injected

# Band fixes SQLI
- Fix for SQLI  
In-band:  
- Use filtering to escape black listed chars  
- Inbuilt MySQL and PHP funcs  
Out-of-band:  
- Prepared statement w/ params  
- Params safely substituted  
ORM and LINQ:  
- Object Relational Mapping for structured DB access  
- LINQ in .NET to access safely

# Tor Hidden Servers
- Architecture that hides the server  
- Choose introduction points to receive conneceetions  
- Advertise service to the database (IPs and Pub Keys)  
- Others query the db and set up a rendezvous point  
- Others send a cookie and RP encrypted with PK  
- You recieve and connect on RP w/ cooki

# Tor Routing
- Users pick 3 proxies (start, middle, exit)  
- Each node establishes a key with the user (DH) along with a hash for data integrity  
- Messages start encrypted by the user with the 3 establishd keys  
- Messages are gradually decrypted at each node  
- Inverse for receiving data

# VPN
-  Virtual Private Network  
- Securely connects you to internet by proxying through a VPN company's servers  
- Use TLS or IPSec to encrypt data  
- Promises anonymity but companies often spy/log traffic

# Defending against LogJam
 Increase DH key size to 2048  
- Disable export-grade ciphers  
- Use unique DH groups  
- Prefer Elliptic Curve Diffie Hellman

# Cipher Downgrading Attack
- Attack on TLS  
- MITM chooses to downgrade to an insecure cipher and then breaks it

# TLS Attacks
- Cipher Downgrading  
- Self Signed Certificates

# SSL/TLS
- Secure Sockets Layer or Transport Layer Security  
- Provides encrypted communication and auth w/ pub keys  
- Supports various crypto algorithms  
- Uses RSA or DH for key exchange

# Mutual Belief
- Protocol provides mutual belief in key for other person if   
- Key is good for other person  
- Other person knows I want to communicate with K  
- Other person knows key is good for me

# Forward Secrecy
Secure against an attacker with:  
- Recording of protocol run  
- Long term keys of principals  
- Ensurees that the session key is fine even if long term keys are exposed

# ARP
- Address Resolution Protocol  
- Router maps IP addresses to MAC addresses
# DHCP
- Dynamic Host Control Protocol  
- Dynamically assigns IP addresses to machines based on the MAC

# NAT
- Network Address Translation  
- Translates public and private IP addresses  
- Private IPs are not unique

# MAC address
- Identifier for a device  
- Assigned by manufacturer

# TCP ports and sockets
- Connection identified by a socket that recieves data  
- Each soket has a port it is bound to  
- Port = buffer  
- Socket = obj with address and port info


