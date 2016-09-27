#Linux Process Lifecycle.

![](https://upload.wikimedia.org/wikipedia/commons/thumb/8/83/Process_states.svg/400px-Process_states.svg.png)

##Created.
(Also called **New**) When a process is first created, it occupies the "created" or "new" state. In this state, the process awaits admission to the "ready" state.   
Thison will be approved or delayed by a long-term, or admission, scheduler. Typically in most desktop computer systems, this admission will be approved automatically. However, for real-time operating systems this admission may be delayed. In a real time system, admitting too many processes to the "ready" state may lead to oversaturation and overcontention for the systems resources, leading to an inability to meet process deadlines.

##Ready
A "ready" or "waiting" process has been loaded into main memory and is awaiting execution on a CPU (to be context switched onto the CPU by the dispatcher, or short-term scheduler). There may be many "ready" processes at any one point of the system's execution—for example, in a one-processor system, only one process can be executing at any one time, and all other "concurrently executing" processes will be waiting for execution.  
A ready queue or run queue is used in computer scheduling. Modern computers are capable of running many different programs or processes at the same time. However, the CPU is only capable of handling one process at a time. Processes that are ready for the CPU are kept in a queue for "ready" processes. Other processes that are waiting for an event to occur, such as loading information from a hard drive or waiting on an internet connection, are not in the ready queue.

##Running
A process moves into the running state when it is chosen for execution. The process's instructions are executed by one of the CPUs (or cores) of the system. There is at most one running process per CPU or core. A process can run in either of the two modes, namely kernel mode or user mode.

##Kernel Mode
- Processes in kernel mode can access both: kernel and user addresses.  
- Kernel mode allows unrestricted access to hardware including execution of privileged instructions.
- Various instructions (such as I/O instructions and halt instructions) are privileged and can be executed only in kernel mode.
- A system call from a user program leads to a switch to kernel mode.

##User Mode
- Processes in user mode can access their own instructions and data but not kernel instructions and data (or those of other processes).  
- When the computer system is executing on behalf of a user application, the system is in user mode. However, when a user application requests a service from the operating system (via a system call), the system must transition from user to kernel mode to fulfill the request.  
- User mode avoids various catastrophic failures:
	- There is an isolated virtual address space for each process in user mode.
	- User mode ensures isolated execution of each process so that it does not affect other processes as such.
	- No direct access to any hardware device is allowed.

##Blocked
A process that is blocked on some event (such as I/O operation completion or a signal), may be blocked due to various reasons, such as exhausting its CPU time allocation or waiting for an event to occur.  

##Terminated  
A process may be terminated, either from the "running" state by completing its execution or by explicitly being killed. In either of these cases, the process moves to the "terminated" state. The underlying program is no longer executing, but the process remains in the process table as a **zombie process until its parent process calls the wait system call to read its exit status**, at which point the process is removed from the process table, finally ending the process's lifetime. **If the parent fails to call wait, this continues to consume the process table entry (concretely the process identifier or PID), and causes a resource leak.**

##Swapped out and waiting
(Also called **suspended and waiting.**) In systems that support virtual memory, a process may be swapped out, that is, removed from main memory and placed on external storage by the scheduler. From here the process may be swapped back into the waiting state.

##Swapped out and blocked
(Also called **suspended and blocked.**) Processes that are blocked may also be swapped out. In this event the process is both swapped out and blocked, and may be swapped back in again under the same circumstances as a swapped out and waiting process (although in this case, the process will move to the blocked state, and may still be waiting for a resource to become available).

[wiki Process state](https://en.wikipedia.org/wiki/Process_state )