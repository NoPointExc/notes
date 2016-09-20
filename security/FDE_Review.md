#File-Based Encryption, Feature of New Released Android 7.0 (Nougat)

###Introduction 
On August 20, Google released the new Android 7.0 which is also known as Nougat or Android N. Android N has many new feature, including **split-screen**, **openJDK based environment**. However, only few people will notice that, Google made some big enhancements of Android 7.0 in security. **File-based Encryption(FBE)** if one of these enhancements.  

###What is FBE
**FBE** as known as file-level encryption in SELinux, is a feature to allow android file-system encrypted in file/directory level. As we all known, Android is an embedded OS based on SELinux, so Android have similar file-system with other Unix-like OS. Similar with Linux, the file-system of Android is in a Tree structure. So, FBE feature different keys for directories in each Tree level. 

For example, if I have following file structure:

    
    /data/user/0/chrome 
    /data/user/10/facebook 
    
 
System will generate a key for root `/data`, and then key for `/user` will derive from this root key. Then keys for `/0` and `/10` will also derived for `/user` independently. So far, each directory have their own keys. 

Actually, the full system of FBE is much more complex then these explanation.  **The length of this essay is so limited, if you want to known more technical detail, just ask me!**

###Why Android needs FBE
Nowadays, on one hand, the mobile device contains many personal information. Contact information of your family members, personal photos which you don't want to show others, Your emails and so on. We have more and more privacy information and sensitive secrets saved in our mobile devices. On the other hand, as we carry mobile devices go every where,  we often lost our devices. **More seriously, most of lost Android devices are in running state which means your android devices without FBE are not encrypted at all!**   

Before Android N, data in Android are protect by **Full-Disk-Encryption**. As the name indicates, Android simply encrypt your whole disk. It sounds not too bad. However, OS can't not boot-up from full encrypted disk. So, Android OS need to unencrypte  the disk when it is booting up and the **whole disk must keep in unencrypted state when Android is running.** This fault of FDE leave a high risk to your personal information. Moreover, **as Android support multiply users. If other users share an Android device with you and he/she got the root right, then he/she access to all of your data.** 

###Conclusion 
Google have a big ambitious in Android. Now, Android can also running in everywhere. Not only your mobile phones and tablets,  Android are also running in your cars, in restaurant order systems, in PC and more and more.  10 years ago, Android is a geek toy which is only known by few people. **Now, there are 1.4 billion active Android running.** As computer engineers, it's our common responsibility to protect these device from potential security risk. Checkout here [selinuxproject.org](https://selinuxproject.org/page/Main_Page "selinuxproject.org") or here [Android Open Source Project](https://source.android.com/index.html "AOSP") to help!


*Ref*  
- [https://en.wikipedia.org/wiki/Android_Nougat](https://en.wikipedia.org/wiki/Android_Nougat "https://en.wikipedia.org/wiki/Android_Nougat")  
- [https://source.android.com/security/encryption/file-based.html](https://source.android.com/security/encryption/file-based.html)  
- [https://source.android.com/security/encryption/full-disk.html](https://source.android.com/security/encryption/full-disk.html)