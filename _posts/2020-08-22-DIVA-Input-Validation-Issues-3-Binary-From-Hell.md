---
layout: post
title: DIVA - Binary From Hell 😈
categories:
  - Mobile
---

<br>So let me clarify one thing straight away, after trying a lot of thing me and KNX was not be able to solve this binary in the intended way, although we are able to do that by manipulating the internal function of the application using FRIDA which is equivalent to Cheating, so the main focus of this blog is to show what are the mistakes and all the FAIL attempt we did and what all things we learned from our journey.
<br>**Let’s Start!!**
<br>So after we notice the application crashed successfully now let’s have a look at logcat
<br>In the terminal open adb logcat and analyze the logs
<br>![14-1](https://teckk2.github.io/assets/images/DIVA/14-1.png)
<br>As you can see the application give the input to the CPU to jump to the location (0x41414141) thus the location address is unknown, which eventually result in crash of the application. And which is also a classic example to exploit a vanilla BOF, let’s exploit and try to get a reverse shell.
<br>For those who don’t know x41 is the hex value for (A)
<br>Now we need to find the offset manually in able to exploit it further, We will try to decrease and keep checking logcat and find in how much strings the address changes
<br>I tried with 35 A’s and I notice the difference of -1 x41
<br>![14-2](https://teckk2.github.io/assets/images/DIVA/14-2.png)
<br>Then I try again with 34 A’s to confirm
<br>![14-3](https://teckk2.github.io/assets/images/DIVA/14-3.png)
<br>We are very close, now try from little backward
<br>![14-4](https://teckk2.github.io/assets/images/DIVA/14-4.png)
<br>The correct offset is 32 because when I tried with 31 A’s it doesn’t crash, but when I tried with 32 A’s the application crashed.  So as we know our offset point, let’s move to the next step
<br>![14-5](https://teckk2.github.io/assets/images/DIVA/14-5.png)
<br>Now we will try with 32 A’s and 4 set of B’s to over write and control the EIP
<br>![14-6](https://teckk2.github.io/assets/images/DIVA/14-6.png)
<br>To proceed with further steps of debugger we need a proper debugger to be attached, so open adb shell and enable gdbserver and connect it remotely 
<br>![14-7](https://teckk2.github.io/assets/images/DIVA/14-7.png)
<br>Make sure you are root, then we will attached the application PID with gdbserver so now we can just connect remotely, but before that we need to forward the port
<br>Open another terminal and run this command with the port you specified 
<br>[**adb forward tcp:8888 tcp:8888**] you may need root permission to run all these commands, so if you face any permission issued don’t forget to run [adb root] before doing all steps
<br>![14-8](https://teckk2.github.io/assets/images/DIVA/14-8.png)
<br>Now everything is setup, initially I tried connect to gdbserver from my kali VM, but I was facing some issue in pivoting the network, then later I installed kali as a windows susbsytem, you can just download kali from Microsoft Store
<br>![14-9](https://teckk2.github.io/assets/images/DIVA/14-9.png)
<br>Once installed run this below command to enable windows subsystem feature, or you can do vice-versa as you wish.
<p class="message">
  Enable-WindowsOptionalFeature -Online -FeatureName Microsoft-Windows-Subsystem-Linux
</p>
<br>Once kali is setup, you can start updating the repos, and install everything you need like: netcat, gdb, msf or if you need anything else for future use, it’s up to you.
<br>You can also download [GDB](https://github.com/hugsy/gdb-static/blob/master/gdb-7.10.1-x32) static binary directly into your android device but in later stage we need gef which have some compatibly issues 
<br>Once you install gdd in your KALI, you can download [gef](https://github.com/hugsy/gef) plugin, to ease our work for this debugging process. 
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>


<p class="message">
  ~ tavşanı sever
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
