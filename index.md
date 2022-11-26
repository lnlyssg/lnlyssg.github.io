## RDEFINE SITE RACF.GURU UACC(READ) DATA(‘RACF TOOLS AND INFO’)

I really only bought this domain for the email address but figured I may as well put _some_ content up alongside it.

### ADDSD 'JIM.TOOLS' UACC(READ)
[z/OS tools](https://github.com/jaytay79/zos) - SETRRCVT and some other bits and pieces
[IRRXUTIL samples](https://github.com/jaytay79/IRRXUTIL) - Some samples of IRRXUTIL
[ENUM](https://github.com/mainframed/Enumeration) - Enumeration Rexx in collaboration with SoF & Ayoul3
[Probable Wordlists](https://github.com/jaytay79/Probable-Wordlists/tree/RACF/Real-Passwords) - Passwords edited to conform to UPPERCASE and 8 character max standards.
[MFBBEdit Modules](https://github.com/jaytay79/MFBBEditModules) - Modules for [BBEdit](https://www.barebones.com/products/bbedit/) for ReXX and JCL highlighting.
[MFWordlists](https://github.com/jaytay79/MFwordlists) - Wordlists for use in cracking RACF passwords


### PERMIT 'JIM.POSTS' ID(*) ACCESS(READ)
<ul>
  {% for post in site.posts %}
    <li>
      <a href="{{ post.url }}">{{ post.title }}</a>
    </li>
  {% endfor %}
</ul>

### RACLINK ID(JIM) LIST
[Bigendian Smalls](https://bigendiansmalls.com)
[Soldier of FORTRAN](https://mainframed767.tumblr.com)
[Nigel Pentland's Utilities](https://www.nigelpentland.co.uk/utilities/)
[Ayoul3's excellent Privesc tools](https://github.com/ayoul3/Privesc)
[/r/mainframe](https://reddit.com/r/mainframe/)

### LISTUSER JIM
[Linktree](https://linktr.ee/racf)
[email](mailto:contact@racf.guru)
<a rel="me" href="https://pleroma.racf.guru/@jaytay" style="display: none;">Pleroma</a>
<a rel="me" href="https://social.racf.guru/@jaytay" style="display: none;">Mastodon</a>

* * *

Any views or opinions represented on this website are personal and belong solely to me and do not represent those of people, institutions or organizations that the owner may or may not be associated with in a professional or personal capacity, unless explicitly stated.
