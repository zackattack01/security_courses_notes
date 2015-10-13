# Memory Layout Overview
- The process itself believes that it owns all of the memory
- From bottom to top:
  - Text segment (the code)
  - Initialized data (`static count int y = 10;`)
  - Unitialized data (`static int x;`)
  - The Heap - area that malloc manages
  - The Stack - holds local variables along with metadata that the program uses to call and return from functions
  - Command line arguments and environment variables, these are set when the process starts

- On push, program will move stack pointer after pushing the value
- On return, program will pop a call off the stack
- Because stack frame arguments and local vars cannot be known at compile time, the program will only know where each variable is *relative* to others

### Summary of Stack and Functions
- Every thread in a process has it's own stack
- This is basically just a chunk of memory used to keep track of the currently running function as well as the functions that were called to get to that point
- Call stack is a specialized version of a stack.
  - Function calls can only be pushed or popped off the top, so it maintains a sequential ordering, FILO
- For each call the stack should store a return address, so the program can continue execution from where it left off
- 
- Very good explanation of the stack and it's security flaws [here](http://arstechnica.com/security/2015/08/how-security-flaws-work-the-buffer-overflow/)

**Note:** 
- `%eip` is the current instruction pointer 
- `%ebp` is the frame pointer
- `%esp` is the end of the stack pointer

###### Calling a function
- Push arguments onto the stack (in reverse order)
- Push on the return address
  - This is the address of the instruction you want to run after control returns to you
- Jump to the function's address    

###### Called Function
- Push the old frame pointer (`%ebp`) onto the stack
- Set the frame pointer (`%ebp`) to where the end of the stack is right now (`%esp`)
- Push the local variables onto the stack

###### Returning function
- Reset the previous stack frame
  - `%esp = %ebp, %ebp = (%ebp)`
- Jump back to the return address
  - `%eip = 4(%esp)`

