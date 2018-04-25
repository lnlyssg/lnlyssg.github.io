---
layout: post
title: Finding RVARY password hashes
date: 2018-04-25 18:59 +0100
author: Jim
tags: RACF RVARY
---
This is also included in [SETRRCVT](https://github.com/jaytay79/zos/blob/master/SETRRCVT.rexx) but to find the DES encrypted RVARY passwords in common storage:  

```
TSO ISRDDN  
BROWSE 10.?+3e0?+1B8  
```
![RVARY passwords]({{ "/assets/rvary.png" | absolute_url }})

In the above example the password was set to "QWERTY1" for both RVARY SWITCH and RVARY STATUS and "5AA70358 A9C369E0" is the DES value for both (RVARY SWITCH is the first set of bytes and RVARY STATUS the second set). If the values are all "0"s then the default password of "YES" is set.  

If you want to run this in hashcat then the key used to generate the DES hashes is the plaintext password itself! e.g. `$racf$*QWERTY1*5AA70358A9C369E0`

_With thanks to [Nigel Pentland](https://www.nigelpentland.co.uk/utilities/) for his assistance on figuring out the key used_