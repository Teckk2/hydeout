---
layout: post
title: (OWASP) A4-Insecure Direct object Reference
categories:
  - Web-Pentesting
---

<p>Insecure Direct Object References occur when an application provides direct access to objects based on user-supplied input. As a result of this vulnerability attackers can bypass authorization and access resources in the system directly, for example database records or files.</p>
<p>Insecure Direct Object References allow attackers to bypass authorization and access resources directly by modifying the value of a parameter used to directly point to an object. Such resources can be database entries belonging to other users, files in the system, and more. This is caused by the fact that the application takes user supplied input and uses it to retrieve an object without performing sufficient authorization checks.</p>

<p Class="message">
  <font color="Black">Question 1</font> – What Insecure Direct Object Reference?
</p>
<br>**Ans**:- Insecure Direct Object Reference occur when an application provides direct access to objects based on user supplied input. As a result of this Vulnerability attackers can bypass authorization and access resources in the system directly, for example database records or files.

<p Class="message">
  <font color="Black">Question 2</font> – What are the Risk of Insecure Direct Object Reference?
</p>
<br>**Ans**:- Insecure Direct Object Reference allow attackers to bypass authorization & access resources directly by modifying the value of a parameter used to directly point to an object. Such resources can be database entries belongings to other users, files in the system, & more. This is caused by the fact that the application takes user supplied input & uses it to retrieve an object without performing sufficient authorization checks.

<p Class="message">
  <font color="Black">Question 3</font> – How to prevent yourself from Insecure Direct Object Reference?
</p>
<br>**Ans**:- Create a map within your CODE that maps objects that could be referenced internally to aliased terms which are exposed to the user.
<br>**For example:-** An array of primary keys to a particular table might be mapped to a random sequence of integers. When the value is Submitted by the user, the number is matched to the real value. This prevents disclosure of the actual value & also limits what the user can alter.
<br>**Example:**

<br>&nbsp; &nbsp; &nbsp; &nbsp;‘default’		=> 	‘index.html’
<br>&nbsp; &nbsp; &nbsp; &nbsp;‘account_summary’	=>	‘account_summary.html’
<br>&nbsp; &nbsp; &nbsp; &nbsp;‘user_profile’		=>	‘user_profile.html’

* Values supplied by the user should be vetted through an access control function to verify that they do in fact have access.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
