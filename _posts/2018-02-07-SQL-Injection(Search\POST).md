---
layout: post
title: SQL Injection (Search\POST)
categories:
  - Web-Pentesting
---

<br>SQL Injection (Search/POST) is also similar to (Search/Get) but the main difference is you cannot see the tittle searched in the URL so you have two options either you can capture the request in burp and do the same steps as we did in (Search/Get) to enumerate the database.

![71](https://teckk2.github.io/assets/images/Web%20Pentest/A1/71.png)
![72.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/72.1.png)
<br>Send the request to repeater
![73](https://teckk2.github.io/assets/images/Web%20Pentest/A1/73.png)
<br>Or you can type the sql syntax in search column itself
![74](https://teckk2.github.io/assets/images/Web%20Pentest/A1/74.png)
<br>And we can also extract the login and password hash in the same way and if we want we can use different columns for that like this.
![75](https://teckk2.github.io/assets/images/Web%20Pentest/A1/75.png)
<br><font color="Black">1' union select 1,login,password,email,5,6,7 from users # </font>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>

