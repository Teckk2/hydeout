---
layout: post
title: HTML Injection-Reflected (GET)
categories:
  - Web-Pentesting
---

<p>HTML injection is a type of injection issue that occurs when a user is able to control an input point and is able to inject arbitrary HTML code into a vulnerable web page. </p>
<br>This vulnerability can have many consequences, like disclosure of a user's session cookies that could be used to impersonate the victim, or, more generally, it can allow the attacker to modify the page content seen by the victims.

![1.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/1.1.png)
<br>In the blank fields enter your name, and click on go.
![2.2](https://teckk2.github.io/assets/images/Web%20Pentest/A1/2.1.png)
<br>Now if you focus the name we put is now showing in the URL
![3.3](https://teckk2.github.io/assets/images/Web%20Pentest/A1/3.1.png)
<br>Because this application is vulnerable to HTML injection we can inject  HTML <h1> tag which will reflect our name. and if we want we can even inject any URL, by clicking the user will be redirected to that site.
![4.3](https://teckk2.github.io/assets/images/Web%20Pentest/A1/4.3.png)
![4.4](https://teckk2.github.io/assets/images/Web%20Pentest/A1/4.4.png)
<br>Now if the user will click on teck then he will be redirect to google.com .
<br>You can also inject the HTML tags like this
![5.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/5.1.png)


<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
