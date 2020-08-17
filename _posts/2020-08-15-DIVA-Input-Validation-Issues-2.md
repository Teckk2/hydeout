---
layout: post
title: DIVA - Input Validation Issues - Part 2
categories:
  - Mobile
---

<br>In this challenge we will solve and learn how we can view sensitive data inside the device, from the application which was meant to view only web URLs
<br>![8-1](https://teckk2.github.io/assets/images/DIVA/8-1.png)
<br>![8-2](https://teckk2.github.io/assets/images/DIVA/8-2.png)
<br>As you can see the application open the webpage inside the application frame.
<br>Let’s see if could read internal device files through application or not?
<br>Let’s start with something basic, create a new file and try to read it from application itself
<br>![8-3](https://teckk2.github.io/assets/images/DIVA/8-3.png)
<br>![8-4](https://teckk2.github.io/assets/images/DIVA/8-4.png)
<br>It’s working fine, let’s try to read some confidential file which we found in our earlier challenges
<br>**[ file:///data/data/jakhar.aseem.diva/shared_prefs/jakhar.aseem.diva_preferences.xml ]**
<br>![8-5](https://teckk2.github.io/assets/images/DIVA/8-5.png)
<br>As you can see we can view the XML file which store our credential from the challenge 3 which we solved earlier.
<br>Now let’s have the source code of the application which is the reason for this vulnerability
<br>![8-6](https://teckk2.github.io/assets/images/DIVA/8-6.png)
<br>![8-7](https://teckk2.github.io/assets/images/DIVA/8-7.png)
<br>This piece of code allow to read any URL even the system internal files, without validating or sanitizing it properly and as the application have permission to read any file in the system, because of which we were able to easily read any file even on SDcard.


<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
