---
layout: post
title: SQL Injection -Stored (SQLite)
categories:
  - Web-Pentesting
---

<br>..

![142](https://teckk2.github.io/assets/images/Web%20Pentest/A1/142.png)
![143](https://teckk2.github.io/assets/images/Web%20Pentest/A1/143.png)
![144](https://teckk2.github.io/assets/images/Web%20Pentest/A1/144.png)
<br>Let’s try with single quote
![145](https://teckk2.github.io/assets/images/Web%20Pentest/A1/145.png)
![146](https://teckk2.github.io/assets/images/Web%20Pentest/A1/146.png)
<br>The entry was added but it’s not showing anything which mean we found the SQLi
<br>Now we have to find the correct syntax so we can see the output of the sqli on the webpage
![147](https://teckk2.github.io/assets/images/Web%20Pentest/A1/147.png)
<br>**','');**
![148](https://teckk2.github.io/assets/images/Web%20Pentest/A1/148.png)
<br>As you can see with **','');** we could add a blank entry in the blog
![149](https://teckk2.github.io/assets/images/Web%20Pentest/A1/149.png)
<br>**', sqlite_version());**
![150](https://teckk2.github.io/assets/images/Web%20Pentest/A1/150.png)
![151](https://teckk2.github.io/assets/images/Web%20Pentest/A1/151.png)
<br>**', (SELECT name FROM sqlite_master WHERE type='table'));**
![152](https://teckk2.github.io/assets/images/Web%20Pentest/A1/152.png)
<br>Table name is **blog**, using this method you can enumerate it further.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>


