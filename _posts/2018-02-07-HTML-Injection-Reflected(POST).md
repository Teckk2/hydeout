---
layout: post
title: HTML Injection-Reflected (POST)
categories:
  - Web-Pentesting
---
<br>In this also we can use the same techniques as we used in Reflected (Get) HTML injection
![6.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/6.1.png)
![7](https://teckk2.github.io/assets/images/Web%20Pentest/A1/7.png)
<br>Or we can do it like this also by capturing the request and inject the html <h1> tag and in the response it will show us the edited content.
![8](https://teckk2.github.io/assets/images/Web%20Pentest/A1/8.png)
<br>Put some random name or word in the name field and capture the post request in burp.
![9](https://teckk2.github.io/assets/images/Web%20Pentest/A1/9.png)
<br>Now inject the html tag in name fields and forward the request.
![10](https://teckk2.github.io/assets/images/Web%20Pentest/A1/10.png)
![11](https://teckk2.github.io/assets/images/Web%20Pentest/A1/11.png)
<br>We have successfully change the first name in the post request and also injected a redirect link, using this we can trick any user to click on that link and they will be redirect to that specific page of our choice.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
