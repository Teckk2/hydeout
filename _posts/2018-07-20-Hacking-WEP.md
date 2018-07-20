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
<br>Let's now setup our lab and for which I am going to use a Linksys08362 or you can use any wifi router which offers WEP/WPA/WPA2/WPA2-Enterprise and we need a Kali, and a Wifi adapter which should have Packet injection capability, And for that I am using TP-Link TL-WN722N.</p>

<br> Go to your Wifi router setting and configure it to WEP,
![WEP-1](https://teckk2.github.io/assets/images/Wifi/WEP-1.1.png)
<br>There you will see two options one to create encryption keys with **40 / 64-bit (10 hex digits)** and one with **104 / 128-bit (26 hex digits)**
<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
