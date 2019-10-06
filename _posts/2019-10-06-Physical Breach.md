---
layout: post
title: Physical Breach
categories:
  - Red Teaming
---


<div class="background-wrap">
	<video id="video-bg-elem" preload="auto" autoplay="true" loop="loop" muted="muted">
		<Source src="http://giphygifs.s3.amazonaws.com/media/5CsmAaFsM0sZa/giphy.mp4" type="video/mp4">
	</video>
</div>


<br>In past few years I observed that most of the people in Infosec don't understand a simple logic, Safety is not a product but a process and must be introduced already in the design phase, typical example the development of safe code (SDC) etc. So many beautiful words and phrases made, and then the reality of the facts? I see a lot of companies entrusting the entire security of their business to the latest equipment (firewall, IDS/IPS & co) by closing the corporate perimeter as much as possible inside a digital wall with the belief that if block threats from the outside, I don't need to secure what's inside. Very well, what if the threat came from the inside? What if someone can get in? These are the companies that then become so debilitated by a cyber-attack to the point that they find themselves forced to close their business.

<br>Few months back we got few projects where I have to perform physical breach, So in this Blog I will share the experience of two of my clients, one which is related to Payment Industry and the second one is Holding Company for them I have to do a physical breach on their showrooms. Let's start:

<br>Let's start with the **First client**, So as we all know before attacking any target enumeration is the most important part, similarly in physical breach also, we need to enumerate every single thing which could help us to breach it successfully, So my colleagues already went in that office for some casual meetings, he took some Videos and pictures of guest entry card, which helped me to understand the security posture, and I created a cloned visitor card, which looks identical to the original card, in case someone ask me about my card, then we noticed another thing, the lift lobby was in middle of the corridor, if you turn left after 10 steps there is security desk where you have to submit your ID and get a visitors card, and from there you can enter the office, and if you turn right there is one door which opens to the office IT department directly, but for that we need a valid RFID card.

<br>Now the plan was me and my colleagues will go in lift until we found someone who is going on the same floor, we were lucky within few minutes we found someone who was going to the same floor, Now time to execute the plan, as soon we reached that floor, my colleagues moved first and turned left to engage the security for me, and I just followed that guy pretending to be on phone, and the tailgating method worked perfectly.

<br>Now I was inside the office and the time was around 3:30 or 4 PM and people usually leave by 4, So it was just perfect time for me to do this activity, after roaming for few minutes I found one place in middle of the office desk area where no one was sitting, there were couple of people were sitting around me, but they were too busy already in their work.

<br>Now I was sitting on a Desk and I found one employee card and the desk belongs to the same person, I wear that employee ID and turned it to back side so no one can see the picture on the card to identify, Now I have access to any RFID door in the office, I later found that card belongs to the finance Manager of the company LoL.

<br>Now time to get inside the network, I removed the cable from the VOIP phone on my desk and connected and after enumerating for some time, I realize that have a NAC, and to bypass I followed my old method **[Bypassing NAC](https://teckk2.github.io/red%20teaming/2019/10/06/Physical-Breach.html)**, but this time the situation was a bit different, the VOIP phone was totally segregated on different Vlan, but I found one Printer broadcasting the wifi, and using airmon-ng I got the mac address of that printer, and luckily that printer was part of that network, and I bypassed the NAC and scanned their whole network and once I scanned everything collected my documents and screenshot, the activity got over and I went out of the office without detecting.


<br>Now time for the **Second Client**, as I mentioned earlier it is a holding company so they manage a lot of showrooms in multiple locations and Malls, So the scenario is I need to perform physical breach on their 5 different showrooms in 2 Big Malls in a single day.
So this time there was no chance of doing enumeration or anything, What all I had was just 1 shot, either I will succeed or fail and they could hand me over to the police, but for that I had a agreement with my client, and they already gave me a immunity papers, in case something goes wrong.

<br>Now before 2 days when I was about to perform the activity I designed and created a New Employee Card which doesn't look similar to the real Employee card, and I Mention my name on that and added the designation of Network Department from their Parental IT Department,
and put the Parental Company logo in Top front, and Top Back and office address and Phone no. on the Back. 

<br>Everything was ready and I put on my suit again to fool some more people 😜.

<br>**1)** I reached my **First** Target showroom and was successfully able to breach the physical security by showing my fake ID And the reason I mention to visit that office was, Our IT team is facing some issue connecting from there office to HO, But there was one guy in the IT Department there, who connected me on call with IT head before giving me the entry to the office where he asked me for the legitimate email, and I was able to convince him that he will get a Mail shortly from head of IT Security, but within some time he already arranged a person to assist me and gave me network access **Wink-Wink**.

<br>Now I was sitting inside their IT department with full access to their network and without any mail sent to the IT Department, in this activity no malicious payload was executed, I only connected to the network and checked the IP address in order to provide a POC.

Within 5 Min I finish my job and went out and after 10 min I got the call from IT head of that Showroom that he still didn’t receive any Mail from HO IT Department, This shows the Loophole where an attacker can get the access to the network easily without even sending a Valid email to the IT Department.


<br>**2)** Now move to the **Second** Showroom, I went inside the showroom, on the main entry I noticed one sales computer, and a lady was standing near that, I asked the lady that I am from HO IT department (showed the ID card form a distance) and want to access this machine, and without doing any more effort the lady got convinced and handed over me the machine, I then tried to plugin a USB device but the USB access was blocked, then I tried to access Internet but there was proxy login enabled.

<br>Once that done, I went ahead and reached the last corner of the showroom, where there was one unattended sales computer was there, I has full access to that machine, but that machine was not connected to the network, but there was one VOIP Phone in the same Desk, I removed the cable and connected to my own laptop to check the connectivity, and shockingly there was one sales guy attending a Customer and walked just in front of me but didn’t ask a single question, and couple of security guys were also standing in a distance where they were able to see me, and didn’t ask a Single question. This is because of Human Phycology, which judge you based on your cloths, if you are wearing a Suite that means you are a Good person. That is what I used it to make this test execute more effectively.

<br>**3)** Time for the **Third** Showroom, I went inside and did the same approach, that I am from HO IT Department and we are facing some issue connecting from this network to our HO, So I need to diagnose the network which will not take much time, but there was one lady who came near to me and asked for my ID card, after Analyzing the card for couple of Second she showed me the way to the sales computer, by the time I was performing my task she was trying to call the IT depart, but she called someone else by mistake and I utilized that time and completed my work, and within 2 min the test was finish, she asked me to sign me in the staff register for records and I had no issue giving my Autograph in their Staff register 😂.

<br>**4)** Now the next two showrooms were located in a different Mall, I reached my **Fourth** target showroom and noticed that it is one of the biggest and secured showroom in the list and very hard to breach, So I started with the same approach by asking a sales person to gave him access to their sales computer, but the lady asked me to go backside of the showroom and get a Staff Entry, then only she will be able to give the access, which was quite good, Generally as an attacker it’s really hard to convince a Security Person to fool them with a Fake Card and the risk of getting caught increase drastically.

<br>So I entered security room from the back side of the showroom, and asked the security person that I am from HO IT department and we are facing some Issue connecting to our HO Network, So he connected me to their IT department manager, I explained him the same thing and also mentioned that I work under HO IT Security head and he asked me to do this troubleshooting, and the IT Manager got very convinced with this and gave approval to the security guy to give me a Staff entry to the showroom.

<br>After hanging up the phone, the security guy notice my ID Card and asked me why there is no Employee ID no. on my Company ID card, So I replied him very calmly, that I recently join this company like last month so I didn’t get any Employee ID yet, and it really worked. Then he took my Government ID and gave a me a Staff RFID Card, with which I had access to any door in the showroom (**Perfect**), Now I start looking a sales person who should stand alone and not with any colleague, as it’s easy to convince a single person then multiple standing together, As I found my target, I got the access to the machine with the similar approach and it was very easy to convince them as they can see a Staff ID in my hand, So there is no reason to ask me any further question. Once I finish the ground floor testing, I went back to security room and gave my staff card and took back and the Government ID card.

Then again entered the showroom and went to the First floor, and walked straight to one section, and there convinced the sales guy with the same approach and got the access to the machine, and he didn’t even bother to ask me for any staff ID Card or anything.

<br>**5)** Now comes the last showroom in the list, As soon I entered the showroom a sales person attended me and I asked him the same thing that I am from HO IT Department, and without asking me as single question he escorted me to One of the sales machine, but there was one more guy who asked me some question so I explained him why I am here and all, I showed him my Fake Employee ID and after looking at the ID for couple of Seconds, he handed over the machine to me, and once I finish my activity one lady came to me to enter my name and sign for Staff Entry Record. 


<br>**Conclusion and Mitigation** - The Activity Executed with the Success rate of 100%, The main reason for that is lack of physical breach awareness in the staff, and as being in the job where they attend the clients whole day, they are too polite and shy to challenge someone. IT and Security team should Confirm via Email, even if someone is saying he is from HO IT department, they should not give the access or Entry until they get a Confirmation Email from a legitimate Person. I also noticed that the Security and Staff are not aware that they all have a same design Employee ID Card, because of which I was able to successfully breach all location with my Fake ID card.  


<p class="message">
  ~ Hack the World and Stay Noob.
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
