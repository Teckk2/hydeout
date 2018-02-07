---
layout: post
title: SQL Injection (Drupal)
categories:
  - Web-Pentesting
---

<br>..

![128](https://teckk2.github.io/assets/images/Web%20Pentest/A1/128.png)
<br>For this vulnerability we have to access the Drupal web inside this server
![129](https://teckk2.github.io/assets/images/Web%20Pentest/A1/129.png)
<br>and to exploit this there is a hint already given for the vulnerability **CVE-2014-3704**
<br>Or we can also check the exact version installed on the server by checking /CHANGELOG.txt
![130](https://teckk2.github.io/assets/images/Web%20Pentest/A1/130.png)
<br>The Drupal version is 7.31 installed.
<br>For this I found a public exploit which is SQLi written in PHP
<br>[https://www.exploit-db.com/exploits/34993/](https://www.exploit-db.com/exploits/34993/)
![131](https://teckk2.github.io/assets/images/Web%20Pentest/A1/131.png)
<br>Just change the URL and run the exploit
![132](https://teckk2.github.io/assets/images/Web%20Pentest/A1/132.png)
<br>Exploit successful, now we can login in drupal with admin:admin
![133](https://teckk2.github.io/assets/images/Web%20Pentest/A1/133.png)
<br>Got the admin access.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>




