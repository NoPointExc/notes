### Redirect log to a file ###
```$ make [selction] > log_file  2>&1```  

All POSIX operating systems have 3 streams: **stdin, stdout, and stderr**. stdin is the input, which can accept the stdout or stderr. stdout is the primary output, which is** redirected with >, >>, or |**. **stderr is the error output,** which is handled separately so that any exceptions do not get passed to a command or written to a file that it might break; normally, this is sent to a log of some kind, or dumped directly, even when the stdout is redirected. To redirect both to the same place.

### track a log file dynamiclly ###

``` tail -f log_file ```

### unable to correct problems you have held broken packages ###

106
down vote
That particular error message may indicate that you have held packages, but it may also indicate a different problem.  

You can get a list of actual held packages with:  

`` dpkg --get-selections | grep hold``  

If there are none, or none look related, then it's probably something else. Check carefully the output of the command you were trying when you got the error message, as there may be other clues in the full output from that command, aside from the error message.  

Another method of troubleshooting may be to use aptitude rather than apt-get to try to install your package:  

``sudo aptitude install <packagename>``  

Aptitude will give up less easily, and will attempt to find solutions which may involve modifying other packages. It may give you more explanation of the problem and options for fixing it.  

Occasionally aptitude will be too eager to remove or downgrade large numbers of packages to satisfy your request, in which case retrying with -f changes its priorities and helps it come up with solutions that involve removing/downgrading fewer packages even if it means not all changes you requested can go ahead:

sudo aptitude -f install <packagename>

ref: [answer from ask ubuntu](http://askubuntu.com/questions/223237/unable-to-correct-problems-you-have-held-broken-packages)

### Why is 1/1/1970 the “epoch time”? ###

Early versions of unix measured system time in 1/60 s intervals. This meant that a 32-bit unsigned integer could only represent a span of time less than 829 days. For this reason, the time represented by the number 0 (called the epoch) had to be set in the very recent past. As this was in the early 1970s, the epoch was set to 1971-1-1.  

Later, the system time was changed to increment every second, which increased the span of time that could be represented by a 32-bit unsigned integer to around 136 years. As it was no longer so important to squeeze every second out of the counter, the epoch was rounded down to the nearest decade, thus becoming 1970-1-1. One must assume that this was considered a bit neater than 1971-1-1.  

Note that a 32-bit signed integer using 1970-1-1 as its epoch can represent dates up to 2038-1-19, on which date it will wrap around to 1901-12-13.  

ref: [answer of commmunity wiki forom stackoverflow.com](http://stackoverflow.com/questions/1090869/why-is-1-1-1970-the-epoch-time)

### check installed software ###
dpkg --get-selections [name1] [name2] ...

refer: [how to geek](http://www.howtogeek.com/howto/linux/show-the-list-of-installed-packages-on-ubuntu-or-debian/)

### rsync ###
To sync files/folders from one machine to another.  
To sync a folder:  
Source Machine:  
```rsync -avhP <Src folder> <username-to>@<address-to> ``` 

Destionation Machine:  
```rsync -avhP <username-from>@<address-from>:<remote path-from> <local path-to>```  
input password for remote device  
ref:[http://linux.die.net/man/1/rsync](http://linux.die.net/man/1/rsync)  

### Yocto Project SDK ###  
- A cross-compile toolchain which is a combination of two sysroots.  

- One for the target  
	
	- Contains headers and libraries for the target  
	- NOTE: Consistent with the generated image from which it is derived  

- One for the host  
	- Contains host specific tools  
	- NOTE: These tools ensure things are consistent and work as expected while building against the target sysroo  

- An environment script to setup the necessary variables to
make these work together


### Using cd to go up multiple directory levels ###

Navigate up the directory using ..n :  
In the example below, ..4 is used to go up 4 directory level, ..3 to go up 3 directory level, ..2 to go up 2 directory level. 
  
Add the following alias to the .bash_profile (or .bashrc) and re-login.
   
    alias ..="cd .." 
    alias ..2="cd ../.."
    alias ..3="cd ../../.."