---
layout: post
title: Windows – stealing hashes
tags: [Security, Active Directory, Pentest, Red-teaming]
comments: true
---

In my preperation of the OSCP course i am learning about windows privilege escalations techniques.
One of the privilege escalation techniques is via kernel exploits.
I have found that git clone <https://github.com/GDSSecurity/Windows-Exploit-Suggester.git> can help me with this.

First we download the script. 
<div class="alert-info">git clone git clone https://github.com/GDSSecurity/Windows-Exploit-Suggester.git
</div>

Next we install dependecies. 
<div class="alert-info">pip install xlrd --upgrade
</div>

As last we update de database.
<div class="alert-info">./windows-exploit-suggester.py --update
</div>
Keep in mind that this will create an xls version of the database which will use later.

Now let's asume we already have user access throug a NetCat reverse shell.
![image](/assets/img/systeminfo)
Copy the output in an text file. We use Windows-Exploit-Suggester to search for any missing updates that could lead us to a privilege escaltion.
<div class="alert-info">./windows-exploit-suggester.py -d 2020-06-11-mssb-xls -i ~/victim-pc/sysinfo.txt
</div>
We 
