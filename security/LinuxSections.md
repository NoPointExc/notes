###  sections: ###
Executable files include four canonical sections called, by convention, .text, .data, .rodata, and .bss.  
 **.text:** section contains executable code and is packed into a segment which has the read and execute access rights.  
 Linux loads the .text section into memory only once, no matter how many times an application is loaded. This reduces memory usage and launch time and is safe because the code doesn't change.

 **.data/.bss:** initialized and uninitialized data respectively, and are packed into a segment which has the read and write access rights.  
.data section contains information that could be changed during application execution, so this section must be copied for every instance.

**.rodata:** contains read-only initialized data, is packed into the same segment that contains the .text section.

###Where are section declared?###
Where are the sections declared? If you look at a standard C program you won't find any reference to a section. However, if you look at the assembly version of the C program you will find several assembly directives that define the beginning of a section. More precisely, the ".text", ".data", and ".section rodata" directives identify the beginning of the the three canonical sections mentioned previously, while the ".comm " directive defines an area of uninitialized data.

The GNU C compiler translates a source file into the equivalent assembly language file. The next step is carried out by the GNU assembler, which produces an object file. This file is an ELF relocatable file which contains only sections (segments which have absolute addresses cannot be defined in a relocatable file). Sections are now filled, with the exception of the .bss section, which just has a length associated with it.

The assembler scans the assembly lines, translates them into binary code, and inserts the binary code into sections. Each section has its own offset which tells the assembler where to insert the next byte. The assembler acts on one section at a time, which is called the current section. In some cases, for instance to allocate space to uninitialized global variables, the assembler does not add bytes in the current section, it just increments its offset.
