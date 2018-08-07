---
layout: post
title: Hacking (WEP)
categories:
  - Wifi Pentesting
---


<p>Before we start attacknig WEP let's learn about it's history a bit. (WEP) stands for Wired Equivalent Privacy, which is a security protocol, specified in the IEEE Wireless Fidelity (Wi-Fi) standard, 802.11b, that is designed to provide a wireless local area network (WLAN) with a level of security and privacy comparable to what is usually expected of a wired LAN.</p>

<br>**WEP** Uses RC4 stream cipher and 64-or 128-bit keys. Static master key must be manually entered into each device.
<br>WEP was introduced in 1999. Within a few years, several security researchers discovered flaws in its design. The "24 additional bits of system-generated data" mentioned above is technically known as the Initialization Vector and proved to be the most critical protocol flaw. With simple and readily available tools, a hacker can determine the WEP key and use it to break into an active Wi-Fi network within a matter of minutes.

<p>Vendor-specific enhancements to WEP like WEP+ and Dynamic WEP were implemented in attempts to patch some of the shortcomings of WEP, but these technologies are also not viable today.</p>
<br>I know WEP is not used anymore, but it's good to understand the concept if you don't know, So Let's start now by setting up our lab and for which I am going to use a Linksys08362 and Linksys47370 or you can use any wifi router which offers WEP/WPA/WPA2/WPA2-Enterprise and we need a Kali, and a Wifi adapter which should have Packet injection capability, And for that I am using TP-Link TL-WN722N.

<br> Go to your Wifi router setting and configure it to WEP,
![WEP-1](https://teckk2.github.io/assets/images/Wifi/1.1.PNG)
<br>There you will see two options one to create encryption keys with **40 / 64-bit (10 hex digits)** and one with **104 / 128-bit (26 hex digits)** this is the security feature which they added before WPA was formally adopted in 2003. This option is not available in many routers/old.

<font size="1">
<div style="height:150px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># iwconfig 
<br>wlan0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;IEEE 802.11  ESSID:off/any  
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<font color="ffff00">Mode:Managed</font>&nbsp;&nbsp;Access&nbsp;Point:&nbsp;Not-Associated&nbsp;&nbsp;&nbsp;Tx-Power=20 dBm   
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retry short limit:7&nbsp;&nbsp;&nbsp;RTS thr:off&nbsp;&nbsp;&nbsp;Fragment thr:off
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Encryption key:off
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Power Management:off</p>
          
<p>lo&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no wireless extensions.</p>

<p>eth0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no wireless extensions.</p>

<font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font>#
</div>
</font>

<br>As you can see in our wifi adapter which is **Wlan0** the mode is showing: Managed and to dump the data from the envirement and for packet injection or to do other stuff we need **Monitor** Mode and to do that we can use a beautiful set of tool airmon-ng which will set out wifi adpater to monitor mode.

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># airmon-ng start wlan0</p>

<p>Found 3 processes that could cause trouble.
<br>If airodump-ng, aireplay-ng or airtun-ng stops working after
<br>a short period of time, you may want to run 'airmon-ng check kill'</p>

<p>&nbsp;&nbsp;PID Name
<br>&nbsp;&nbsp;518 NetworkManager
<br>&nbsp;&nbsp;741 wpa_supplicant
<br>&nbsp;4814 dhclient</p>

<p>PHY&nbsp;Interface	Driver&nbsp;&nbsp;Chipset</p>

<p>phy0	wlan0&nbsp;&nbsp;ath9k_htc&nbsp;Atheros Communications, Inc. AR9271 802.11n</p>

<p>&nbsp;&nbsp;(mac80211 monitor mode vif enabled for [phy0]wlan0 on [phy0]wlan0mon)
<br>&nbsp;&nbsp;(mac80211 station mode vif disabled for [phy0]wlan0)</p>

<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># iwconfig 
<br><font color="53E100">wlan0mon</font>&nbsp;&nbsp;IEEE 802.11&nbsp;&nbsp;<font color="ffff00">Mode:Monitor</font>&nbsp;&nbsp;Frequency:2.457 GHz&nbsp;&nbsp;Tx-Power=20 dBm   
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Retry short limit:7&nbsp;&nbsp;&nbsp;RTS thr:off&nbsp;&nbsp;&nbsp;Fragment thr:off
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Power Management:off</p>
          
<p>lo&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no wireless extensions.</p>

<p>eth0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;no wireless extensions.</p>

<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># </p>
</div>
</font>

<br>Now as you can see the Mode has been chnaged to Monitor and the adapter name is also changed from wlan0 to wlan0mon, Now to proceed further we need to kill some process which may cause problem while we scan for availbale network or dump the data. to do that we just need to use **airmon-ng check kill** and it will kill the process which may cause problemin our way.

<font size="1">
<div style="height:180px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">
<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font># airmon-ng check kill</p>

<p>Killing these processes:</p>

<p>&nbsp;&nbsp;PID Name
<br>&nbsp;&nbsp;741 wpa_supplicant
<br>&nbsp;4814 dhclient</p>

<p><font color="red">root@kali</font>:<font color="RoyalBlue">~/Desktop</font>#</p>
</div>
</font>

<br>Now we can use Wifite, which will automate a lot of stuff for us, using airodump-ng, aireplay-ng and aircrack-ng in the background and will give us our desired result.
![2](https://teckk2.github.io/assets/images/Wifi/2.PNG)
<br>Now as we start this tool with **--wep** which we used to search only **WEP** enables devices and **--mac** to randomize our Wlan mac.
![3](https://teckk2.github.io/assets/images/Wifi/3.PNG)
<br>As soon you see your target **SSID** press ctrl+c and it will ask you for option which target you wanna select and attack based on serial no. and then it will start attacking the target by first capturing the handshake and once the handshake is done, it will start the cracking the password, as you all know WEP algorithm is not that secure, it cracked the Key within 40-Sec.
<br>**Key-**2627F68597



<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
