---
layout: post
title: (OWASP) A3-Cross-Site Scripting (XSS)
categories:
  - Web-Pentesting
---

<p>Cross-Site Scripting (XSS) attacks are a type of injection, in which malicious scripts are injected into otherwise benign and trusted web sites. XSS attacks occur when an attacker uses a web application to send malicious code, generally in the form of a browser side script, to a different end user. Flaws that allow these attacks to succeed are quite widespread and occur anywhere a web application uses input from a user within the output it generates without validating or encoding it.</p>
<p>An attacker can use XSS to send a malicious script to an unsuspecting user. The end user’s browser has no way to know that the script should not be trusted, and will execute the script. Because it thinks the script came from a trusted source, the malicious script can access any cookies, session tokens, or other sensitive information retained by the browser and used with that site. These scripts can even rewrite the content of the HTML page.</p>

<p Class="message">
  <font color="Black">Question 1</font> – What is (XXS) ?
</p>
<br>**Ans**:- 

* An attacker can inject unrestricted snippets of JavaScript into your application without Validation.
* This JavaScript is then executed by the victim who is visiting the target site.
* There are 3 Primary types of XSS, Reflected, Stired, & DOM based.
  *	Reflected XXS - An attacker sends the victim a link to the target application through email, social media, etc. This link has a script embedded within it which executes when visiting the target site
  *	Stored XSS – An attacker is able to plant a persistent Script in the target Website which will execute when anyone visits it.
  *	Dom Based XSS – No HTTP request is required, the script is injected as a result of modifying the DOM of the target site in the client side code in the victim’s browser and is then executed.
* Approximately 17% of all applications tested are vulnerable to XSS.

<p Class="message">
  <font color="Black">Question 2</font> – What are the Risk of (XSS) ?
</p>
<br>**Ans**:- 

* Compromise or take over the Victim’s user account in the application.
* Retrieval of data from the target web application.
* Modification of content on the target page.
* Redirection victim’s to another malicious or spoof site.
* Platform to install other malware on the victim’s system.

<p Class="message">
  <font color="Black">Question 3</font> – How to prevent yourself from (XSS) ?
</p>
<br>**Ans**:- Many different strategies can be used to protect an application against (XXS).

  *	Use Vetted Library or Framework
  * Output Encoding
  * Use HTTP Only attribute
  * Input Validation

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
