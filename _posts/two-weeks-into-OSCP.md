---
layout: post
title: My journey to OSCP
subtitle: Two weeks into the OSCP
tags: [Security, OSCP, Privilege escalation, Pentest, Red-teaming]
comments: true
---

So this blogpost will cover my first 2 weeks in the OSCP labs and materials and what i have done the last 14 days.  
I won't go into much detail about the boxes because it is not allowed. But you have easy, medium and hard boxes.  
The hard boxes are as anyone should already know; Pain, Humble, Sufferance, Gh0st and 1nsider.  
If you need help or tips feel free to contact me or follow me on twitter and i will be happy to help. (no spoilers)  

So it was sunday morning 07:00 am when i woke up and checked my mail and found the logon credentials for the Labs and the 
link to download the materials.  I immediatly started to work through the PDF and the video's at the same time.  
You guys should know that i have some experience in pentesting as i hold my eJPT and eCPPT which helped me to understand
a lot of the materials. Also i am sometimes playing around on hackthebox.  

So after i did do some of the PDF and Videos i went to the labs and figured out the IP's of the boxes and started to pentest them.  
I use autorecon which is created by Tib3rius. I am wellknow with the tool because i use it on HTB as well.  
<https://github.com/Tib3rius/AutoRecon>  
It is also allowd on the exam so definitaly going to use it.  

A strong word of advise is that you should esthablish a good methodology that works for you.  
Don't follow someone's metholodogy but create one yourself. This is could be harder then it sounds.  
Bu try and build one for yourself.  
Also keep an eye out for rabbitholes because there are plenty of them and you have to think straight when going through the results of your scans.  

Let me give an example. If you manage to upload something on a server via FTP (port 21) and you have no option of calling it then you should move on right?  
If you upload a shell and are not able to execute it then by all means leave it as it could be a rabbit hole.  

Another tip is read ever line, word, sentence in the scan results do not skip a thing!  
I have read to quick through scan results and missed alot of things that are definitly usefull, like software version, headers.  
Don't forget to check the source of a http(s) service as well.

All the boxes are vulnerable you just have to find the right exploit and use it.
So search for exploits on the pre-installed (if you use Kali) searchsploit ( searchsploit apache 2, for example).  
Get used to search on exploit-db.com and also start searching exploits on github.

When you have found an exploit read the code, 9 out of 10 times there is something you need to change.
Like an IP, port number or maybe even the payload itself (x86/x64)

When you have a low shell obtained you have to transfer files to it.
You can read my previous blogpost about Windows and Linux Privilege Escalation Tools
<https://ribersec.com/2020-06-12-Windows-Privilege-Escalation-Tools/>

So untill now these are some of my advices and findings during the first 2 weeks into the OSCP.
While writing this i have managed to root 30 boxe so far, including Pain, Sufferance and Gh0st.

One final thought is that i use the tips in the forums for almost every box.
I do this because i (only) have 30 days and cannot be searching for ages as my time is limited in this journey.

Hope you guys did enjoy reading this and feel free to reach out or follow me on twitter.




