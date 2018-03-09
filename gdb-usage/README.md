## Learning to use GDB
### What is gdb?
GDB (GNU Debugger), as the name suggests is a command line tool which is used to debug native binary files with formats like [ELF](http://resources.infosecinstitute.com/elf-file-format/) (Executable and Linkable Format), and supports languages like C, C++, Go, etc. Have a look [here](https://sourceware.org/gdb/current/onlinedocs/gdb/Supported-Languages.html#Supported-Languages) to know more about the supported languages.

The following C file is used:
**SimpleDemo.c**
```c
#include<stdio.h>
#include<stdlib.h>

int add(int x, int y)
{
        int z =10;
        z = x + y;
        return z;
}

main(int argc, char **argv)
{
        int a = atoi(argv[1]);
        int b = atoi(argv[2]);
        int c;
        char buffer[2];
        gets(buffer);
        puts(buffer);
        c = add(a,b);
        printf("Sum of %d+%d = %d\n",a, b, c);
        exit(0);
}
``` 
### Some common commands
- `gdb ./<executable>` - It is used to start the debugger for the executable used. For this example, the executable can be easily generated and tested by running the following set of commands:
    ```
    gcc -ggdb -o SimpleDemo SimpleDemo.c
    gdb ./SimpleDemo
    ```
    > Read more about compiling a program using **gcc** [here](https://stackoverflow.com/questions/3178342/compiling-a-c-program-with-gcc) or read its man pages.
- Once the debugger has started, `list <line no.>` will list the source code starting from the line no. provided.
- `run <argv_1> <argv_2>` - Used to run the program with arguments as **argv_1** and **argv_2**.
- `disassemble <function_name>` - Used to see the assembly level code of the **function_name** specified.
- `break <line_no>` - Used to set a breakpoint at the specified line in the source code. Use `help break` for more help on setting breakpoints.
- `info registers` - Shows the values of various registers (gpr and segment) and flags.
- `x/FMT ADDRESS` - Examine memory at any moment in the program.
    - Here, **FMT** represents the format in which you desire to see the results. Format is a repeat count followed by the format letter (octal, decimal, etc) and a size letter (word, byte, etc). Available format letters and size letters can be seen from its help by running `help x`.
    - **ADDRESS** is the address from where we wish to start viewing memory.


