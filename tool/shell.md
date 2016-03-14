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

ref:[http://askubuntu.com/questions/223237/unable-to-correct-problems-you-have-held-broken-packages](http://askubuntu.com/questions/223237/unable-to-correct-problems-you-have-held-broken-packages "ask-ubuntu")


