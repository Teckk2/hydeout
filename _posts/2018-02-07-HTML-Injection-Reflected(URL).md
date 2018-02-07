---
layout: post
title: HTML Injection -Reflected (URL)
categories:
  - Web-Pentesting
---

<br>As you can see our current URL is <font color="Black">http://192.168.140.138/bWAPP/htmli_current_url.php</font>

![12.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/12.1.png)
<br>Now capture the request in burp
![13.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/13.1.png)
<br>In the host it’s showing the IP of the VM
![14.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/14.1.png)
![15.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/15.1.png)
<br>(But using the HTML injection vulnerability we can change the URL which is specified in the web page and trick our victim.)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
