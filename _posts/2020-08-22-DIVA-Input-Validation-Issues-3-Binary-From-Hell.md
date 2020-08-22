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
<br>![14-10](https://teckk2.github.io/assets/images/DIVA/14-10.png)
<br>Now open gdb and connect to the remote local port, as we are now sharing the same network port with the host, there will be no issue connecting to the local port which we forwarded.
<br>![14-11](https://teckk2.github.io/assets/images/DIVA/14-11.png)
<br>![14-12](https://teckk2.github.io/assets/images/DIVA/14-12.png)
<br>![14-13](https://teckk2.github.io/assets/images/DIVA/14-13.png)
<br>As you can see we can’t use run, which restricted us to a limited debugging feature to use only Continue and get all the inputs directly from the application.
<br>![14-14](https://teckk2.github.io/assets/images/DIVA/14-14.png)
<br>![14-15](https://teckk2.github.io/assets/images/DIVA/14-15.png)
<br>I tried to feed first 32 bytes as A’s and 4 bytes of B’s and then lot of C’s and the ESP and EBP is full of our C’s as we can see in our gdb output, this is where we will store our shellcode.
<br>There is one drawback in debugging Android application, every time you crash the application, you need to restart the application, but in our case it restart automatically, but create a new PID every time which means you need to set the gdbserver with the new PID again and again after every crash.
<br>![14-16](https://teckk2.github.io/assets/images/DIVA/14-16.png)
<br>As we already know the offset, the next step is to find jump esp address and bad characters, so we can generate our shellcode and get a reverse shell without any issues. 
<br>After some time, if you face issue of crashing the app regularly, you can just try deleting the cache or app data, and allow full storage access, it may solve your problem as it solved mine.
<br>![14-17](https://teckk2.github.io/assets/images/DIVA/14-17.png)
<br>First let’s find out the esp address where we will jump our shellcode, we will quickly duplicate 500 c’s using python 
<br>![14-18](https://teckk2.github.io/assets/images/DIVA/14-18.png)
<br>And add it after our offset and EIP
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now setup the gdb and paste this inside application to crash it
<br>![14-19](https://teckk2.github.io/assets/images/DIVA/14-19.png)
<br>![14-20](https://teckk2.github.io/assets/images/DIVA/14-20.png)
<br>Now let’s analyze ESP and see how much space we have for our shellcode and where we can jump to
<br>![14-21](https://teckk2.github.io/assets/images/DIVA/14-21.png)
<br>Looks like we have all the 500 bytes of data to use, perfect now we can move to our next step to find bad characters, and we can use any of the address mention on the left side,
<br>![14-22](https://teckk2.github.io/assets/images/DIVA/14-22.png)
<br>The safest option is to leave the first 16 bytes as nop slides(\x90) and put your shellcode from 0xbf7fc760: or whatever address you have in your system respectively. 
<br>But the complexity in this binary is, if you feed an ascii character, then the CPU will convert it to UTF8-hex by itself, but if you try to feed a hex value for example; if you try to feed hex value of C which is 43, the CPU will convert it to hex itself and revert the value so, the hex value of 43 should be 3433 but the CPU will revert it and show us like 3334 which means the ascii is 34, this is very complex but easy if you understand a simple logic.
<br>![14-23](https://teckk2.github.io/assets/images/DIVA/14-23.png)
<br>Now let’s try something and see if it works or not, let’s take a scenario we want to see x90 in $ESP , but the CPU will convert it to 3039, so what should we de?
<br>As we already know CPU is converting everything into UTF8-HEX itself, so we can go one step back and convert x90 into ascii which resemble for **[space]**
<br>![14-24](https://teckk2.github.io/assets/images/DIVA/14-24.png)
<br>Write a simple code to convert hex into ascii, as we want 90 in our registers
<br>Now run and save it into a new file.
<br>![14-25](https://teckk2.github.io/assets/images/DIVA/14-25.png)
<br>Open file and press ctrl+A and you will see just space, as we expected, we are on the right path, now go to the start line and add 32 A’s and 4 B’s
<br>![14-26](https://teckk2.github.io/assets/images/DIVA/14-26.png)
<br>It should look like this, now copy everything and feed it into application and analyze the debugger
<br>![14-27](https://teckk2.github.io/assets/images/DIVA/14-27.png)
<br>![14-28](https://teckk2.github.io/assets/images/DIVA/14-28.png)
<br>Haha, finally I could see the desired result, but it’s still in little endian style did default by CPU
<br>![14-29](https://teckk2.github.io/assets/images/DIVA/14-29.png)
<br>Now we need to find the bad character, after analyzing I understand that the application only allow ascii characters to be as input, so if we feed anything other than ascii it will be messed
<br>![14-30](https://teckk2.github.io/assets/images/DIVA/14-30.png)
<br>So we will only focus on these hex bytes for our future reference
<br>Now remove the \x and make it simple
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f202122232425262728292a2b2c2d2e2f303132333435363738393a3b3c3d3e3f404142434445464748494a4b4c4d4e4f505152535455565758595a5b5c5d5e5f606162636465666768696a6b6c6d6e6f707172737475767778797a7b7c7d7e7f
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>You can convert hex to ascii from any online tool like [Rapidtables](https://www.rapidtables.com/convert/number/hex-to-ascii.html)
<br>![14-31](https://teckk2.github.io/assets/images/DIVA/14-31.png)
<br>If we convert this hex into ascii it will look like this, but this is also not working, because of special keyboard sign like upper arrow or something similar sign which CPU is not able to identify when feeding directly from the application, so now what we have left is all the keyboard signs and alpha numeric and remove all the keyboard signs.
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>!"#$%&'()*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\]^_\`abcdefghijklmnopqrstuvwxyz{|}~
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now convert it to hex
<br>![14-32](https://teckk2.github.io/assets/images/DIVA/14-32.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
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
