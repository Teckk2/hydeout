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
