---
layout: post
title: SQL Injection -Blind -Time-Based
categories:
  - Web-Pentesting
---

<br>..

![172](https://teckk2.github.io/assets/images/Web%20Pentest/A1/172.png)
![173](https://teckk2.github.io/assets/images/Web%20Pentest/A1/173.png)
<br>**teck'-SLEEP(5)#**
![174](https://teckk2.github.io/assets/images/Web%20Pentest/A1/174.png)
<br>Time-based SQL Injection is an inferential SQL Injection technique that relies on sending an SQL query to the database which forces the database to wait for a specified amount of time (in seconds) before responding. The response time will indicate to the attacker whether the result of the query is TRUE or FALSE.
![175](https://teckk2.github.io/assets/images/Web%20Pentest/A1/175.png)
<br>**teck'-IF(MID(VERSION(),1,1) = '5', SLEEP(5), 0)#**
<br>Depending on the result, an HTTP response will be returned with a delay, or returned immediately. This allows an attacker to infer if the payload used returned true or false, even though no data from the database is returned. This attack is typically slow (especially on large databases) since an attacker would need to enumerate a database character by character.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
