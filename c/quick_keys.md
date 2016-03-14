Pointers on C, Note 2

* %d integer, 2^16

* when "=="+mistake-->'=', no systax error report.

* pointer define, pointer name in

rearrange( char *output, char const *input, in n_columns, int const columns[] ) //define as pointer, use as name input

* tips
putting function prototypes in #include files.
can't initialize 'i' in while or for
be careful with arrays' bounds.

* Enumerated Type
enum Jar_Type {CUP, PINT, QUART, HALF_GALLON, GALLON};
enum Jar_Type milk_jug, gas_can, medicine_bottle;

* declaring pointers

int *a; a pointer named 'a' point to a int.

char *message="Hello world!";
*"Hello world!" is assigned to message not *message *
//equals to 
char *message;
message="Hello world!"

int *pi; // pointer to integer
int const *pci; //pointer to a const int.
int * const cpi; // const pointer to a int.
int const * const cpci; // both pointer and int are constants

 * /#define vs const
 define can be used to define something like the size of array. 

* scope

block scope{}/ File Scope/prototype scope/Function scope

* Linkage
 
?? do not unstand

* storage class: ordinary memory, runtime stack and hardware register

variable declared outside block--> static memory

within block --> (automatic)on the stack

within block+static--> static, exist with the entire duration of the program

with key word *register* --> hardware register

* static variable's space exists at the beginning of the program, default initial to zero. While automatic variable have no default initialization, initialization at runtime.

   
 