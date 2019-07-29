---
layout: post
title:  "HackTheBox Grandpa Walkthrough - NO METASPLOIT"
date:   2019-07-27 00:00:00 -0500
categories: Tutorials
---
<meta name="twitter:image" content="https://mrrob0to.github.io//files/HTBGrandpa_01.png">

```
              ,-----.
            W/,-. ,-.\W
            ()>a   a<()
            (.--(_)--.)
          ,'/.-'\_/`-.\`.
        ,' /    `-'    \ `.
       /   \           /   \
      /     `.       ,'     \
     /    /   `-._.-'   \    \
   ,-`-._/|     |=|o    |\_.-<
  <,--.)  |_____| |o____|  )_ \
   `-)|    |//   _   \\|     )/
     ||    |'    |    `|
     ||    |     |     |
     ||    (    )|(    )
     ||    |     |     |
     ||    |     |     |
     ||    |_.--.|.--._|
     ||     /'""| |""`\
     []     `===' `==='  hjw
```


This was a bit challenging box without metasploit, but luckily all the exploits worked out the box. Three of the most challenging aspects of the box were:

* The low priv reverse shell exploit I was using was a oneshot deal. If I were to lose the shell, I would then have to restart the VM (Probably there was a way around this, but I did not throughly check...)
* This box has *MANY* vulnerabilities. 
* When running the privsec exploit I only had a limited window to execute commands. This was due to a flakey process the exploit was using, and I was not able to manually migrate to a different PID. (More info about Process Migration here...<https://jlajara.gitlab.io/posts/2018/11/26/process-migration.html>)


**1)** Scanned, then researched exploits for Microsoft IIS 6.0 exploits.
![NMAP]({{ "/files/HTBGrandpa_00.png" | absolute_url }})<br/> 
<br/>

**2)** Used this exploit for a reverse shell - <https://github.com/g0rx/iis6-exploit-2017-CVE-2017-7269>
![ReverseShell]({{ "/files/HTBGrandpa_01.png" | absolute_url }})<br/>
<br/>

**3)** Once in the box - *whoami*
![whoami]({{ "/files/HTBGrandpa_02.png" | absolute_url }})<br/>
<br/>

**4)** Ran *windows-exploit-suggester.py* 😮
![suggester]({{ "/files/HTBGrandpa_03.png" | absolute_url }})<br/>
<br/>

**5)** Found this exploit that used Token Kidnapping for a privlage escalation to NT Authority\SYSTEM - <https://github.com/SecWiki/windows-kernel-exploits/tree/master/MS09-012>
<br/>

**6)** But first we need to upload the exploit. I configured a FTP server on my Attacking Machine using Anonymous Login. Then connected to my Kali Box from the Victim. Be sure to make sure you are transfering the file using BINARY mode, also flag -A for Anonymous login.
![FTP]({{ "/files/HTBGrandpa_04.png" | absolute_url }})<br/>
![FTP2]({{ "/files/HTBGrandpa_05.png" | absolute_url }})<br/>
<br/>

**7)** Run the exploit for an elevated shell. The shell may crash due to the unstable process it is using.
![root]({{ "/files/HTBGrandpa_06.png" | absolute_url }})<br/>
<br/>

