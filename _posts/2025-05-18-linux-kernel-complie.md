---
layout: post
title:  "Linux Kernel compile guide"
date:   2025-05-18 00:00:00 -0500
categories: Tutorials
---

### Disclaimer

This guide does not explain the details of compiling a Linux kernel, nor does it guarantee that it will work on other systems.
Do check out the Linux Foundation for more information: [https://training.linuxfoundation.org/training/a-beginners-guide-to-linux-kernel-development-lfd103/](https://training.linuxfoundation.org/training/a-beginners-guide-to-linux-kernel-development-lfd103/)

### Hardware

* MBP M2 - MacOS Sequoia <br/>
* Parallels running Ubuntu VM 24.04.02 6.8.0-59 generic
<br/>

### Commands

```
 # Commands to compile linux kernel
 594  sudo apt-get install build-essential vim git cscope libncurses-dev libssl-dev bison flex
 595  cd ~ && mkdir linux_work
 596  git clone git://git.kernel.org/pub/scm/linux/kernel/git/stable/linux-stable.git linux_stable
 598  cd linux_stable
 601  git checkout linux-6.9.y 
 605  cp /boot/config-6.8.0-59-generic.config
 607  vim .config
 608  make clean
 609  make oldconfig
 612  make -j12
 620  sudo make modules_install install
 644  cd /etc/default
 649  sudo vim grub
 650  sudo update-grub
 657  reboot

```

</br>
### Notes 
<br/>

```
###################

# 601  git checkout linux-6.9.y
# This was the latest branch at the time 05/25  
# Use 'git branch -a' to check the latest releases  

###################

# 607 vim .config 
# If you receive a certificate error when compiling,
# in .config edit these lines as follows

 CONFIG_SYSTEM_TRUSTED_KEYS=""
 CONFIG_SYSTEM_REVOCATION_KEYS="" 

###################

# 609  make oldconfig
# You can use 'make menuconfig' to customize the kernel
# oldconfig uses the current host configuration

###################

# 612 make -j12
# Change '12' to the number of jobs you want to use
# My MBP has 12 cores so I used 12 jobs

###################

# 649 sudo vim grub
# Change the values below: 
    
 #GRUB_TIMEOUT_STYLE=hidden
 GRUB_TIMEOUT=10
 GRUB_CMDLINE_LINUX="earlyprintk=vga"

```
