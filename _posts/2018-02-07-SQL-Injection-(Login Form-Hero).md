---
layout: post
title: SQL Injection (Login Form\Hero)
categories:
  - Web-Pentesting
---

<br>In this we have to bypass the login using sqli, So first check the SQLi with single quote (‘)

![98.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/98.1.png)
![99](https://teckk2.github.io/assets/images/Web%20Pentest/A1/99.png)
<br>We got the error, now try to bypass this login
![100](https://teckk2.github.io/assets/images/Web%20Pentest/A1/100.png)
<br>Put **(‘ or 1=1 -- #)** or **(‘ or 1=1 -- -)** in username field and type anything in the password field and press login
![101](https://teckk2.github.io/assets/images/Web%20Pentest/A1/101.png)
<br>And we bypass the login form and got the access of user Neo.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
