---
layout: post
title: (OWASP) A1-Injection
categories:
  - Web-Pentesting
---

<p>Injection flaws occur when untrusted data is sent to an interpreter as part of a command or query.
The attacker’s hostile data can trick the interpreter into executing unintended commands or accessing data without proper authorization.</p>

<p Class="message">
  <font color="Black">Question 1</font> – What is Injection?
</p>
<br>**Ans**:- 

* There are many types of injection vulnerabilities, some of the most common include:
  * SQL Injection
    * Error based SQLi
    * Blind SQLi
    * String SQLi
    * Blind Numeric SQLi
    * Blind String SQLi
  * Code injection
  * OS Commanding
  * LDAP Injection
  * XML injection
  * XPATH Injection
  * SSL injection
  * IMAP/SMTP Injection
  * Buffer Overflow
  
* All involve allowing untrusted or manipulated request, Commands, or queries to be executed by a web application.
* SQL injection alone continues to be the most common breach paradigm in 2013.

<p Class="message">
  <font color="Black">Question 2</font> – What are the Risk of Inejection?
</p>
<br>**Ans**:- Injection vulnerability also present some of the most significant risk when effectively exploited. Some of these risk include:

* Data loss or corruption.
* Data could be stolen.
* Unauthorized access.
* Denial of access.
* Complete host System takeover.

<p Class="message">
  <font color="Black">Question 3</font> – How to prevent yourself from this vulnerability?
</p>
<br>**Ans**:- 

* Use a Vetted Library or Framework.
* Use an API which avoids the use of an interpreter (parameterized).
* Run the application with minimum privileges.
* Escape all special characters used by an interpreter.
* Input Validation/Sanitization, white list only allowed characters.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
