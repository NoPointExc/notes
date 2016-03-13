###  array as input var=pointer ###

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

the src[] and dst[] in substr are pointers. so, when you call sizeof(src) inside the substr, the return value is 4(the size of a pointer).

### const pointer VS pointer to a const value ###

```char * const a; ```

*a is writeable but a is not. You can modify the value pointed but you can not modify the pointer a itself. a is point to a char.

``` const char *a;```

### how to assign pointed value from a pointed value ###

    
    char *p="123";
    char *a="abcd"; 
    *p=*a;
    
for string in both java and C can't be modified. But the behavior of Java and c are different. For java, compiler will copy and create a new string. For C, the machine will sample tell you the memory is read-only and you can't do that. So, alternatively, you should create a char array for modify rather than a string.

### input var of functions ###

function get copy of input variable rather than variable itself. So function can modify variable without changing the original value. However, for arrays and pointers, it is a different story. The function will get the copy of the pointer rather than the copy of array, so original array will be modified(just as array as input in java).

### must declare function prototype before use ?? ###

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
