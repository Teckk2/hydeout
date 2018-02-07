---
layout: post
title: SQL Injection (AJAX\JSON\jQuery)
categories:
  - Web-Pentesting
---

<br>In this (AJAX/JSON/JQUERY) SQLi, to find the vulnerability is little but tricky, you have focus on the out what you are getting

![82](https://teckk2.github.io/assets/images/Web%20Pentest/A1/82.png)
<br>Because as soon you type something the webapp will start predicting it and will start showing you the result.
![83](https://teckk2.github.io/assets/images/Web%20Pentest/A1/83.png)
<br>In this I have just typed aplhabet (i) and it’s start showing me all the name of the movies who consist the letter (i) in it.
![84](https://teckk2.github.io/assets/images/Web%20Pentest/A1/84.png)
<br>And with (ir) only Iron Man is available, now the trick to find the SQLi vulnerability in this is we have to focus on the end result to enumerate
<br>First let’s start finding the columns using {order by}
![85](https://teckk2.github.io/assets/images/Web%20Pentest/A1/85.png)
<br>Using this (' -- #) syntax we can see the result without even typing any alphabet, now to find the exact number of columns we really need to focus on the result.
![86](https://teckk2.github.io/assets/images/Web%20Pentest/A1/86.png)
![87](https://teckk2.github.io/assets/images/Web%20Pentest/A1/87.png)
<br>Result of order by 1 and 2 is same but in order by 3 the result is different
![88](https://teckk2.github.io/assets/images/Web%20Pentest/A1/88.png)
<br>We will do this until the result stops changing
![89](https://teckk2.github.io/assets/images/Web%20Pentest/A1/89.png)
![90](https://teckk2.github.io/assets/images/Web%20Pentest/A1/90.png)
![91](https://teckk2.github.io/assets/images/Web%20Pentest/A1/91.png)
![92](https://teckk2.github.io/assets/images/Web%20Pentest/A1/92.png)
![93](https://teckk2.github.io/assets/images/Web%20Pentest/A1/93.png)
<br>At order by 8 the result stops changing so the number of columns are 7
<br>Now let’s use union select to further enumerate the database
![94](https://teckk2.github.io/assets/images/Web%20Pentest/A1/94.png)
<br><font color="Black">' union select 1,version(),3,4,database(),6,7 -- # </font>
<br>Look at the bottom of the result we can see our desired result in the list.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
