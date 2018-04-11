---
layout: category
title: OSCP
---

<h1 Class="message">
  A Noobs OSCP Journey
</h1>

  
![OSCP-logo](https://teckk2.github.io/assets/images/offsec-logo.png)

So it all starts when I graduated last year in 2016 and finding my way to get a job in Infosec domain, before graduation I already have a [**CEH**](https://www.eccouncil.org/programs/certified-ethical-hacker-ceh/) certification,But as you know it's so hard to get a job as a fresher in this domain especially in India until you have some skills or have a reference. After getting rejected by almost 15 companies I decided to start to increase my skill, and there is no better way than [**OSCP**](https://www.offensive-security.com/information-security-certifications/oscp-offensive-security-certified-professional/). So on the 31st Dec night I talked to my father that I want to spend 1 year on OSCP, after some discussion he eventually agreed, I took the time limit very seriously.

On 1st Jan, my Journey Started, as I was total noob at that time I only knew how to use Nmap, Nessus, Nexpose and reporting Vulnerability Assessment, and some sort of Wifi hacking, not even Metasploit Framework 😂

So it took me 2 months to figure out where to start because there was no one to guide me at that stage, So before I realised, the sand was slipping from my hands and month of march had begun. Then I downloaded [**OSCP syllabus**](https://www.offensive-security.com/documentation/penetration-testing-with-kali.pdf) and googled about some OSCP related VMs from [Vulnhub](http://www.abatchy.com/2017/02/oscp-like-vulnhub-vms). I pwned a few from them; like Kioptrix series, IMF, Brainpan etc. If you are new to Buffer overflow, I recommend to start with [Brainpan 1](https://www.vulnhub.com/entry/brainpan-1,51/). It took me 2 more months to complete these machines. In May, I got introduced to Hack The Box[(HTB)](https://www.hackthebox.eu), If you really want to do [**OSCP**](https://www.offensive-security.com/information-security-certifications/oscp-offensive-security-certified-professional/). I wholeheartedly suggest you to buy HTB VIP pack and finish all the retired machines before you start your lab. I was stuck after 'rooting' 3-4 machines. This is a point where every learner in information security domain hopes for guidance. A guidance on what to learn, a guidance on where am I wrong. During my hard hunt for a mentor, I was lucky enough to meet my mentor _**KNX**_. I am very thankful to him for all his support, teachings and resources.

After completing all the machines in [**HTB**](https://www.hackthebox.eu). I started my OSCP PWK-Lab on 1st oct and due to unfamiliarity with the environment my progress was very slow-going, I signed up for 2 months lab and within 40 days I completed all the machines on all 4 networks.To be noted, complete videos, course manual and lab exercises before you start rooting lab machines.

**OSCP lab Overview**
* In any pentesting the first step is to scan for open ports where we cannot afford to be wrong, because by default Nmap only scan top-1000 ports and sometime vulnerability lies in the top ports, so first scan for default 1000 ports and start working on it and then perform a full port scan in the background as a backup.
* In the lab always try to restrict yourself using Metasploit framework because it's good to learn the manual way, but there are few machines on which you have to use Metasploit framework and there is no public exploit available and this is because PWK want you to learn not only the manual way but also the Metasploit way.
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
      * command:- **sshuttle -l (any port) -r root@10.10.0.1 10.10.0.0/24** 
    * [Networ Pivoting Using MSF](https://www.offensive-security.com/metasploit-unleashed/Pivoting/)
    * [Port forward using MSF](https://www.offensive-security.com/metasploit-unleashed/Portfwd/)
* You need to focus on one more thing which usually many people don't talk about which is post exploit enumeration, which comes after rooted a target machine. In this phase you may find some passwords or some hints to some other machines which might be helpful to get user level access in certain systems.

**My OSCP Exam Experience**

After completing my 2 months of lab, and a week of rest, I scheduled my exam for 7th Dec 12:30 pm, I have a very bad habit to sleep in day and work overnight and I don't know why but my focus is on peak during night. Even I am writing this blog at 4:11 am 😂.
On 6th Dec I woke up around 3:00 pm and started preparing myself for the next day and decided to sleep early around 2 am, now the irony is because of my old habit to be awake late nights and excitement of exam, I couldn't sleep. Hence, It so happened I gave the exam without proper sleep. At 12:30, I started scanning the ports for all machines and done the BOF machine within 3 hours and now I have 25 marks in my pocket; Moved to the next big machine and I did that in next 3 hours. Within 6 hours I had 50 marks. The rest 3 machines was of 20-20-10 marks respectively, I completed them in another 9 hours and within 15 hours I rooted all machines and got 100 marks. Now ,time to make exam report. Because of sleep deprivation for more than 36 hours my mind and body started rusting. I dont advocate for long working without sleep as it can cause serious health issues but I am used to this and I was so excited for OSCP. After spending next 6 hours on my lab report, I still had few hours left for the exam to end. So I went to sleep, after waking up in the evening I reviewed the exam report and mailed to Offsec as per the exam guide.

After Spending almost a year, without stepping out from my house for months, without meeting any friends,  all my hard work paid off when that final day come I got the email that I cleared OSCP.**Wink**-**Wink**
![OSCP-logo](https://teckk2.github.io//assets/images/offsec-student-certified-emblem-rgb-oscp.jpeg)

<iframe src="https://player.vimeo.com/video/115074667" width="640" height="360" frameborder="0" webkitallowfullscreen mozallowfullscreen allowfullscreen></iframe>
I will miss my OSCP labs,Thanx to the _**offensive security**_, **OSCP** was the best learning experience of my life. It was a wonderful phase which I might renew hopefully with OSCE.

* Thanks to my _**Family**_ for supporting me throughout this journey.
* Thanks to my mentor _**KNX**_ for guiding me on the right path.
* Thanks to my Best Friend _**Nyks**_ for supporting and encouraging me always and standing by my side when there was no one.

<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/l4FGF4DVYSeS5oIx2/giphy.mp4" type="video/mp4">
	</video>
</div>

<p Class="message">
~ Fuck The Best Play With The Rest
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script 
  src="https://www.hackthebox.eu/badge/966">
</script>

