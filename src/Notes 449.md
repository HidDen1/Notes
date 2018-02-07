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
