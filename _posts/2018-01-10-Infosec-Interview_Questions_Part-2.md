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
  
  * <font color="Black">1)  Fragment Packets:-</font> 
    This technique was very effective especially in the old days however you can still use it if you found a firewall that is not properly configured.The Nmap offers that ability to fragment the packets while scanning with the -f option so it can bypass the packet inspection of firewalls.
  <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -f 192.168.1.50
  
  * <font color="Black">2)	Specify a specific MTU:-</font>
    * Nmap is giving the option to the user to set a specific MTU (Maximum Transmission Unit) to the packet.This is similar to the packet fragmentation technique that we have explained above.
    * During the scan that size of the nmap will create packets with size based on the number that we will give.In this example we gave the number 24 so the nmap will create 24-byte packets causing a confusion to the firewall.Have in mind that the MTU number must be a multiple of 8 (8,16,24,32 etc).  
    * You can specify the MTU of your choice with the command –mtu number target.
  <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap –mtu 24 192.168.1.50
  
  * <font color="Black">3)	Use Decoy addresses:-</font>
  In this type of scan you can instruct Nmap to spoof packets from other hosts.In the firewall logs it will be not only our IP address but also and the IP addresses of the decoys so it will be much harder to determine from which system the scan started.There are two options that you can use in this type of scan:-
    * <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -D RND:10 [target] (Generates a random number of decoys)
    * <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -D decoy1,decoy2,decoy3 etc. (Manually specify the IP addresses of the decoys)
    * <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap –D 192.168.1.40,192.168.1.45 192.168.1.50
    
  * <font color="Black">4)	Idle Zombie Scan:-</font>
    
    * This technique allows you to use another host on the network that is idle in order to perform a port scan to another host.The main advantage of this method is that it very stealthy because the firewall log files will record the IP address of the Zombie and not our IP.However in order to have proper results we must found hosts that are idle on the network.
    
    * Metasploit framework has a scanner that can help us to discover hosts that are idle on the network and it can be used while implementing this type of scan.
    <br><font color="Black">msf > use auxiliary/scanner/ip/ipidseq</font>
    <br><font color="Black">msf auxiliary(<font color="red">ipidseq</font>) > set RHOST 192.168.1.2-192.168.1.50</font>
    
    * using this scanner you can find which IP is idle in the network and are potential candidate for use on an idle Zombie Scan. In order to implement an Idle Zombie scan we need to use the command :-
    
    <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -sI [Zombie IP] [Target IP]
  
  * <font color="Black">5)	Source port number specification:-</font>
    A common error that many administrators are doing when configuring firewalls is to set up a rule to allow all incoming traffic that comes from a specific port number.The –source-port option of Nmap can be used to exploit this misconfiguration.Common ports that you can use for this type of scan are: 20,53 and 67
    <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap –source-port 53 scanme.nmap.org
  
  * <font color="Black">6)	Append Random Data:- </font>
    * Many firewalls are inspecting packets by looking at their size in order to identify a potential port scan. This is because many scanners are sending packets that have specific size.In order to avoid that kind of detection you can use the command –data-length to add additional data and to send packets with different size than the default. 
    * In the below nmap command we have changed the packet size by adding 25 more bytes. By default the packet size is 58 bytes but after adding 25 more bytes the packet size will be 83 bytes.
    <br><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap –data-length 25 192.168.1.50
  
  *  <font color="Black">7)	Scan with Random Order:- </font>
    o	In this technique you can scan a number of hosts in random order and not sequential.The command that you use to instruct Nmap to scan for host in random order is –randomize-hosts.
    o	This technique combined with slow timing options in nmap command can be very effective when you don’t want to alert firewalls.
    o	root@kali:~/Desktop# nmap –randomize-hosts 192.168.1.50-80
  
  * <font color="Black">8)	MAC Address Spoofing:-</font>
    * Another method for bypassing firewall restrictions while doing a port scan is by spoofing the MAC address of your host.This technique can be very effective especially if there is a MAC filtering rule to allow only traffic from certain MAC addresses so you will need to discover which MAC address you need to set in order to obtain results.
    * Specifically the –spoof-mac option gives you the ability to choose a MAC address from a specific vendor,to choose a random MAC address or to set a specific MAC address of your choice.Another advantage of MAC address spoofing is that you make your scan more stealthier because your real MAC address it will not appear on the firewall log files.
      * Specify MAC address from a Vendor —-> –spoof-mac Dell/Apple/3Com
      * Generate a random MAC address —-> —spoof-mac 0
      * Specify your own MAC address —-> —spoof-mac 00:01:03:25:46:AK
      
      * <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap -sT -Pn --spoof-mac Dell 192.168.1.50
  
  * <font color="Black">9)	Send Bad Checksums:-</font>
    * Checksums are used by the TCP/IP protocol to ensure the data integrity. However sending packets with incorrect checksums can help you to discover information from systems that is not properly configured or when you are trying to avoid a firewall.
    * You can use the command nmap –badsum IP in order to send packets with bad checksums to your targets.If you didn’t get any results. It means that the system is suitable configured.
    
    <font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># nmap --badsum 192.168.1.50
  
  
<p Class="message">
  <font color="Black">Question 2</font> – What kind of attack is ARP Spoofing considered and how could you leverage it on a penetration test?
</p>

<br>**Ans**:- 
  * ARP spoofing considered as (Man-In-The-Middle) attack. In a Penetrations test we can act like an attacker and perform the attack in which a malicious actor sends falsified ARP (Address Resolution Protocol) messages over a local area network.
  * This results in the linking of an attacker’s MAC address with the IP address of a legitimate computer or server on the network. Once the attacker’s MAC address is connected to an authentic IP address, the attacker will begin receiving any data that is intended for that IP address.
  * ARP spoofing can enable malicious parties to intercept, modify or even stop data in-transit. ARP spoofing attacks can only occur on local area networks that utilize the Address Resolution Protocol.
  
<p Class="message">
  <font color="Black">Question 3</font> – Answer true or false and explain your answer: Does Web-loggin 2-step verification protect user from session hijacking?
</p>

<br>**Ans**:- 2 Factor authentication doesn't protect the site being vulnerable to session hijacking rather the site should be protected from client-side attacks like XSS. This is because session hijacking involves injecting victim's session cookies extracted using attacks like XSS.

<p Class="message">
  <font color="Black">Question 4</font> – what is stream cipher?
</p>

<br>**Ans**:- 
  * A stream cipher is a symmetric key cipher where plaintext digits are combined with a pseudorandom cipher digit stream (keystream).
  * In a stream cipher, each plaintext digit is encrypted one at a time with the corresponding digit of the keystream, to give a digit of the ciphertext stream. 
  * Since encryption of each digit is dependent on the current state of the cipher, it is also known as state cipher. In practice, a digit is typically a bit and the combining operation an exclusive-or (XOR)
  
<h1 Class="message">
  Part-3 Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
  
