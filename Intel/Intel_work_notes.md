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


### Test Patch ###
476786/476789/476835 fetched and cherry-picked. Build failed in 1st time. 
TODO: build success, download to 3gr.

16/March 2016
-----------------------

### workstation dev environment ruined ###  
when I try to setup download tool for sofia phone in linux. I apt-get failed to install a lib package. So I turn to aptitude for a quick solution. Aptitude promote me a solution and and I chose 'Y' without cofirmming. 5 mins later, I found aptitude alrady uninstalled everything. Then I try to resetart the computer, the workstation simply can't boot up.  
So, I need to re-install the whole system.

### VNC ###

[VNC](https://www.realvnc.com/) allow you to connect to your remote ubuntu workstation/server.  
download VNC for server and VNC viwer for client. 

### Connect to Ubuntu via FTP ###
**set up FTP in ubuntu**  
``$ sudo apt-get install vsftpd``  
``$ sudo service vsftpd restart``  
for more info: [http://www.krizna.com/ubuntu/setup-ftp-server-on-ubuntu-14-04-vsftpd/](http://www.krizna.com/ubuntu/setup-ftp-server-on-ubuntu-14-04-vsftpd/)  

**connect from windows**  
install [FileZilla](https://filezilla-project.org/)  
set port number ==21

### TODO ###
build up ubuntu download 

### JNI ###
Java Native Interface (JNI)  is a programming framework that enables Java code running in a Java Virtual Machine (JVM) to call and be called by[1] native applications (programs specific to a hardware and operating system platform) and libraries written in other languages such as C, C++ and assembly.  
The JNI framework lets a native method use Java objects in the same way that Java code uses these objects. A native method can create Java objects and then inspect and use these objects to perform its tasks. A native method can also inspect and use objects created by Java application code.  
ref: [wiki](https://en.wikipedia.org/wiki/Java_Native_Interface)  


### g++ commend not found Error: 127 ###

**libxml2.so.2** not installed or linked. Try    
1)   if not installed , for 64 bits   
```sudo apt-get install libxml2:i386 libstdc++6:i386```  
2)   if not linked,  
```sudo ln -s /usr/lib/i386-linux-gnu/libxml2.so.2.7.8 /usr/lib/i386-linux-gnu/libxml2.so.2```

ref: [askubuntu](http://askubuntu.com/questions/373532/when-executing-acroreader-it-fails-with-error-while-loading-shared-libraries-l)

### OC6 work-flow ###
    enter_oc6 -i
    module load opticm6
    
	#--------------------init -----------------
    mkdir <workarea_dir>
    cd <workarea_dir>
    bee create -b sofia_3gr_maint -j16   --> Checkout on tip of the branch --> This is for LPOP Branch.
     
     
    bee create -p SF_3GR_MAINT -v TAG -j16  --> Directly checkout on the give Tag.
    e.g.: 
    bee create -p SF_3GR_MAINT -v SF_3GR_MAINT_1605_5_0735 -j16
    bee switch -p SF_3GR_MAINT -v TAG -j16  --> Directly checkout on the give Tag. This is same as bee create -p .. -v .. option.
    e.g.:
    bee switch -p SF_3GR_MAINT -v SF_3GR_MAINT_1605_5_0735 -j16
	
	#-----------------build -----------------
    cd android
    oc6env -v -t aosp_l 
    source build/envsetup.sh   
    lunch 
    module load openjdk   
    make -j16

    

 
 