---
layout: post
title: SQL Injection -Stored (User-Agent)
categories:
  - Web-Pentesting
---

<br>This is the vulnerability where we will learn to do SQLi in user-agent

![153](https://teckk2.github.io/assets/images/Web%20Pentest/A1/153.png)
<br>First reload the page and capture the GET request in burp
![154](https://teckk2.github.io/assets/images/Web%20Pentest/A1/154.png)
<br>Send the request to repeater and check the SQLi with single quote in User-Agent:
![155](https://teckk2.github.io/assets/images/Web%20Pentest/A1/155.png)
![156](https://teckk2.github.io/assets/images/Web%20Pentest/A1/156.png)
![157](https://teckk2.github.io/assets/images/Web%20Pentest/A1/157.png)
<br>And we got the error.
![158](https://teckk2.github.io/assets/images/Web%20Pentest/A1/158.png)
![159](https://teckk2.github.io/assets/images/Web%20Pentest/A1/159.png)
<br>Now let’s try to extract the mysql root password
![160](https://teckk2.github.io/assets/images/Web%20Pentest/A1/160.png)
![161](https://teckk2.github.io/assets/images/Web%20Pentest/A1/161.png)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
