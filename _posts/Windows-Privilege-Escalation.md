---
layout: post
title: Windows and Linux Privilege Escalation
tags: [Security, OSCP, Privilege escalation, Pentest, Red-teaming]
comments: true
---

In my preperation of the OSCP course i am learning about both linux and windows privilege escalations techniques.
There are differten escaltion techniques like escalation via kernel exploits, unqoted services, misconfigruations and stuff like that.
I built myself an own lab to practice on. I have used the <https://github.com/sagishahar/lpeworkshop> for the lab. Everything you need to know is in there. 

You can find the different privilege escalation manually or via automated scripts.
The two tools i use for automation are;
linux-smart-enumeration for Linux <https://github.com/diego-treitos/linux-smart-enumeration>
winPEAS for Windows <https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite>

To use lse (Linux-smart-enumeration)
First we download the script. 
<div class="alert-info">git clone git clone https://github.com/diego-treitos/linux-smart-enumeration.git
</div>

Next we can use lse. you can use the -h parameter to show the options. I am not going to get in details about this.
<div class="alert-info">./lse.sh -h
</div>
Of course you have to run this on the victim-pc or victim-server.

To use winPEAS
First we download the scripts.
<div class="alert-info">git clone git clone https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite.git
</div>
As with the lse.sh script, you have to run this on the victim-pc or victim-server.

To transfer one of these files you have a few options you can use.
On linux you can start a http server to download the files via the shell on the victim.
Other options are to transfer these files via SMB or NetCat if it is available on the victim.
When transfering via SMB you have to setup SMB on kali.

To start a http server run the following command.
<div class="alert-info"> python3 -m http.server 80</div>   // this will start a http on port 80 in the directory you currently are.

You can now download the lse.sh if you are on Linux or winPEAS.exe if you are on Windows.
Once you have transferd one of the files you can run it and read the output carefully for anything interesting that could lead to a privilege escalation.
