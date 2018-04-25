---
layout: post
title: ISRDDN Control Block Browsing
date: 2018-04-25 18:48 +0100
author: Jim
tags: ISRDDN
---
1. From a TSO `READY` prompt or in ISPF option 6 `ALLOC DA(ISRDDN.CB) DSORG(PS) SPACE(1,0) TRACKS LRECL(80) RECFM(F,B) BLKSIZE(27920) NEW`

2. Copy the data from [MVS Control Blocks.txt](https://github.com/jaytay79/zos/blob/master/MVS%20Control%20Blocks.txt) into `yourid.ISRDDN.CB`.

3. Enter `ALLOC F(ISRDDN) DA('yourid.ISRDDN.CB') SHR` from ISPF option 6 (and additonally add this to your logon allocations if required)

4. You can then enter `TSO ISRDDN` and type `B ACEE` to jump to your ACEE in storage etc.

Process taken from [here](http://www.meerkatcomputerservices.com/mfblog/wp-content/uploads/2016/07/Browsing-MVS-Control-Blocks-Using-DDLIST.pdf)