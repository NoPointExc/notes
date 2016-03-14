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



14/March 2016
-----------------------

### krb5-user ###
*Basic programs to authenticate using MIT Kerberos.*

Kerberos is an authentication protocol using a combination of secret-key cryptography and trusted third parties to allow secure authentication to network services over untrusted networks. More information about the Kerberos protocol is available from MIT's Kerberos site. Designing an Authentication System is an accessible introduction to the principals of Kerberos' authentication scheme.

### Repo vs Git###
**repo is a tool to manage gits in one big project. repo is the 'git' for gits**

Repo is a repository management tool that we built on top of Git. Repo unifies the many Git repositories when necessary, does the uploads to our revision control system, and automates parts of the Android development workflow. Repo is not meant to replace Git, only to make it easier to work with Git in the context of Android. The repo command is an executable Python script that you can put anywhere in your path. In working with the Android source files, you will use Repo for across-network operations. For example, with a single Repo command you can download files from multiple repositories into your local working directory.

ref: [https://source.android.com/source/developing.html](https://source.android.com/source/developing.html)

### Gerrit ###
**web-based code review system**

Gerrit is a web-based code review system for projects that use git. Gerrit encourages more centralized use of Git by allowing all authorized users to submit changes, which are automatically merged if they pass code review. In addition, Gerrit makes reviewing easier by displaying changes side by side in-browser and enabling inline comments.
