---
layout: post
title: InfoSec Interview Questions (Part-2)
categories:
  - Misc
---

This Part of the **(InfoSec Interview Questions)** blog has some senario based questions hope you all like it.

<p Class="message">
  <font color="Black">Question 1</font> – When running an NMAP scan what is the techniques for avoiding Firewalls ?
</p>

<br>**Ans**:- As a penetration tester you will come across with systems that are behind firewalls and they are blocking you from getting the information that you want.So you will need to know how to avoid the firewall rules that are in place and to discover information about a host.This step in a penetration testing called Firewall Evasion Rules.
<p>Nmap has different options to :-</p>
  * **1)	Fragment Packets:- **
  <br>This technique was very effective especially in the old days however you can still use it if you found a firewall that is not properly configured.The Nmap offers that ability to fragment the packets while scanning with the -f option so it can bypass the packet inspection of firewalls.
  <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -f 192.168.1.50
  * **2)	Specify a specific MTU:-**

