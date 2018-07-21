---
layout: post
title:  "Quick and Dirty JPG LSB Steganography"
date:   2018-07-05 03:30:50 -0400
categories: Quick and Dirty
---

Programs:
(1) HxD
(2) MS Paint 3D




Using the Least Significant Bit of a .jpg, we can manipulate the data to incorporate our own binary message.






 .jpg HEX Header value starts with FFD8FF

![jpgHeader]({{ "/files/post1_01.png" | absolute_url }})<br/> 

 .jpg HEX Footer value ends with FFD9

![jpgFooter]({{ "/files/post1_02.png" | absolute_url }})<br/> 

 (Optional) Using MS paint I used a black bar to create a reference point to "encode" my message.

![Original]({{ "/files/post1_0060_01.png" | absolute_url }})<br/>
![MSPaintEdit]({{ "/files/post1_0060_02.png" | absolute_url }})<br/>  

Opening up the .jpg with the edited black bar, we can easily pinpoint the "area" in HxD.

![LSB]({{ "/files/post1_03.png" | absolute_url }})<br/>

We then manipulate the LEAST SIGNIFICANT BIT as, no pun intended, will cause the the LEAST manipulation on the image.

*The example used does show heavy manipulation, which is intened.


