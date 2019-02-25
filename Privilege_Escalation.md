# Privilege Escalation

### Learn Privilege Escalation

* [Windows / Linux Local Privilege Escalation Workshop](https://github.com/sagishahar/lpeworkshop) - The Privilege Escalation Workshop covers all known (at the time) attack vectors of local user privilege escalation on both Linux and Windows operating systems and includes slides, videos, test VMs.
<img src="https://pbs.twimg.com/media/DAZsE2VUQAA_bpZ.jpg">

### Linux Privilege Escalation

* [Basic Linux Privilege Escalation](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/) - Linux Privilege Escalation by [@g0tmi1k](https://twitter.com/g0tmi1k)
* [linux-exploit-suggester.sh](https://github.com/mzet-/linux-exploit-suggester) - Linux privilege escalation auditing tool written in bash (updated)
* [Linux_Exploit_Suggester.pl](https://github.com/PenturaLabs/Linux_Exploit_Suggester) - Linux Exploit Suggester written in Perl (last update 3 years ago)
* [Linux_Exploit_Suggester.pl v2](https://github.com/jondonas/linux-exploit-suggester-2) - Next-generation exploit suggester based on Linux_Exploit_Suggester (updated)
* [Linux Soft Exploit Suggester](https://github.com/belane/linux-soft-exploit-suggester) - linux-soft-exploit-suggester finds exploits for all vulnerable software in a system helping with the privilege escalation. It focuses on software packages instead of Kernel vulnerabilities
* [checksec.sh](https://github.com/slimm609/checksec.sh) - bash script to check the properties of executables (like PIE, RELRO, PaX, Canaries, ASLR, Fortify Source)
* [linuxprivchecker.py](http://www.securitysift.com/download/linuxprivchecker.py) - This script is intended to be executed locally on a Linux box to enumerate basic system info and search for common privilege escalation vectors such as world writable files, misconfigurations, clear-text passwords and applicable exploits (@SecuritySift)
* [LinEnum](https://github.com/rebootuser/LinEnum) - This tool is great at running through a heap of things you should check on a Linux system in the post exploit process. This include file permissions, cron jobs if visible, weak credentials etc.(@Rebootuser)


### Windows Privilege Escalation

* [PowerUp](https://github.com/PowerShellMafia/PowerSploit/tree/master/Privesc) - Excellent powershell script for checking of common Windows privilege escalation vectors. Written by [harmj0y](https://twitter.com/harmj0y) [(direct link)](https://raw.githubusercontent.com/PowerShellMafia/PowerSploit/master/Privesc/PowerUp.ps1)
* [PowerUp Cheat Sheet](https://github.com/HarmJ0y/CheatSheets/blob/master/PowerUp.pdf)
* [Windows Exploit Suggester](https://github.com/GDSSecurity/Windows-Exploit-Suggester) - Tool for detection of missing security patches on the windows operating system and mapping with the public available exploits
* [Sherlock](https://github.com/rasta-mouse/Sherlock) - PowerShell script to quickly find missing software patches for local privilege escalation vulnerabilities
* [Precompiled Windows Exploits](https://github.com/abatchy17/WindowsExploits) - Collection of precompiled Windows exploits
* [Metasploit Modules](https://github.com/rapid7/metasploit-framework)
  * post/multi/recon/local_exploit_suggester - suggests local meterpreter exploits that can be used
  * post/windows/gather/enum_patches - helps to identify any missing patches
