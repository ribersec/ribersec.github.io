In my preperation of the OSCP course i am learning about windows privilege escalations techniques.
One of the privilege escalation techniques is via kernel exploits.
I have found that git clone https://github.com/GDSSecurity/Windows-Exploit-Suggester.git can help me with this.

First we download the script<div class="alert-info">
git clone git clone https://github.com/GDSSecurity/Windows-Exploit-Suggester.git
</div>

Next we install dependecies<div class="alert-info">
pip install xlrd --upgrade
</div>

As last we update de database<div class="alert-info">
./windows-exploit-suggester.py --update
</div>

