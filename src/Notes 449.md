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
    | - compare bits ExL 1100|1010 = 1110
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