---
layout: post
title: SQL Injection (Select\GET)
categories:
  - Web-Pentesting
---

<br>To exploit this vulnerability first we have to select one movie from the list

![65](https://teckk2.github.io/assets/images/Web%20Pentest/A1/65.png)
![66](https://teckk2.github.io/assets/images/Web%20Pentest/A1/66.png)
<br>Once we get the movie select with it’s id we can try to inject single quote (‘) to check the slqi
![67](https://teckk2.github.io/assets/images/Web%20Pentest/A1/67.png)
<br>And we got the error now we can proceed to next step and enumerate the database as we have done in our previous sqli blogs
![68](https://teckk2.github.io/assets/images/Web%20Pentest/A1/68.png)
<br>but you have to take care of one thing if you select movie ID which is available then it will not show you what you are looking for for ex. In this the movie ID 2 is available in the database, but 200 is not available, now if we try with 200 we will get our result
![69](https://teckk2.github.io/assets/images/Web%20Pentest/A1/69.png)
![70](https://teckk2.github.io/assets/images/Web%20Pentest/A1/70.png)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
