---
layout: post
title: hashcat commands for RACF passwords
date: 2018-04-24 21:41 +0100
author: Jim
tags: RACF passwords
---
Start [here](https://mainframed767.tumblr.com/post/43072129477/how-to-copy-the-racf-database-off-the-mainframe) for the initial steps. You then have two options to get the hashes into the hashcat format of `$racf$*QWERTY1*5AA70358A9C369E0` rather than the John the Ripper format of `QWERTY1:$QWERTY1$*QWERTY1*5AA70358A9C369E0`:

1. After running racf2john use a regex Find/Replace in Notepad++/BBEdit etc. of `^[^:]*:` and replace with nothing (or use grep and sed from a terminal if you prefer)

2. If running Windows, use [Nigel Pentland's racfsnow](https://www.nigelpentland.co.uk/utilities/) which will, as well as crack passwords, also write the hashes out in both hashcat and John the Ripper output.  

Install hashcat and a dictionary file. If MIXEDCASE is not enabled on the system in question then for added cracking speed I would recommend an all uppercase dictionary with words no longer than 8 characters. I suggest starting with one of the dictionaries from [here](https://github.com/berzerk0/Probable-Wordlists) and then editing as needed (e.g. convert all to uppercase, remove words longer than 8 characters etc.). I have already done this for you [here](https://github.com/jaytay79/Probable-Wordlists/blob/RACF/Real-Passwords/Top304Thousand-probable-v2.txt).     

The below assumes basic knowledge of hashcat as well as having copied my [racf.rule](https://github.com/jaytay79/zos/blob/master/racf.rule) file to the rules subdirectory of hashcat. The command format below is for macOS/Unix, for Windows substitute `./hashcat` with `hashcat64.exe` and swap any `/` characters for a `\`  

These examples are ordeerd from quickets to slowest.  


### Basic dictionary attack
`./hashcat -m 8500 hashes.txt dictionary.txt`

### Dictionary with rule
`./hashcat -m 8500 hashes.txt -r rules/racf.rule dictionary.txt`

### Hybrid attack - uses dictionary and appends 3 numerics - adjust as you see fit
`./hashcat -m 8500 hashes.txt -a 6 dictioanry.txt ?d?d?d

### Mask attack for 8 character passwords using uppercase, digits and national characters
`./hashcat -m 8500 hashes.txt  -a 3 -1 ?u?d@#£ ?1?1?1?1?1?1?1?1`  
replace `@#£` with your own national characters as approrpriate e.g. `$` for `£`, `§` for `@` etc.

For an incremental version that cycles through from e.g. 6 characters up to 8 then add `--increment --increment-min=6`  

##### [OA43999](https://www.ibm.com/support/docview.wss?uid=isg1OA43999) version of the above:
`./hashcat -m 8500 hashes.txt  -a 3 -1 ?u?d#£@.<+|&!*-%_>?:=' ?1?1?1?1?1?1?1?1`

### Print any cracked passwords to a file
`./hashcat -m 8500 hashes.txt --show --outfile=cracked.txt`  

___
If running on a unix based OS I would recommend pulling out the cracked passwords, removing duplicates and then creating a new dictionary file. This file can then be moved between hashcat/John the Ripper and should help speed up any future cracking attempts  
  
```
cut -d: -f 2- hashcat.pot | sort -u > cracked.dic
cat cracked.dic dictionary.txt > combined.txt
cut -d: -f 2- combined.txt | sort -u > dictionary.txt
```
