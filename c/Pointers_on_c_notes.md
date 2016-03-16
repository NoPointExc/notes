###  Array as input var=pointer ###

when array as input, the input variables are pointers indeed. The sizeof() return 1 for char, return 4 for pointer, return the size of a char array.
for the codes blow,

    main(void){
    	char src[]="abcdefghijklmnopqrsguvwxyz1234567890+-~";
    	char dst[30];
     	int i=0;
    
     	int rst=substr(dst,src,4,40);
     	printf("rst=%d  dst=%s\n",rst,dst);
    }
    
    int substr(char dst[], char src[], int start, int len){
    	int i=-1;
    
    	int srcLen=strlen(src);
    	int dstLen=strlen(dst);
    	if(start<0 || start>=srcLen || len<0) return i;	
    	if(len+start<srcLen){
    		for(i=start;i<len+start;i++) dst[i-start]=src[i];		
    		dst[len]='\0';
    
    	}else{
    		for(i=start;i<srcLen;i++) dst[i-start]=src[i];
    		dst[srcLen]='\0';
    	}
    	return i-start;
    }

the ```src[]``` and ```dst[]``` in substr are pointers. so, when you call sizeof(src) inside the substr, the return value is 4(the size of a pointer).

### const pointer VS pointer to a const value ###

```char * const a; ```

*a is writeable but a is not. You can modify the value pointed but you can not modify the pointer a itself. a is point to a char.

``` const char *a;```

### How to assign pointed value from a pointed value ###

    
    char *p="123";
    char *a="abcd"; 
    *p=*a;
    
for string in both java and C can't be modified. But the behavior of Java and c are different. For java, compiler will copy and create a new string. For C, the machine will sample tell you the memory is read-only and you can't do that. So, alternatively, you should create a char array for modify rather than a string.

### Input var of functions ###

function get copy of input variable rather than variable itself. So function can modify variable without changing the original value. However, for arrays and pointers, it is a different story. The function will get the copy of the pointer rather than the copy of array, so original array will be modified(just as array as input in java).

### Must declare function prototype before use ?? ###

Not necessary. But programmers are suggested to do so.

In ANSI C (meaning C89 or C90), you do not have to declare a function prototype; however, it is a best practice to use them. The only reason the standard allows you to not use them is for backward compatibility with very old code.

If you do not have a prototype, and you call a function, the compiler will infer a prototype from the parameters you pass to the function. If you declare the function later in the same compilation unit, you'll get a compile error if the function's signature is different from what the compiler guessed.

Worse, if the function is in another compilation unit, there's no way to get a compilation error, since without a a prototype there's no way to check. In that case, if the compiler gets it wrong, you could get undefined behavior if the function call pushes different types on the stack than the function expects.

Convention is to always declare a prototype in a header file that has the same name as the source file containing the function.

In C99 or C11, standard C requires a function declaration in scope before you call any function. Many compilers do not enforce this restriction in practice unless you force them to do so.

###  #define vs const ###
```#define``` is a constant and can be used of define array length. On the other hand, ```const ``` is a constant variable(it is a variable) and can not define the length of array.  

### px->a ###
if a is a pointer in a struct, then the Left-Value of this expression is the address of this pointer, the Right-Value is *a. 
 
### sizeof() ###
Queries size of the object or type.  
1) Returns size in bytes of the object representation of type.  
2) Returns size in bytes of the object representation of the type that would be returned by expression, if evaluated.

### Troubleshooting Segmentation Violations/Faults ###

A common run-time error for C programs by beginners is a "segmentation violation" or "segmentation fault." When you run your program and the system reports a "segmentation violation," it means your program has attempted to access an area of memory that it is not allowed to access. In other words, it attempted to stomp on memory ground that is beyond the limits that the operating system (e.g., Unix) has allocated for your program.

Any time your program gives a "segmentation violation" or "segmentation fault" error, review this document for tips on correcting the error.

###Common causes of this problem:###
**Improper format control string in printf or scanf statements:**

Make sure the format control string has the same number of conversion specifiers (%'s) as the printf or scanf has arguments to be printed or read, respectively, and that the specifiers match the type of variable to be printed or read. This also applies to fprintf and fscanf.

**Forgetting to use "&" on the arguments to scanf:**

Function scanf takes as arguments the format control string and the addresses of variables in which it will place the data that it reads in. The "&" (address of) operator is used to supply the address of a variable. It is common to forget to use "&" with each variable in a scanf call. Omitting the "&" can cause a segmentation violation.

**Accessing beyond the bounds of an array:**

Make sure that you have not violated the bounds of any array you are using; i.e., you have not subscripted the array with a value less than the index of its lowest element or greater than the index of its highest element.

**Failure to initialize a pointer before accessing it:**

A pointer variable must be assigned a valid address (i.e., appear on the left-hand-side of an assignment) before being accessed (i.e., appearing on the right-hand-side of an assignment). Make sure that you have initialized all pointers to point to a valid area of memory. Proper pointer initialization can be done several ways. Examples are listed below.

**Incorrect use of the "&" (address of) and "\*" (dereferencing) operators:**

Make sure you understand how these operators work. Know when they should be applied and when not to apply them. As mentioned above, it is common to forget to use "&" with each variable in a scanf call. Remember, scanf requires the address of the variables it is reading in. Especially, know when "&" and "*" are absolutely necessary and when it is better to avoid using them.

### Proper pointer initialization: ###
One common way is to assign the pointer an address to a previously defined variable. For example:


    int * ptr;
    int variable;
    ptr = &variable; 

Or, equivalently,

    
    int variable;
    int *ptr = &variable;

Other common ways include assigning the pointer the address of memory allocated with matrix, vector, calloc, or malloc or other equivalent allocation functions. Remember, a pointer must be initialized to a value (i.e., assigned a value by appearing on the left-hand-side of an assignment statement) BEFORE you attempt to access it!

### Minimizing the use of pointer variables. ###
Also, many times a function requires that an address (corresponding to a parameter of pointer type) be sent to it as an argument (as is true of many of the Numerical Recipes in C functions). The standard function scanf is an example of such a function.
In these cases, it is usually best to simply declare a variable of the correct type before calling the function and just sending the address of the variable to the function. In fact, that is what is intended in the vast majority of these cases. And, that's how you usually scanf:


    	double x_initial;/* initial guess */
    	scanf("%lf",&x_initial); /* Read the initial guess. */
    
For example, see how 'idum' is used below:


long idum = -1; /* initialize idum to be a negative integer */

/* generate a random number from the normal distn.*/
x = normal(&idum,average,stddev);

The function normal expects an address to a variable of type long. That's what we send it without explicitly using a pointer variable in the calling routine.

### Troubleshooting the problem: ###
Check EVERY place in your program that uses pointers, subscripts an array, or uses the address operator (&) and the dereferencing operator (*). Each is a candidate for being the cause of a segmentation violation. Make sure that you understand the use of pointers and the related operators.

**If the program uses many pointers and has many occurrences of & and \*, then add some printf statements to pinpoint the place at which the program causes the error and investigate the pointers and variables involved in that statement.**

Remember that printf statements for debugging purposes should have a new-line character (\n) at the end of their format control strings to force flushing of the print buffer.

ref : [Troubleshooting Segmentation Violations/Faults](http://web.mit.edu/10.001/Web/Tips/tips_on_segmentation.html)

