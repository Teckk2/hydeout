---
layout: post
title: (OWASP) A8-Cross-Site Request Forgery (CSRF)
categories:
  - Web-Pentesting
---

<p>This attack can be Consider as anyone who can load content into your users’ browsers, and thus force them to submit a request to your website. Any website or other HTML feed that your users access could do this.
Attacker creates forged HTTP requests and tricks a victim into submitting them via image tags, XSS, or numerous other techniques. If the user is authenticated, the attack succeeds.</p>
<br>CSRF takes advantage the fact that most web apps allow attackers to predict all the details of a particular action. Because browsers send credentials like session cookies automatically, attackers can create malicious web pages which generate forged requests that are indistinguishable from legitimate ones.
Detection of CSRF flaws is fairly easy via penetration testing or code analysis.

<p Class="message">
  <font color="Black">Question 1</font> – What is Cross-Site request forgery (CSRF)?
</p>
<br>**Ans**:- 

*	A Vulnerability that makes it possible for an attacker to force a user to unknowingly perform actions.
*	Common targets for CSRF include cloud storage, Social media, Banking & On-Line shopping web application.
*	Approximately 23% of all applications tested are Vulnerable to Cross-Site Request forgery.

<p Class="message">
  <font color="Black">Question 2</font> – Why is CSRF an issue?
</p>
<br>**Ans**:- 

*	Depending on the action being performed, a CSRF Vulnerability can have Serious Consequences for the user using the web application.
*	Users are usually unaware that malicious actions are being performed.
*	Practical applications of CSRF range from embarrassing social media post to losing money from your online accounts.

<p Class="message">
  <font color="Black">Question 3</font> – How an Online Banking CSRF accomplished?
</p>
<br>**Ans**:- 

*	While logged into your bank, you visit a page that contains a CSRF attack.
*	Upon Visiting the page, a request is performed to transfer money from one account to another.

<p Class="message">
  <font color="Black">Question 4</font> – How did CSRF occurs?
</p>
<br>**Ans**:- The two main reasons:

*	The banking application allows requests to originate from Servers other than itself.
*	There is no unique token that is tied to the user session.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
