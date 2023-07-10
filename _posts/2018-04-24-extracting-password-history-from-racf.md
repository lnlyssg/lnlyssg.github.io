---
layout: post
title: Extracting password history from RACF
date: 2018-04-24 21:48 +0100
author: Jim
tags: RACF passwords
---
With thanks to [Dhiru Kholia](https://github.com/kholia), who was able to tidy up the "mystery" [racf_debug.c program](https://gist.github.com/anonymous/848a5219560b18989fcf878e1df034d2), it is possible to extract old passwords for IDs from a RACF database. Unfortunately this is one downside to having an extensive password history enabled on a system - e.g. `SETROPTS HISTORY(12)` means that 12 old passwords are retained in the RACF database to ensure users do not re-use their passwords. It also means that all 12 password hashes are also stored...

**Q:** Why would you want the old hashes?
**A:** Why not? 😃 Apart from idle curiosity, a genuine use would be to track password patterns used which could allow you to predict future passwords for an ID

1. Save the [code](https://github.com/lnlyssg/zos/blob/master/racf_debug_cleanup.c) to your PC (or clone the repo if you prefer)

2. On a Unix-like system, compile and run it (if using macOS you will need to have Xcode and the command line tools installed to use gcc): `gcc racf-debug-cleanup.c -o racf-debug-cleanup; ./racf-debug-cleanup
SYS1.RACFDB  | grep '\$racf' > hashes.txt`

3. Use the resulting hashes.txt file in [hashcat]({{ site.baseurl }}{% post_url 2018-04-24-hashcat-commands-for-racf-passwords %})