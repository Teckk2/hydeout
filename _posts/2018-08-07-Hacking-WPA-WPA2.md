---
layout: post
title: Hacking (WPA/WPA2)
categories:
  - Wifi Pentesting
---

<br>**Wi-Fi Protected Access (WPA)**
<p>Wi-Fi Protected Access (WPA) was the Wi-Fi Alliance’s direct response and replacement to the increasingly apparent vulnerabilities of the WEP standard. WPA was formally adopted in 2003, a year before WEP was officially retired. The most common WPA configuration is WPA-PSK (Pre-Shared Key). The keys used by WPA are 256-bit, a significant increase over the 64-bit and 128-bit keys used in the WEP system.</p>

<p>Some of the significant changes implemented with WPA included message integrity checks (to determine if an attacker had captured or altered packets passed between the access point and client) and the Temporal Key Integrity Protocol (TKIP). TKIP employs a per-packet key system that was radically more secure than the fixed key system used by WEP. The TKIP encryption standard was later superseded by Advanced Encryption Standard (AES).</p>

<p>Despite what a significant improvement WPA was over WEP, the ghost of WEP haunted WPA. TKIP, a core component of WPA,  was designed to be easily rolled out via firmware upgrades onto existing WEP-enabled devices. As such, it had to recycle certain elements used in the WEP system which, ultimately, were also exploited.</p>

<p>WPA, like its predecessor WEP, has been shown via both proof-of-concept and applied public demonstrations to be vulnerable to intrusion. Interestingly, the process by which WPA is usually breached is not a direct attack on the WPA protocol (although such attacks have been successfully demonstrated), but by attacks on a supplementary system that was rolled out with WPA—Wi-Fi Protected Setup (WPS)—which was designed to make it easy to link devices to modern access points.</p>

<br>**Wi-Fi Protected Access II (WPA2)**
<p>WPA has, as of 2006, been officially superseded by WPA2. One of the most significant changes between WPA and WPA2 is the mandatory use of AES algorithms and the introduction of CCMP (Counter Cipher Mode with Block Chaining Message Authentication Code Protocol) as a replacement for TKIP. However, TKIP is still preserved in WPA2 as a fallback system and for interoperability with WPA.</p>

<p>Currently, the primary security vulnerability to the actual WPA2 system is an obscure one (and requires the attacker to already have access to the secured Wi-Fi network in order to gain access to certain keys and then perpetuate an attack against other devices on the network). As such, the security implications of the known WPA2 vulnerabilities are limited almost entirely to enterprise level networks and deserve little to no practical consideration in regard to home network security.</p>

<p>Unfortunately, the same vulnerability that is the biggest hole in the WPA armor—the attack vector through the Wi-Fi Protected Setup (WPS)—remains in modern WPA2-capable access points. Although breaking into a WPA/WPA2 secured network using this vulnerability requires anywhere from 2-14 hours of sustained effort with a modern computer, it is still a legitimate security concern. WPS should be disabled and, if possible, the firmware of the access point should be flashed to a distribution that doesn’t even support WPS so the attack vector is entirely removed.</p>

<br>Now set-up the lab
<br>![1](https://teckk2.github.io/assets/images/Wifi/9.PNG)
<br>Just type **airodump-ng -i wlan0mon**
<br>And it will start shwoing all the available APs in the evironment across all the channels.
<br>![2](https://teckk2.github.io/assets/images/Wifi/18.PNG)
<br>Select your target IP
<br>![3](https://teckk2.github.io/assets/images/Wifi/11.png)
<br>Where **-c** is to specify the channel, **--bssid** is to specify the bssid/MAC of the AP, and **-w** is to name the file on which we need to write the captured file.
<br>![4](https://teckk2.github.io/assets/images/Wifi/12.PNG)
<br>Under station we can see the connected clients to that AP, in this case that is my Phone.
<br>Now we will perform a de-auth attack and try to capture the handshake.
<br>![5](https://teckk2.github.io/assets/images/Wifi/13.PNG)
<br>Make sure you send enough deauth packets until we capture the handshake
<br>![6](https://teckk2.github.io/assets/images/Wifi/14.PNG)
<br>As you can see we successfully captured the handshake now we can try to crack it using **aircrack-ng**
<br>![7](https://teckk2.github.io/assets/images/Wifi/15.PNG)
<br>![8](https://teckk2.github.io/assets/images/Wifi/16.PNG)
<br>As password was in the list already it was easy to crack, but what if we don't have that password in the dictionary file?
<br>We can generate our own Password-list and pipe it to aircrack-ng without thinking for storing TB's of password in our machine.
<br>![9](https://teckk2.github.io/assets/images/Wifi/17.PNG)
<br>This method of cracking is really time consuming and it depends based on your hardware capability.



<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
