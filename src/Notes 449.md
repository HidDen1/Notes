# Introduction to System Software
## 1/8
* Hello world program
#
    #include <stdio.h>
    int main(){
    printf("Hello, world! \n");
    return 0;
    }
* whereas java defines size of int, in C int is defined by the native word size (cpu bit size)
## 1/10
* Shorts in C are at least 16 bits
* short <= int <= long
    * short < long
#
                    short   int   long
    16 bit cpu:     16      16    32
    32 bit cpu:     16      32    32
    64 bit cpu:     16      32    64
                            64    64
* C does not run on every system reliably today, due to no control over the language or compilers
* adjective words (short, long, etc) can be applied to an int
* Keywords: signed & unsigned
    * adjective to describe ints (positive v negative)
        * a bit will be used to describe the sign or not
## 1/17
* keywords affect compile-time
* sizeof keyword - comptime construct & constant
    * sizeof(expression or type)
    * Ex: sizeof(char) - returns: how big is this type? 1
    * Ex: sizeof(int) - returns: 4 on a 32-bit (32 bit = 4 bytes)
##### Operators
    Arithmetic
    *
    /
    % - can be used on doubes & floats
    +
    -
    ()
    same as in java
    Comparison
    <
    <=
    >
    >=
    ==
    !=
    false will return 0, true will return anything other than 0
    Logical
    &&
    ||
    !
    Bitwise
    & - compare bits Ex: 1100&1010= 1000
    | - compare bits Ex: 1100|1010 = 1110
    ~ - turn bits to other values Ex: ~010 = 101
    ^ - XOR, ecclusive or Ex: 1100^101 = 0110
    << - left shift operator: 1100(2) << 2(10)
    >> - right-shift
* Assignment
    * Declaring Variables: Type identifier
        * Must be letters, numbers, _
        * Must start w/ letter or _
        * shouldn't start w/ _
### 1/22
* In C89, subtle difference between declaration block and usage block
    * all declarations must occur at the top
    * in C99 or later, declarations can be done anytime
* Block comments "/* */"
    * No line comments officially exist, but it does somehow
* printf("Hello, world!\n");
    * literal text, and it displays literally
* printf("x is %d \n" x);
    * % says that a value has to be interpolated
        * %d - int
        * %o - octal
        * %x - hex
        * %f - float
        * %e - 1e9
        * %g - %f or %e
        * %s - string
        * %c - char
        * %p - pointer
        * %u - unsigned
 * scanf() gets value from user
    * scanf("%d" &x); 
        * takes an int
 ### 1/29
* Usage of goto
    * Error handling
    * Not used in 449
* compiler reads from top to bottom
    * requires any functions used in main to be declared prior to main
    * by using function prototype, ex: int f(int);, allows one to declare a function before its implementation
    * in C89, prototyping is not necessary exactly because of "defaulting"
    * in C99 prototyping is required
* Arrays
    * Homogenous, aggregate data structures
    * int a[10];
    * how to find length?
        * not an object
        * sizeof(a) = 40 //in this case
        * when passing arrays, the length is also required
        * sizeof(a)/sizeof(a[0]) works when in scope
### 1/31
* Recall in C89, declarations cannot be made after the first usage
    * Thus, making an array with a variable length:
#
    int n;
    scanf("%d", &n);
    int[n];
* This is illegal
    * However, it is perfectly legal in C99
    * There is a way to achieve this in C89, just not with this syntax
* What is normal in Java is an OUT OF BOUNDS EXC.
    * However, there are no "exceptions" in C
    * So how do these problems manifest
        * Crash
        * Silent corruption of data
            * What normally would seem like a math error is actually the array destroying or creating data in wrong places
            * A crash only occurs when one goes over the array bounds by thousands
            * It will normally just assign a value in memory close to the array, corrupting current and future variables
            * In java, the JVM had the ability to know how to check this problem
            * C does not have a VM, so it has no way to catch this issue
            * This is the responsibility of the programmer to ensure the program is not corrupting the system
* In C there is the Structure (Struct):
     * It is like an array in that it is a contiguous block of variables
     * However, it is able to contain different types of variables
     * It is not guarenteed the addresses are all neatly aligned
        * This is due to padding for storing different variables (like chars with ints)
     * Fields are accessed with dot
#
    struct student{
        int age;
        float qpa;
        char name[20];
    }
    
    int main{
        struct student bob;
        bob.age = 20;
        
        return 0;
    }
* A struct is a value type
    * Meaning when it is passed in an arugment, its values cannot be changed
        * because it is a pass by value, not reference
        * This is not true for arrays, they are passed by "reference"(pointer)
        
* Strings
    * Array of chars
    * Sentinel value (NUL - '\0')
    * Functions:
        * strcopy(str, "Hello");
        * strcmp(a, b); //where a & b are strings
            * Returns same numerical value java does for compareTo()
        * strlen
            *
        * strcat(a, b) //where a & b are strings
            * a is a source & a destination
            * a will have the result of the function
    * How do we know what part is currently occupied?
        * Explicit length variable (programmer made & designed)
        * Sentinel value (like a null in java)
### 2/5
* strcopy is an unsafe function
    * When writing, it can go into unallocated memory
        * Because it does not have a knowledge of the length
    * strncopy will take a numerical value to know its length
        * However, it doesn't necessarily produce a C string
            * one that has a \0 (NUL) at the end
* A pointer is a variable that holds an address
    * Declared by an operator * before the variable name
#
    int x;
    int *p;
    p = &x; // p holds address of x, x holds 3
    x = 3; or *p = 3 //changes the value at what p is pointing to
### 2/12
* Pointers as parameters
    * Use to return a value
    * Avoid cost of copying a giant struct or value
* Arrow pointer dereference
    * struct pixel p;
    * (*p).red
    * p->red
        * These two statements calling red are equivalent in nature
* Why strings do not need & for their address when passing to scanf
    * scanf("%s", str); //Correct statement
    * The name of an array stands in for its address
* Pointer Arithmetic
    * C scales by type
    * Meaning adding 1 to an address will move it by a (type) size (possibly 4 addresses)
    * This will go for any type, particularly for arrays
### 2/14
* malloc(int size)
    * Allocates memory of the int size
    * functions sort of like new ___ in java
    * allows dynamic allocation of memory
    * enables us to create runtime-specified sizes for things like structs or arrays
    * if it fails it will return NULL
    * if something is not freed at the end of its use, it will create a memory leak
        * Meaning long-running programs would eventually run out of space
* Scope
    * where in the code you can use a variable name
    * enforced by compilers
        * encapsulation - cannot be used elsewhere
        * reuse names
    * Compile time (static) concept
* Lifetime
    * when memory is allocated for a variable
    * Runtime (dynamic) concept
#
                Scope             Lifetime
    "local"     Block      function call->return
    auto var
    
    "global"    File       Program start->finish
    
    "Malloc'd"  pointers      Malloc -> Free
* "static" keyword locally
    * allows for limited scope (block) but program lifetime
### 2/19
* From code to software
    * C source (.c files)
    * Preprocessor (C source -> preprocessed source)
        * "#include" takes header files and puts it into our code
    * Compiler
        * Takes the preprocessed source and turns it into object files
    * Object Files (.o)
        * Mostly machine code
        * Meaning source code written by the programmer
        * But what about the library functions? Other C files we wrote?
            * The Linker (the next step)
    * The Linker
        * Links all source files dependent on eachother
        * This way the code now contains all necessary code files (like the library functions)
        * End result...
* Executable file
    * Is now a runnable file
        * Kind of
        * It contains the POTENTIAL for a program
        * It is in storage though, not memory
        * It has to get to memory to run
        * Since it is compiled, it can be run anywhere
            * No requirement of source code necessary
    * What do we need to store?
    * Code, Data, More??
        * Resources like images and sounds
    * Agreed upon on a common format (much like with bitmap tags)
        * Every system has a different file format (for executables)
    * Old executable file formats:
        * a.out (assembler OUTput)
            * Oldest UNIX format
            * Not used anymore
        * COFF (Common Object File Format)
            * Older UNIX format
            * Not used anymore
            * Ancestor of Portable Executable File Format (PE)
                * Used by windows
        * ELF (Executable & Linking Format)
            * Linux
        * Mach-O
            * Mac
### 2/21
* Program's address space
    * When a program is set to execute by the OS, it needs to be in memory to run
        * The OS then allocates an "Address soace" in RAM
        * This space contains different "blocks"
            * Text (code)
            * Data (globals)
            * Data (heap)
                * Runtime variables
            * Stack
                * Keeps track of runtime in general
        * If you try to access space OUTSIDE OF the program's space OR in an unauthorized address (the program's space, but not in use just yet)
            * Crash
* The Linker
    * Static Linking
        * Copy code into executable at compile time
        * Done by "linker"
    * Dynamic Linking
        * Copy code into Address Space at load time or later
        * Code is from an archive file
            * DLL: Windows
            * SO: UNIX
        * Done by link loader
        * At load time
    * Dynamic Loading
        * copies data & code from some archive file into address space
        * At runtime
    * Which of these is the best way to link???
### 2/26
* A pointer but instead of a variable a function??
    * A pointer function
        * Gives the location of *code* in memory rather than data
#
    int f(int x){
        return x;
    }
    
    int main(){
        int (*g)(int x);
    
        g = f;
        printf("%d\n", g(3));
        return 0;
    }
* X86
    * Not MIPS
        * That is a reduced instruction set
        * Maybe at 130 instructions at most
    * This is a complex instruction set
        * Hundreds of instruction sets, well over 700
    * Lets give an example of an instruction
        * F2XM1 - Compute 2^x-1
            * Except x has to be between -1 and 1
* 32-bit x86 general purpose registers
    * EAX - Accumulator
    * EBX - Base
    * ECX - Counter
    * EDX - Data
    * ESI - String Source
    * EDI - String Destination
* Other registers
    * EIP - Instruction pointer
    * ESP - Stack pointer
    * EBP - Base or Frame Pointer
    
    * EFLAGS - Flag register
* Thats a lot of Es isn't it?
    * It is for Extended
    * Meaning without it, its just a 16 bit register
        * for compatability
    * If you change AX, you've changed the lower 16 bits of EAX
        * these exist for every register
        * some registers allow access to a single byte
        * but only the first four general purpose regs
### 2/28
* Activation record
    * A stack basically keeping track of what "function" is running
### 3/12
* Local variables are typically allocated to the stack activation record
    * For arrays, this is like a "dynamic allocation"
    * The stack will have a huge activation record to get room for the array plus lots of padding
    * This is what enables vulnerabilities if the array takes input that isn't checked right (scanf)
    * You can overrite data and eventually overrite a jump so now the user can jump to any address they want
        * allowing them to run code in our program
        * ..and add code to the program thru input redirection
        * and now the user can do anything
        * so gets() and scanf() are vulnerable
            * scanf can be told to be careful using %#s # = a number
        * use fgets() because a parameter is the size
* Null (NUL) is address 0x00000000
    * Anytime it is accessed, the CPU knows and tells the OS to crash you
### 3/14
* OS jobs:
    * Manage resources
        * Keep track of who gets what ram or bandwidth or HD space
    * Abstract details
        * Prevent maliciousness
        * Keep details we don't need away
            * prevent confusion
* There are details we are concerned with though:
* Memory Management
    * We need to know what is taken and what is free
    * Simple when thinking about the Stack
        * This is where it begins, and the rest is free
    * But what about the heap?
        * Memory can be freed in the middle, far different from the stack where it is freed from "top to bottom"
        * Meaning we don't know yet what exactly is freed and what isn't
    * Maybe use "chunks"
        * designate a space of bits that we map as either used (1) or free (0)
        * But if we are mapping a small space, say a chunk size of a byte
            * We are wasting 11% of space now
            * So what do?
        * Make the chunk size huge
            * Now its efficiently mapping
            * But what if we want to use an int of space?
            * Well you'll get at least that, but now you have the rest of the chunk empty
        * We have to make it big so to waste less space, but not large because it could fragment easily
            * We have to benchmark it, figure out what will be comfortable for the program
            * Typically 4096 bytes (4 Kbytes)
        * Memory "chunk" by OS memory: Page
            * chunk of disk: block
        * But maybe we want to decrease the space used even more than 4 kb
            * Compression?
                * By writing the data in a bigger base, we can write down the amount of space filled with (1)s rather than with the 1s themselves
                    * Called run length encoding
                * Encode lengths of runs and sparse places using a linked list
                    * Now it has information about what is and isn't freed, and their lengths, rather than the actual information
                        * By omitting the free space and writing down the used space