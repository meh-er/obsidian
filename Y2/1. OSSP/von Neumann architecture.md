#OSSP 
Consists of three main components

1. Central Processing Unit (CPU)
2. Memory
3. Input/Output (I/O) interfaces

## The CPU

The CPU can be considered the heart of the computing system.

It includes two main components:

1. Control Unit (CU)
2. Arithmetic and Logic Unit (ALU)

## The Memory

The computer’s memory is used to store both program instructions and data


![[Pasted image 20260120141525.png]]

## The Input/Output Interfaces

- The I/O interfaces are used to receive or send information from/to connected devices.
- Connected devices are called **peripheral devices**

## Program execution on von Neumann computer

e.g. program:

```c
main() {
	read a;
	read b;
	c = a + b;
	store c;
	}
```

1. Control Unit understands that data needs to be provided by User.
2. Data is read from input device (e.g. keyboard) and brought to the CPU
3. Similar to 1
4. Similar to 2
5. Controller commands ALU to computer addition
6. Controller copies data from ALU to Memory
7. Controller commands ALU to compute subtraction
8. Controller sends data from ALU to display

# Organization of a CPU

### Arithmetic and Logic Unit

**ALU** is the union of the circuits for performing arithmetic and logical operations.



![[Pasted image 20260120141558.png]]

### Control Unit

Control Unit is responsible for step-by-step execution of instructions during a program execution.

### Registers

- Registers are small storage elements that are located very close to the ALU.
- Registers are used as temporary storage during computation.
- ALU can read from and write to registers very fast.

![[Pasted image 20260120141619.png]]

**What is the advantage of having registers inside CPU?**

Register reads or writes have zero-time overhead, i.e. Registers improve processing speed.

### Approx Latency numbers

![[Pasted image 20260120141641.png]]
# Organization of Memory

- Memory consists of small ‘cells’
- Each cell can store a small piece of data
- The cells have addresses. e.g. 0 to n-1
- During Read and Store operations, CPU generates memory addresses.
- Memory Management Unit (MMU) reads or writes from/to the requested memory-location.