---
layout: post
title: Physical Breach
categories:
  - Red Teaming
---


<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="http://giphygifs.s3.amazonaws.com/media/5CsmAaFsM0sZa/giphy.mp4" type="video/mp4">
	</video>
</div>


<br>In past few years I observed that most of the people in Infosec don't understand a simple logic, Safety is not a product but a process and must be introduced already in the design phase, typical example the development of safe code (SDC) etc. So many beautiful words and phrases made, and then the reality of the facts? I see a lot of companies entrusting the entire security of their business to the latest equipment (firewall, IDS/IPS & co) by closing the corporate perimeter as much as possible inside a digital wall with the belief that if block threats from the outside, I don't need to secure what's inside. Very well, what if the threat came from the inside? What if someone can get in? These are the companies that then become so debilitated by a cyber attack to the point that they find themselves forced to close their business.

<br>Few months back we got few projects where I have to perform physical breach, So in this scencarion I will share the experience of two of my clients, one which is related to Payment Industry and the second one is Holding Company for them I have to do a physical breach on their showrooms. Let's start:

<br>Let's start with the **First client**, So as we all know before attacking any target enumeration is the most important part, similarly in physical breach also, we need to enumerate every single thing which could help us to breach it successfully, So my colleagues already went in that office for some casual meetings, he took some Videos and pictures of guest entry card, which helped me to understand the security posture, and I created a cloned visitor card, which looks identical to the orignal card, in case someone ask me about my card, then we noticed another thing, the lift loby was in middle of the corridor, if you turn left after 10 steps there is security desk where you have to submit your ID and get a visitors card, and from there you can enter the office, and if you turn right there is one door which opens to the office IT department directly, but for that we need a valid RFID card.

<br>Now the plan was me and my colleagues will go in lift untill we found someone who is going on the same floor, we were lucky within few minitues we found someone who was going tp the same floor, Now time to execute the plan, as soon we reached that floor, my colleagues moved first and turned left to engage the security for me, and I just followed that guy pretending to be on phone, and the tailgating method worked perfectly.

<br>Now I was inside the office and the time was around 3:30 or 4 PM and people usually leave by 4, So it was just perfect time for me to do this activity, after roaming for few minutes I found one place in middle of the office desk area where no one was sitting, there were couple of people were sitting around me, but they were too busy already in their work and one more thing I noticed in human nature, If you are wearing a Suit that means you are good person 😂.

<br>Now I was sitting on a Desk and I found one employee card and the desk belogs to the same person, I wear that employee ID and turned it to back side so no one can see the picture on the card to identify, Now I have access to any RFID door in the office, I later found that card belogs to the finacce head of the company LoL.

<br>Now time to get inside the network, I removed the cable from the VOIP phone on my desk and connected and after enumerating for some time, I realise that have a NAC, and to bypass I follwed my old method **[Bypassing NAC](https://teckk2.github.io/red%20teaming/2019/10/06/Physical-Breach.html)**, but this time the situation was a bit different, the VOIP phone was totally segrgated on different Vlan, but I found one Printer brodcasting the wifi, and using airmon-ng I got the mac address of that printer, and luckily that printer was part of that network, and I bypassed the NAC and scanned their whole network.





<p class="message">
  ~ Hack the World and Stay Noob.
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
