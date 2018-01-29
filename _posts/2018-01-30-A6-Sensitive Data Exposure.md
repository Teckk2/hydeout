---
layout: post
title: (OWASP) A6-Sensitive Data Exposure
categories:
  - Web-Pentesting
---

<p>Using this vulnerabilty an attacker can gain access to your sensitive data and any backups of that data. This includes the data at rest, in transit, and even in your customers’ browsers. Include both external and internal threats. 
Attackers typically don’t break crypto directly. They break something else, such as steal keys, do man-in-the-middle attacks, or steal clear text data off the server, while in transit, or from the user’s browser.</p>
<br>The most common flaw is simply not encrypting sensitive data. When crypto is employed, weak key generation and management, and weak algorithm usage is common, particularly weak password hashing techniques. Browser weaknesses are very common and easy to detect, but hard to exploit on a large scale. External attackers have difficulty detecting server side flaws due to limited access and they are also usually hard to exploit.

<p Class="message">
  <font color="Black">Question 1</font> – What is Sensitive data?
</p>
<br>**Ans**:- 

*	Banking Information (account number, credit card numbers).
*	Health Information.
*	Personal information (date of birth, SSN/SIN)
*	User account/passwords.

<p Class="message">
  <font color="Black">Question 2</font> – What are the implications?
</p>
<br>**Ans**:- 

*	Financial loss
*	Identity Hi-jacking
*	Decreased brand trust

<p Class="message">
  <font color="Black">Question 3</font> – What are the main cause of this vulnerability?
</p>
<br>**Ans**:- 

*	Insufficient Transport Layer Protection
*	Insecure Cryptographic storage
  *	Data stored in an unprotected manner can be easily stolen.

<p Class="message">
  <font color="Black">Question 4</font> – How to prevent yourself from Sensitive Data Exposure?
</p>
<br>**Ans**:- 

*	Encrypt data during transport & at rest.
*	Minimize data Surface area.
*	Use the latest encryption algorithms.
*	Disable autocomplete on forms that collect data.
*	Disable caching on forms that collect data.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
