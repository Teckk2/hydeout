---
layout: post
title: (OWASP) A7-Missing Function Level Access Control
categories:
  - Web-Pentesting
---

<p>Anyone with network access can send your application a request. Could anonymous users access private functionality or regular users a privileged function?
Attacker, who is an authorized system user, simply changes the URL or a parameter to a privileged function. Is access granted? Anonymous users could access private functions that aren’t protected.</p>
<br>Applications do not always protect application functions properly. Sometimes, function level protection is managed via configuration, and the system is misconfigured. Sometimes, developers must include the proper code checks, and they forget.
Detecting such flaws is easy. The hardest part is identifying which pages (URLs) or functions exist to attack.

<p Class="message">
  <font color="Black">Question 1</font> – What is Missing function level access Control?
</p>
<br>**Ans**:- 

*	Can a user directly browse to a resource?
*	Does the UI expose an unauthorized resource?
*	Server should not solely rely on user supplied input.

<p Class="message">
  <font color="Black">Question 2</font> – How to prevent yourself from this Vulnerability?
</p>
<br>**Ans**:- 

*	Deny access to functionality by default.
*	Use Access control lists & role based authentication mechanism.
*	Don’t just hide functions.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
