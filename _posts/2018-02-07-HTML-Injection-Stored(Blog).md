---
layout: post
title: HTML Injection -Stored (Blog)
categories:
  - Web-Pentesting
---

<br>For this vulnerability consider a scenario where the blog stores a commend or some sort of text message from the users.

![16.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/16.1.png)
![17.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/17.1.png)
<br>As you can see the user teck submitted the text “test” at 15:21:36 on 2018-02-02
<br> Let’s try basic html injection first
![18.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/18.1.png)
![19.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/19.1.png)
<br>As you can see it’s working.
<br>Now let’s try with <iframe>
![20.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/20.1.png)
![21.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/21.1.png)
<br>It’s working, so using this we can trick the user to login to the web page and meanwhile we will capture the credential of that user.
![22.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/22.1.png)
<br>[Payload (Github)](https://github.com/Teckk2/Teck_k2/blob/master/HTML%20Injection%20-Stored%20(Blog))
<br>Now as soon you will submit, the web page will show session expired and login page
![23.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/23.1.png)
<br>Now refresh the nc and start listening again, and next time any user will login, we will be able to see the credentials.
![24.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/24.1.png)
![25.1](https://teckk2.github.io/assets/images/Web%20Pentest/A1/25.1.png)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>


