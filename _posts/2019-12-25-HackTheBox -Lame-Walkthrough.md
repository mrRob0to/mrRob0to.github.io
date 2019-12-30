---
layout: post
title:  "HackTheBox Lame Walkthrough"
date:   2019-12-25 00:00:00 -0500
categories: Tutorials
---

```
                                                 -----               
                                                 /      \              
                                                 )      |              
          :================:                      "    )/              
         /||              ||                      )_ /*                
        / ||    System    ||                          *                
       |  ||     Down     ||                   (=====~*~======)        
        \ || Please wait  ||                  0      \ /       0       
          ==================                //   (====*====)   ||      
   ........... /      \.............       //         *         ||     
   :\        ############            \    ||    (=====*======)  ||     
   : ---------------------------------     V          *          V     
   : |  *   |__________|| ::::::::::  |    o   (======*=======) o      
   \ |      |          ||   .......   |    \\         *         ||     
     --------------------------------- 8   ||   (=====*======)  //     
                                        8   V         *         V      
     --------------------------------- 8   =|=;  (==/ * \==)   =|=     
     \   ###########################  \   / ! \     _ * __    / | \    
      \  +++++++++++++++++++++++++++   \  ! !  !  (__/ \__)  !  !  !   
       \ ++++++++++++++++++++++++++++   \        0 \ \V/ / 0           
        \________________________________\     ()   \o o/   ()         
         *********************************     ()           ()         
                                                                       
                                           EW                          
                                                                       
GET IT ?!?!?! THE GUY IS WAITING FOR THE MACHINE AND HE'S A SKELETON   
BECAUSE HE DIED AND DECAYED HE WAS WAITING SO LONG !!!! STILL DON'T    
GET IT ??? HERE LET ME DRAW A DIAGRAM :::                              
                                                                       
                                         _        _    __  __ _____    
     _____________________________|\    | |      / \  |  \/  | ____|   
    |                               \   | |     / _ \ | |\/| |  _|     
    |_____________________________  /   | |___ / ___ \| |  | | |___    
                                  |/    |_____/_/   \_\_|  |_|_____|   
                                                                    tQn
                                                                       
```


This box was pretty easy, even easier with using Metasploit. 

* Don't go down the rabbit hole with Port 21.
* There are some other writeups that use smbclient -L 10.10.10.3 to find an exploit. Back in the day I was able to find the user.txt by connecting //10.10.10.3/tmp using anonymous login, but it seems it has been patched, as I receive an error -
```
protocol negotiation failed: NT_STATUS_CONNECTION_DISCONNECTED
```

</br>
</br>


**1)** Scanned and saw that port 21 you are able to log into the FTP service using anonymous login. Also port 445 Samba smbd service specifies a version which we will search for vulnerabilties. 
![NMAP]({{ "/files/HTBLame_00.png" | absolute_url }})<br/> 
<br/>

**2)** Logging into FTP with the anonymous login (press enter for password), after looking through the directories I did not find anything special. - <https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269>
![FTP]({{ "/files/HTBLame_01.png" | absolute_url }})<br/>
<br/>

**3)** Found an exploit for Samba smbd version 3.0.20 - be sure to install the required pysmb depenedencies. 
![whoami]({{ "/files/HTBLame_02.png" | absolute_url }})<br/>
<br/>

**4)** Ran the usermap_script.py exploit and was able to get a root reverse shell. Found the user.txt and root.txt. <br/>

*Once connected with a reverse shell and if python is installed on the victim's machine, you can make the shell interactive with the following code -*

```
python -c 'import pty; pty.spawn("/bin/sh")'
```
![reverseShell]({{ "/files/HTBLame_03.png" | absolute_url }})<br/>
![user]({{ "/files/HTBLame_04.png" | absolute_url }})<br/>
![root]({{ "/files/HTBLame_05.png" | absolute_url }})<br/>


