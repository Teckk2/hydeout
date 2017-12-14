---
layout: category
title: OSCP
---

<h1 Class="message">
  My OSCP Journey from Noob to Pro
</h1>

![OSCP-logo](https://teckk2.github.io/assets/images/offsec-logo.png)

So it all starts when I graduated last year in 2016 and finding my way to get a job in Infosec domain, before graduation I already have a CEH certification,But as you know it's so hard to get a job as a fresher in this domain especially in India until you have some skills or have a reference. After getting rejected by almost 15 companies I decided to start increasing my skill, and there is no better way then OSCP. So on the 31st Dec night I talked to my father that I want to spend 1 year on OSCP and give me time to prove myself and I can't do the job for now, after some discussion he eventually agreed. but the condition was I have to complete everything within the time limit.

So on the 1st Jan, my journey start, as I was total noob at that time I only knew how to run Nmap, Nessus, Nexpose and doing Vulnerability assessment report, and some sort of Wifi hacking, that it nothing more than that not even MSF 😂

So it took me 2 months to figure out where to start because there was no one to guide me at that time, So before I realise the sand is slipping from hands the month of march has reached, Then I downloaded the OSCP syllabus and googled about some OSCP realted VMs from [Vulnhub](http://www.abatchy.com/2017/02/oscp-like-vulnhub-vms), did few from them and like kioptix seriense and IMF and Brainpan to learn BOF, If you are new to BUffere overflow I recomend to start with [brainpan 1](https://www.vulnhub.com/entry/brainpan-1,51/), I had a slow hand at that time so it took me 2 more months to complete these machine, In MAY I got to know about Hack The Box[(HTB)](https://www.hackthebox.eu), If you really want to do OSCP I wholeheartedly recommend you to buy the HTB Vip pack and finish all the retired machine before you start your lab. So, After finishing 2-3 simple machine in the start I start getting stuck, See when you are learning new stuff which you are not aware off and even you have all the resource available, it is hard to understand some stuff by your self and at that time you need someone to guide you / mentor you which is hard to find, because most of the people don't care to share their knowledge with anyone, but I was lucky I met my mentor _**KNX**_. I am very thankful to him to teach me so many new things.

After completing all the machines in **HTB** I started my OSCP lab on 1st oct and in the start I was unfamiliar with the environment so it took me few days to get pace, I took the 2 months lab and within 40 days I completed all the machine on all 4 networks, and I would recommend completing the videos course and lab exercises before you start rooting lab machines.

**OSCP lab Overview**
* In any pentesting the first step is to scan for open ports where we cannot afford to be wrong, because by default Nmap only scan top-1000 port and sometime vulnerability lies in the top ports, so first scan for default 1000 ports and start working on it and then scan for full port scan in the background for the backup.
* Some usefull Tools and command from my [list](https://teckk2.github.io/2017/12/12/OSCP-Tools-and-commands.html)
* In the lab always try to restrict yourself using Metasploit framework because it's good to learn the manual way, but there are few machine on which you have to use Metasploit framework and there is no public exploit available and this is because PWK want you to learn not only the manual way but also the Metasploit way.
* Don't think too much, or above the ground, try the simple default things first before you start some bruteforcing, you need to _**Try Smarter**_ before you _**Try Harder**_.

* Once you get inside the machine the hardest part is to perform privilege escalation or getting root access
  * [Linux Privilege Escalatio](https://blog.g0tmi1k.com/2011/08/basic-linux-privilege-escalation/)
  * [Windows Privilege Escalation](http://www.fuzzysecurity.com/tutorials/16.html)
  * [Local exploit Suggester for windows](https://pentestlab.blog/2017/04/24/windows-kernel-exploits/)
  * [Windows Pre-compiled Kernal exploits-1](https://github.com/abatchy17/WindowsExploits)
  * [Windows Pre-compiled Kernal exploits-2](https://github.com/SecWiki/windows-kernel-exploits)
  * [Reverse Shell Cheat Sheet](http://pentestmonkey.net/cheat-sheet/shells/reverse-shell-cheat-sheet)
  * [Passing the hash with remote Desktop](https://www.kali.org/penetration-testing/passing-hash-remote-desktop/)
  * [Learning LFI-RFI -1](https://www.hackersonlineclub.com/lfi-rfi/)
  * [Learning LFI-RFI -2](https://0xzoidberg.wordpress.com/category/security/lfi-rfi/)
  * [SQL Injection Cheat-sheet -1](http://resources.infosecinstitute.com/backdoor-sql-injection/)
  * [SQL Injection Cheat-sheet -2](http://resources.infosecinstitute.com/backdoor-sql-injection/)
  * [Online hash-cracking tool -1](https://crackstation.net)
  * [Online hash-cracking tool -2](https://hashkiller.co.uk)
  * [Online NTLM hashcracking tool](http://md5decrypt.net/en/Ntlm/)
  * Learn SSH tunnuling/Network Pivoting and port forwarding
    * [Using SSH](http://www.debianadmin.com/howto-use-ssh-local-and-remote-port-forwarding.html)
    * [using sshuttle (My recommendation)](http://blog.trackets.com/2014/05/17/ssh-tunnel-local-and-remote-port-forwarding-explained-with-examples.html)
      * command:- **sshuttle -r root@192.168.1.101 192.168.1.0/24** 
    * [Networ Pivoting Using MSF](https://www.offensive-security.com/metasploit-unleashed/Pivoting/)
    * [Port forward using MSF](https://www.offensive-security.com/metasploit-unleashed/Portfwd/)
* You need to focus on one more thing which usually many people don't talk about which is post exploit enumeration, which comes after rooted a target machine, this is the end part of any pnetetsting and really important, in this phase you can find some password or some hint to some other machine which you have not rooted yet and it can give you a direct shell, so always post enumerate the system files and logs after rooting it.

**My OSCP Exam Experience**

After completing my 2 months lab with a one week gap I scheduled my exam on 7th Dec 12:30 pm, I have a very bad habit to sleep in day and work whole night don't know why but I can focus more in night time, even I am writing this blog at 4:11 am 😂.
so on the 6th Dec I wake up around 3:00 pm and started preparing myself for the next day and decided to sleep early around 2 am, now the irony is because of my old habit to wake up till late and because of the exam excitement I couldn't sleep,So I have to take my whole exam without sleep. At 12:30 I started scanning the ports for all machines and done the BOF machine within 3 hours and now I have 25 marks in my pocket, move to the next big machine I did that in next 3 hours now total of 6 hours and I have 50 marks, then the rest 3 machine comprises of 20-20-10 marks respectively, I completed them in another 9 hours So within 15 hours I rooted all machines and got 100 marks. Now it time to make exam report, now because I have been awake for more than 36 hours so my mind an body is starting rusting, I do not recommend to wake for this long as it can cause you serious health issues but I am used to this and I was so excited for this oscp that's why I can't able to sleep. After spending next 6 hours my lab report was completed and I still have few hours left for the exam to end, So I went to sleep, after waking up in the evening I reviewed the exam report and send that to offsec.

After Spending almost my whole year, without stepping out from my house for months, without meeting any friends, my all the hard work paid off and the final day come I got the email that I cleared OSCP.**Wink**-**Wink**
![OSCP-logo](https://teckk2.github.io//assets/images/offsec-student-certified-emblem-rgb-oscp.jpeg)

I will miss my OSCP lab, that was the best experience I have experienced so far in my life and learned so much.

* Thanks to my _**Family**_ for supporting me throughout this journey,
* Thanks to my Best Friend _**Nyks**_ for supporting and encouraging me always and standing by my side when there was no one.

