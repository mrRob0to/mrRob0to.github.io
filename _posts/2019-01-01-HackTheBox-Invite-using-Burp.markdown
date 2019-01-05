---
layout: post
title:  "HackTheBox invite using Burp"
date:   2019-01-01 00:00:00 -0500
categories: Tutorials
---


How I got the HackTheBox invite code using Burp suite.


***Programs:*** <br/>
 **•** Burp suite <br/>
 **•** Firefox ESR<br/>
<br/>



#### **(1)** First I set my Firefox proxy to *127.0.0.1* for Burp to interecept the traffic.

![FirefoxProxy]({{ "/files/post2_00.PNG" | absolute_url }})<br/> 
![BurpIntercept]({{ "/files/post2_01.PNG" | absolute_url }})<br/> 
<br/>
<br/>
#### **(2)** Turned on Spider

![BurpSpider]({{ "/files/post2_02.PNG" | absolute_url }})<br/> 
<br/>
<br/>

#### **(3)** Looked at the sitemap and saw something interesting... *inviteapi.min.js*

![BurpSitemap]({{ "/files/post2_06.PNG" | absolute_url }})<br/>
![inviteapi.min.js]({{ "/files/post2_03.PNG" | absolute_url }})<br/> 
<br/>
<br/> 

#### **(4)** Converted the inviteapi.min.js to something more readable using beautifier.io.

![beautifier.io]({{ "/files/post2_04.PNG" | absolute_url }})<br/>
![beautifure.io]({{ "/files/post2_05.PNG" | absolute_url }})<br/>
<br/>
<br/>

#### **(5)** Sent the inviteapi.min.js file to the repeater, changed GET to POST.

![BurpRepeater]({{ "/files/post2_06_edited.PNG"| absolute_url }})<br/>
![BurpRepeaterGET]({{ "/files/post2_07_edited.png" | absolute_url }})<br/>
![BurpRepeaterResponse]({{ "/files/post2_08.PNG" | absolute_url }})<br/>
<br/>
<br/>

#### **(6)** Saw some interesting data encoded in R0T13.

![R0T13]({{ "/files/post2_10.PNG" | absolute_url }})<br/>
<br/>
<br/>

#### **(7)** Added https://www.hackthebox.eu/invite to the repeater, and POSTED the decrypted filepath

![BurpSitemap]({{ "/files/post2_11.PNG" | absolute_url }})<br/>
![BurpRepeater]({{ "/files/post2_12.PNG" | absolute_url }})<br/>
<br/>
<br/>


#### **(8)** Saw another interesting data and encoded in base 64, found the invite code once decrypted :)

![BurpRepeaterResponse]({{ "/files/post2_12_edited.png" | absolute_url }})<br/>
![Base64Decrypt]({{ "/files/post2_13.PNG" | absolute_url }})<br/>





