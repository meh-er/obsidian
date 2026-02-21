#Theory 
- Allocated dynamically during program execution. Unlike [[stack]], it is not freed automaticallly, requires **manual deallocation (in C/C++)**
- Whenever an **object** is created, it is stored in **heap memory**, while references to these objects are stored in **stack memory**.
- Less safe than stack because it is **accessible by multiple threads**, increasing the risk of **data corruption** and **memory leaks** if not handled properly

Key Features of Heap Allocation
- If heap memory is full, JVM throws an error: **java.lang.OutOfMemoryError**
- **Automatic Deallocation** does not happen, a **garbage collector** is needed to **free** unused memory
- **Slower** than stack memory due to **manual allocation**
- Less **thread-safe**
- Typically **larger in size** compared to stack memory
- Heap memory **persists** as long as the entire application is running

e.g.
```
int main()
{
	// This memory is for 10 integers
	// is allocated on the heap
	int *ptr = new int[10];
}
```

