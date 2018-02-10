---
layout: post
title: iFrame Injection
categories:
  - Web-Pentesting
---
<br>An iframe injection is an injection of one or more iframe tags into a page’s content. The iframe typically does something bad, such as downloading an executable application that contains a virus or worm in it… something that compromises a visitor’s system.
<br>If you have a very recent browser (like Firefox 2) then iframe injections aren’t really a worry — these browsers are smart enough not to automatically download and run applications without your permission. But older browsers are more trusting.
<br>Using this vulnerability we can manipulate and redirect the site to show the user what we want to show them. 

![26.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/26.1.png)
<br>As you can see in the URL the site is accessing the robots.txt, but if put any site URL it will start showing the content of that site in this web page.
![27.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/27.1.png)
<br>Using this iframe injection vulnerability, we can manipulate what content to show to our victim, or maybe make him to login to our spoofed Phishing Site.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
