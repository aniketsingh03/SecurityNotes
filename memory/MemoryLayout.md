## Assembly Code Structure
The assembly code is divided into various segments which are as follows: 
- `.data` - representation of that segment which holds all the uninitialised data. This segment has fixed size.
- `.bss` - (block started by symbol) that segment which holds all the unallocated variables. This segment also has a fixed size unlike the heap segment which is dynamically allocated.
- `.text` - holds all the program instructions .
    - `_start` - place/label where the assembly program actually starts.
    - `.global _start` - externally callable function so that other parts of the code can use it.

Here is how the memory actually looks like:
<br>
<center><img src="../memory.png" alt="Memory" style="width: 500px; height:400px"/></center>

### Linux system calls
- These are the libraries that linux exposes to get various tasks done. Examples are `exit()`, `read()`, etc.
- A list of all system calls available can be viewed in `/usr/include/asm/unistd.h`.
- System calls are invoked by processes by using a software interrupt - `INT 0x80`.

### Arguments for a syscall
The `eax` register holds the *system call number*, whereas others such as `ebx`, `ecx`, etc hold the arguments to be passed.
For example, for `exit(0)` syscall which has the declaration as `void _exit(int status)`, the `ebx` reg will hold the value for the argument status ie 0.<br>
> **TRIVIA** - All system call numbers can be seen within the `/usr/include/asm-generic/unistd.h` file.

An example of the assembly code segment for `exit(0)` syscall:
```assembly
.text
    .globl _start 
    _start:
            mov $1,%eax        //syscall number is 1
            mov $0,%ebx        //argument is 0
            int $0x80            //call 
```
> **TRIVIA** - A simple way to generate an executable for the assembly code is to run `as -o <file_name>.o <file_name>.s | ld -o <file_name> <file_name>.o`. The first command will generate an object file (relocatable format), and the command after piping links the object file to executable format.

### General Info
- Heap is that section of memory where dynamic data is stored. In order to use any section of heap, one needs to first allocate memory by using `malloc()` function in C.
- The `malloc()` function returns a void pointer, which needs to be typecast into a pointer whose type is that of the variable which needs to be stored.