---
layout: post
title: InfoSec Interview Questions (Part-3)
categories:
  - Misc
---

<p>This Part is Short but it has two very Important questions which I encounter On almost every Interview, The way I Answer it maybe many people will not like it but who cares.😂😂 </p>

<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/RBYBWi1IT8vDy/giphy.mp4" type="video/mp4">
	</video>
</div>
  
<br>
<p Class="message">
  <font color="Black">Question 1</font> – On which layer Nmap works?
</p>
<br>**Ans**:- 
<br>{_**Small and simple answer**_} 
  * Nmap works on Two layers Network (Layer 3) and Transport (Layer 4)

<br>{_**If they ask for more In-depth answer**_} 
  * Nmap Use Network layer to send packets , and for detecting whether the host is Up or not.
  * Transport Layer is used for SYN scan and also to detect which ports are open/closed.
  * Sequence number detection also happens in Transport Layer which is used to detect the OS of the target.

<p Class="message">
  <font color="Black">Question 2</font> – Explain Pen testing lifecycle in Detail.
</p>

<br>**Ans**:- This question can vary either they can ask you to explain this in a telephonic interview or in an online written interview, So you need to manage accrodingly.

<br> This is the Cycle I usually follow while doing Pentesting.

![Pentesting-life-Cycle](https://teckk2.github.io/assets/images/pentestingLifeCycle-4.jpeg)

<br>1) **Scope** - In this we need to find how many IP’s are available in the network, or provided by the client to scan.

<br>2) **Reconnaissance** - this is the first interaction with the target machine in which we will enumerate to find the open ports for which we will use Nmap based on that result we will move to the next step.
<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/xUNd9L1VpqjRxXEw5W/giphy.mp4" type="video/mp4">
	</video>
</div>	

<br> **Note**: {The Target is given by the Client So I am not going to explain Passive Reconnaissance as it is simple to understand I guess you guys already know about it.}

<br>3) **Vulnerability Detection** -  Based on the Nmap result we need to find on which port the service is running and which version is installed. 

<br>4) **Information Analysis and Planning** – If we found any service which is running we will search for the public exploit if available or try to find it manually if it’s running any web server for which further enumeration of the web service we can use Nikto, gobuster, etc..

<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/BHNVC6suWIKs/giphy.mp4" type="video/mp4">
	</video>
</div>

<br>5) **Penetration Testing** - If the service we found is vulnerable to some sort of vulnerability 
	* For example, if there is old iweb http server is running then we can exploit it through directory traversal attack and download and have access to sensitive files.
<br>Or if there is some service running like
	* Achat 0.150 service running on port 9255 and 9256 then we can get a shell using a public bof exploit which is available on exploit db just by replacing the shell code we can get a shell.
	
<br>6) **Privilege Escalation** – This is the most important part after gaining shell is to gain root access on the system, for that there are numerous ways, but first I like to go the old classic way by finding what permission the user have if we have user access, what is running on the crontab, what file permission we have and what are the binary file which have suid or guid permission on the server and on what kernel the server is running on, based on these enumeration we can try to privilege our user to get root level access.

<br>7) **Reporting** – This is important step to create a clean and understandable report because sometime, the client we are interacting with is not that technically good, So we have to make a report in such a way so he can easily understand, and if possible there IT team can mimic the steps which we have done to compromise the machine by following the Report.

<br>8) **Clean-Up** – This is the last and important part in which we need to clean the footprint before we go out, remove the logs of your system from the server, delete the file you download for enumeration or testing.

<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/3oKIPCSX4UHmuS41TG/giphy.mp4" type="video/mp4">
	</video>
</div>
	
	
<p class="message">
 Tip ~ Don't fall for girls, Instead fall for knowledge atleast it will Love you back one day!
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
	
