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
    * Nmap is giving the option to the user to set a specific MTU (Maximum Transmission Unit) to the packet.This is similar to the packet fragmentation technique that we have explained above.
    * During the scan that size of the nmap will create packets with size based on the number that we will give.In this example we gave the number 24 so the nmap will create 24-byte packets causing a confusion to the firewall.Have in mind that the MTU number must be a multiple of 8 (8,16,24,32 etc).  
    * You can specify the MTU of your choice with the command –mtu number target.
  <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap –mtu 24 192.168.1.50
  
  * **3)	Use Decoy addresses:-**
  In this type of scan you can instruct Nmap to spoof packets from other hosts.In the firewall logs it will be not only our IP address but also and the IP addresses of the decoys so it will be much harder to determine from which system the scan started.There are two options that you can use in this type of scan:-
    * <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -D RND:10 [target] (Generates a random number of decoys)
    * <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -D decoy1,decoy2,decoy3 etc. (Manually specify the IP addresses of the decoys)
  
  <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap –D 192.168.1.40,192.168.1.45 192.168.1.50
    
