#Boot

##Programmable ROM
- small non-valatile memory loaded with vendor specific software. 
- Perfoms some basic checks (POST) and finds the boot device; Runs the boot program. Power on self-test.
- Usually Boot Program is stored on block 0 (boot sector) of a boot disk. 
- System can be booted from any other devices as well if you have access to ROM.


##Boot Process -Steps
- Kernel checks the Memory Availability.  
- Probles & COnfigures hardware devices.
- Updates the entries in /dev directory.
- set up all RAM tables to hold the processes information, memory allocation and open files,etc.  
- At the end of the booting, KERNEL creates the **init** process.  

   		$#run when start-up
    	$mv myscript /etc/init.d/.  
    	$sudo chmod +x myscript 
    	$#ln -s to /etc/rc2.d

##Dummy Processes.  
- Process that cannot be killed is known as DUMMY process. 
- used for crucial system fucntions.  
- Created by kernel during booting process, part of the kernel.  
- Some samples: virtual memory paging services(vhand). periodic buffer flushing service. 
- To see dummy process, ``$ps -ef`` 

##OS Run Levels
- OS runs in different levels indicating a specific mode.
- init command changes the run level of OS(init process is different from ``$init`` command).  
- Different levels have the different limited set of processes running.  
- Different sample level  
0 - halt   
1 - single user mode  
2 - multi-user mode 
3 - full multi-user  
4 - Reserved. Also X-windows.  
5 -x11 graphical mode
6 - Reboot. 

    
    	$runlevel # to see runlevel
    	$sudo init $runlevel # swithc run level
		$duso init 6 #e.g , to reboot.


#Process 
##Process Hierarchy
- KERNEL Process is created as part of the booting. 
- KERNEL first loads the init process. 
- All other processes are created by init. 
- Each process is given an unique process id(PID)
	- PID of init is 1.
	- PID of kernel is 0.
- Each process is associated with its creator - Parent- identified by the parent process ID (PPID)
- init process is the parent of all processes. 
- when parent process of any process dies, it will be linked to **init** process as its parent.  
- Each processs runs with a specific priority(PRI)
- E.g:
	- for Ubuntu. 0~139. 
	- 0~99 real time. 
	- 100~399 for users.
	- nice value: nicer a process is, more willing to give up resource to process with same priority.
	- -20(highest) <Nice value<=19 (lowest)
	- PRIORITY = 20 + NICE (so , PR between 0 ~ 39 map to 100~139) 

- ``$ps -ax`` list all process.

##Process Creation
- New processes are crated using either ``fork`` or ``exec`` command.  
- ``fork`` creates an independent process .
	- Except kernel everything else is created using ``fork``.
- ``exec`` creates a new process as a sub-process(thread) of the calling program.  
	- it shares the memory and other resources of the parent process.  
- E.g: a shell script with ``find`` command in it.  
	- Shell creates the independent (fork) process to execute the shell script.
	- script process create(``exec``) the sub-process to execute the ``find`` command.
- Kernel allocates the memory to the new process known as ADDRESS SPACE.  
- Address Space contains four main segments.
	- Text -stores the program instructions.  
	- Data - contains program variables (initialized)  
	- BSS/Heap Memory -contains un-initialized program variables (synamically shrinking as used)
	- Free Store -unused memory; used as programs allocates.
	- Stack -stores local variables and function parameters (dynamically grows)

## Process Execution Modes.
- Kernel Mode.
	- When process is executing kernel instructions is known as in KERNEL MODE.  
	- Control transfers to the Kernel and Kernel carries out the instructions on behalf of the user process.  
	- During this mode, process can access entrie Address Space of any process.  
	- e.g: User process is making a System call, interrupt, generating exception, etc.  

- User Mode.
	- Process created by user and executing in CPU is known as USER MODE.  
	- It can access only its Address space and can't access any other user's space.  
![Process life Cycle](http://image.slidesharecdn.com/unixinternalspart1orb-100712110148-phpapp02/95/unix-internals-os-architecture-15-728.jpg?cb=1278932786)

##Process Interruption - Two Types.  
- **Interrupt**: Caused by some event that is external to and asynchronous to the currently running process.  
	-e.g. Completion of IO.
- **Trap** Error or exception condition generated within the currently running process.  
	- e.g, illegal access to a file, arithmetic exception. 

##Common Signals
- SIGUP ----Hang-up.  
- SIGINT ---Interrupt.
- SIGQIT ---- Quit.
- SIGINS -----illegal instruction.
- SIGTRAP ----Trace Trap.
- SIGKILL -----kill.
- SIGSYS -----Bad Argument to System Call. 
- SIGPIPE ----Write on pipe with no one to read it.
- SIGTERM -----software termination signal from kill.  
- SIGSTOP -----Stop signal.

see also: ``/usr/include/sys/signal.h``
    