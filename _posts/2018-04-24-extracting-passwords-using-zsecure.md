---
layout: post
title: Extracting passwords using zSecure
date: 2018-04-24 21:54 +0100
tags: RACF zSecure
---
zSecure is an excellent product that I [heartily endorse](https://www.youtube.com/watch?v=BfOmkqz06SY).  

Here is some CARLa to pull out password hashes from a RACF DB and write out the results in JohnTheRipper and/or Hashcat formats. Just delete the relevant lines to suit your needs.  
To pull out KDFAES hashes replace `password` with `pwdx` but be aware that this will print empty lines for users with a DES password only. At the time of writing there is no publivly known way of cracking KDFAES passwords. I expect this will change in time.  

Note that this requires a RACF database to be allocated in SE.1 and will not work with a zSecure unload (since they don't contain passwords).  

**Note for RACF admins:** Define `XFACILIT` profiles of `CKG.CMD.FIELD.PASSWORD` and `CKG.CMD.FIELD.PWDX` with `UACC(NONE)` to prevent this from working.  

```
newlist nopage
  select  segment=base has_password=yes
/* JtR format */
  sortlist KEY(0) | ":$racf$*" | key(0) | "*" | password(hex,0)
/* Hashcat format*/
  sortlist "$racf$*" | key(0) | "*" | password(hex,0)
```