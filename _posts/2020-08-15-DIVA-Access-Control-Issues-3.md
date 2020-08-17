---
layout: post
title: DIVA - Access Control Issues - Part 3
categories:
  - Mobile
---

<br>Now we have reached to the last challenge of our Access Control Issues
<br>![11-1](https://teckk2.github.io/assets/images/DIVA/11-1.png)
<br>The application is meant to save notes, but before accessing the notes we need to create a 4 digit pin, once we do that we can access the notes, but the objective of this challenge is to view the notes without entering the pin, let’s have a look in the application and then we will analyze AndroidManifest.xml
<br>![11-2](https://teckk2.github.io/assets/images/DIVA/11-2.png)
<br>Put your 4 digit pin and click on create/change pin
<br>Once you create a pin, you will able to see a new option to go to private notes
<br>![11-3](https://teckk2.github.io/assets/images/DIVA/11-3.png)
<br>![11-4](https://teckk2.github.io/assets/images/DIVA/11-4.png)
<br>It will again ask you to enter your pin
<br>![11-5](https://teckk2.github.io/assets/images/DIVA/11-5.png)
<br>Once you enter the correct pin, you will be able to see the private notes
<br>Now let’s have a look at AndroidManifest.xml to find the vulnerable piece of code.
<br>![11-6](https://teckk2.github.io/assets/images/DIVA/11-6.png)
<br>If you focus on the above highlighted line, it shows the content provider is set to [**android:enabled:”true”**]
<br>Generally the content provider is represented like [content://] let’s have a look inside smali code and find the correct URI
<br>![11-7](https://teckk2.github.io/assets/images/DIVA/11-7.png)
<br>If we try to find the content:// from all the file, we found the following inside the NotesProvider.smali, let’s open and have a look inside
<br>![11-8](https://teckk2.github.io/assets/images/DIVA/11-8.png)
<br>As you can see in the above URI it provide us the exact URI path 
<br>[**content://jakhar.aseem.diva.provider.notesprovider/notes**]
<br>If you remember few steps above we found that the content provider can we queried without any permission, let’s try to open it from adb shell
<br>[**adb shell content query --uri content://jakhar.aseem.diva.provider.notesprovider/notes**]
<br>![11-9](https://teckk2.github.io/assets/images/DIVA/11-9.png)
<br>As you can see we can view all the private notes from the application without providing any pin. 

<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
