#Linux Modules


## Compiling Kernel Modules
Kernel modules need to be compiled a bit differently from regular userspace apps. Former kernel versions required us to care much about these settings, which are usually stored in Makefiles. Although hierarchically organized, many redundant settings accumulated in	sublevel Makefiles and made them large and rather difficult to maintain. Fortunately, there is a new way of doing these things, called kbuild, and the build process for external loadable modules is now fully integrated into the standard kernel build mechanism. To learn more on how to compile modules which are not part of the official kernel (such as all the examples you'll find in this guide), see file linux/Documentation/kbuild/modules.txt.
###Makefile for a basic kernel module

    obj-m += hello-1.o
    
    all:
    	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) modules
    
    clean:
    	make -C /lib/modules/$(shell uname -r)/build M=$(PWD) clean

Now you can compile the module by issuing the command make . You should obtain an output which resembles the following:

    hostname:~/lkmpg-examples/02-HelloWorld# make
    make -C /lib/modules/2.6.11/build M=/root/lkmpg-examples/02-HelloWorld modules
    make[1]: Entering directory `/usr/src/linux-2.6.11'
      CC [M]  /root/lkmpg-examples/02-HelloWorld/hello-1.o
     Building modules, stage 2.
      MODPOST
      CC  /root/lkmpg-examples/02-HelloWorld/hello-1.mod.o
      LD [M]  /root/lkmpg-examples/02-HelloWorld/hello-1.ko
    make[1]: Leaving directory `/usr/src/linux-2.6.11'
    hostname:~/lkmpg-examples/02-HelloWorld#

Use **modinfo hello-\*.ko** to see what kind of information it is.  


    hostname:~/lkmpg-examples/02-HelloWorld# modinfo hello-1.ko
    filename:   hello-1.ko
    vermagic:   2.6.11 preempt PENTIUMII 4KSTACKS gcc-3.3
    depends:

##Insert Module to Kernel

    insmod ./hello-1.ko # without dependence checking.
	modprobe ./hello.ko # more cleaver

All modules loaded into the kernel are listed in /proc/modules. Go ahead and cat that file to see that your module is really a part of the kernel.      