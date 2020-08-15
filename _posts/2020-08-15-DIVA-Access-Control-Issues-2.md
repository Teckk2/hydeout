---
layout: post
title: DIVA - Access Control Issues - Part 2
categories:
  - Mobile
---

<br>Now we will move to our next challenge which is the second part of the Access Control Issues, in which there are two option either we can register and get a pin to see the Tveeter API credential, or if we already have the pin we can see the API credentials, So the objective of this challenge is to access the API credentials without registering for it.
<br>![10-1](https://teckk2.github.io/assets/images/DIVA/10-1.png)
<br>Before we proceed let’s have a quick view of source code ()
<br>![10-2](https://teckk2.github.io/assets/images/DIVA/10-2.png)
<br>If you solved the previous challenge, I explained in that the intent filter should not be considered as protection method, if you are using it in an activity, eventually it will be accessible to export publicly.
<br>So let’s open our adb shell and exploit this
<br>**{ adb shell am start jakhar.aseem.diva/.APICreds2Activity}**
<br>![10-3](https://teckk2.github.io/assets/images/DIVA/10-3.png)
<br>![10-4](https://teckk2.github.io/assets/images/DIVA/10-4.png)
<br>But in the application it’s still asking for pin, now we need to find a way to bypass it
<br>Let’s have a look at APICreds2Activity.class to understand the application in more detail
<br>![10-5](https://teckk2.github.io/assets/images/DIVA/10-5.png)
<br>![10-6](https://teckk2.github.io/assets/images/DIVA/10-6.png)
<br>![10-7](https://teckk2.github.io/assets/images/DIVA/10-7.png)
<br>After analyzing both the source code, we could understand that to view the credential we need a pin, but if we disable the pin check it will ask for no further verification and land us directly to the API credentials, let’s try this
<br>**{adb shell am start jakhar.aseem.diva/.APICredsActivity check_pin false}**
<br>![10-8](https://teckk2.github.io/assets/images/DIVA/10-8.png)
<br>**{ adb shell am start jakhar.aseem.diva/.APICredsActivity -ez check_pin false}**
<br>![10-9](https://teckk2.github.io/assets/images/DIVA/10-9.png)
<br>You can try both the commands, whichever works for you.
<br>![10-10](https://teckk2.github.io/assets/images/DIVA/10-10.png)
<br>And it works like a charm, this time it didn’t ask for any PIN and landed us directly to the view credentials.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
