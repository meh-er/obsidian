#Theory 

The Base Pointer (EBP) (also called the *Frame Pointer*) is a 32-bit register that acts as a **fixed reference point** for the current function's [[stack frame]]. A [[stack frame]] is the portion of the [[stack]] allocated to a single [[function call]], containing its arguments, return address, and local variables.

Unlike ESP (which moves as data is pushed/popped), EBP remains fixed during a function's execution. This stability makes EBP ideal for referencing arguments and local variables via fixed offsets.

##### Function Prologue and Epilogue
EBP is set up in the function prologue (Start of the function) and restored in the epilogue (end of a function)

```
push ebp
; Save the calling function’s EBP (old EBP) onto the stack

mov ebp, esp 
; Set EBP to the current ESP (now ESP anchors the new stack frame)

```


After this, EBP acts as a 'base' for the frame. The [[stack]] now looks like this.


| **Address**  | **Content**              | **Offset from EBP** |
| ------------ | ------------------------ | ------------------- |
| `[ebp]`      | Old EBP (saved)          | `ebp + 0`           |
| `[ebp + 4]`  | Return address           | `ebp + 4`           |
| `[ebp + 8]`  | First function argument  | `ebp + 8`           |
| `[ebp + 12]` | Second function argument | `ebp + 12`          |

Epilogue (Restoring EBP)
```
mov esp, ebp
Restore ESP to EBP (deallocates local variables)

pop ebp
Restore the calling function's EBP from the stack

ret
Pop return address from stack into EIP (Resume execution)
```

With EBP fixed, we use offsets to access data in the [[stack frame]]:
- Arguments: Positive offsets from EBP (e.g. `[ebp + 8]` for the first argument)
- Local variables: Negative offsets from EBP (e.g. `ebp - 4` for the first local variable.)
