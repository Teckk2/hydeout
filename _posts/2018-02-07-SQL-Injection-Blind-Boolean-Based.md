---
layout: post
title: SQL Injection -Blind -Boolean-Based
categories:
  - Web-Pentesting
---

<br>..

![162](https://teckk2.github.io/assets/images/Web%20Pentest/A1/162.png)
<br>This is a Blind-Boolean Based injection which is really difficult to enumerate, still let’s try
![163](https://teckk2.github.io/assets/images/Web%20Pentest/A1/163.png)
![164](https://teckk2.github.io/assets/images/Web%20Pentest/A1/164.png)
<br>Single quote is being detected by server so this is not going to work we have to add something else.
![165](https://teckk2.github.io/assets/images/Web%20Pentest/A1/165.png)
![166](https://teckk2.github.io/assets/images/Web%20Pentest/A1/166.png)
<br>The above syntax didn’t give us any error because, Boolean-based SQL Injection is an inferential SQL Injection technique that relies on sending an SQL query to the database which forces the application to return a different result depending on whether the query returns a TRUE or FALSE result.
![167](https://teckk2.github.io/assets/images/Web%20Pentest/A1/167.png)
<br>**' or 1=0 order by 1-- #**
![168](https://teckk2.github.io/assets/images/Web%20Pentest/A1/168.png)
<br>To check the number of columns we can use the above syntax until it gives us incorrect syntax error!
![169](https://teckk2.github.io/assets/images/Web%20Pentest/A1/169.png)
![170](https://teckk2.github.io/assets/images/Web%20Pentest/A1/170.png)
![171](https://teckk2.github.io/assets/images/Web%20Pentest/A1/171.png)
<br>At order by **8** it gave us error so which means it has **7** columns
<br>Depending on the result, the content within the HTTP response will change, or remain the same. This allows an attacker to infer if the payload used returned true or false, even though no data from the database is returned. This attack is typically slow (especially on large databases) since an attacker would need to enumerate a database, character by character.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>

