---
layout: post
title: InfoSec Interview Questions (Part-3)
categories:
  - Misc
---

<p>This Part is Short but it has very Important 2 questions which I encounter On almost every Interview, The way I Answer it maybe many people will not like it but who cares.😂😂 </p>

<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="https://media.giphy.com/media/RBYBWi1IT8vDy/giphy.mp4" type="video/mp4">
	</video>
</div>
  
<p Class="message">
  <font color="Black">Question 1</font> – On which layer Nmap works?
</p>
<br>**Ans**:- 
br>{_Small and simple answer_} 
  * Nmap works on Two layers Network (Layer 3) and Transport (Layer 4)
<br>{_If they ask for more In-depth answer_} 
  * Nmap Use Network layer to send packets , and for detecting whether the host is Up or not.
  * Transport Layer is used for SYN scan and also to detect which ports are open/closed.
  * Sequence number detection also happens in Transport Layer which is used to detect the OS of the target.
