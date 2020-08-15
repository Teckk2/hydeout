---
layout: post
title: DIVA - Input Validation Issues - Part 1
categories:
  - Mobile
---

<br>Our next challange is abourt Input Validation Issues
<br>Input validation attack happens when the application could not sanitize the user input properly, and which could lead to data information leak, one of the simplest example of this is SQLi and XSS.
<br>![7-1](https://teckk2.github.io/assets/images/DIVA/7-1.png)
<br>So in this challenge there are 3 default users, and if we could find any of them, we can see the secret data, so let’s start
<br>![7-2](https://teckk2.github.io/assets/images/DIVA/7-2.png)
<br>First I tried with a single quote (‘) and looked at Logcat to see the error
<br>![7-3](https://teckk2.github.io/assets/images/DIVA/7-3.png)
<br>We can see a sql error, which means we are on the right path as it’s using dynamic queries to retrieve data from the database, and as usual a single quote created an error in the query
<br>Now let’s try with two and three quotes and see the response in the Logcat
<br>![7-4](https://teckk2.github.io/assets/images/DIVA/7-4.png)
<br>![7-5](https://teckk2.github.io/assets/images/DIVA/7-5.png)
<br>Perfetto, now have verified that odd number of single quotes are causing sql errors, now let’s try to retrieve the username from the database
<br>![7-6](https://teckk2.github.io/assets/images/DIVA/7-6.png)
<br>With a simple true statement we can extract the stored credentials from the database
<br>Now, let’s have a look in the source code which is the reason behind this vulnerability.
<br>![7-7](https://teckk2.github.io/assets/images/DIVA/7-7.png)
<br>![7-8](https://teckk2.github.io/assets/images/DIVA/7-8.png)
<br>This line of code allow the user to retrieve the data from sql query.


<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
