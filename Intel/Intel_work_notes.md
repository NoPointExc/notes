  03/March 2016
-------------
####Fix a Error 
> enter_oc6
//for bee
[tcsh] jiayangs@shsxgull001:/> module load opticm6
== OptiCM6 env. v16.01.01 - Commands available: bee, oc6gui, enter_oc6, oc6env ==

bee startsms -all //create a branch 

git commit --amend || bee commit --amend 
// commit and overrite the last commit

#### Rebase ####


#### Cross Repo Dependency ####
* CRD is the mechanism to logically combine commits from different repos into one meta-commit (Bundle) which is handled as one unit in Gerrit.

* All changes belonging to a Bundle will be tested together in one testrun on TCloud.

* All changes belonging to a Bundle will be submitted together to the mainline only after all received code Review +2 and Verified +1

* CRD Workflow * 
//create workspace   |  create new branch |    stage and commit changes | upload the files|
bee init -b ...-crd -> bee startsms --all -> bee stage; bee commit; ->    bee upload    ->    conduct reviews&CI test         

11/March  2016
-----------------
####Possible Error: 
 
    cc Command not found  
    [config.o] Error 127  

####Possible Reason: 
cc not linked to gcc or gcc not installed.



03/March 2016
### reset local repo branch to be  just like remote repo HEAD

``git fetch origin``  
``git reset --hard origin/master``  
if you want to save your current branch's state before doing this (just in case), you can do:  

``git commit -a -m "Saving my work, just in case"  ``  
`` git branch my-saved-work ``

### discard local changes and update with remote 
``git reset --hard origin/master``  
``git pull origin master``

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

### krb5-user ###
*Basic programs to authenticate using MIT Kerberos.*

Kerberos is an authentication protocol using a combination of secret-key cryptography and trusted third parties to allow secure authentication to network services over untrusted networks. More information about the Kerberos protocol is available from MIT's Kerberos site. Designing an Authentication System is an accessible introduction to the principals of Kerberos' authentication scheme.