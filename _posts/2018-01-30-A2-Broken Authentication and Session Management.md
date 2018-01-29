---
layout: post
title: (OWASP) A2-Broken Authentication and Session Management
categories:
  - Web-Pentesting
---

<p>In this attack, an attacker (who can be anonymous external attacker, a user with own account who may attempt to steal data from accounts, or an insider wanting to disguise his or her actions) uses leaks or flaws in the authentication or session management functions to impersonate other users. Application functions related to authentication and session management are often not implemented correctly, allowing attackers to compromise passwords, keys, or session tokens, or to exploit other implementation flaws to assume other users’ identities.</p>
<p>Developers frequently build custom authentication and session management schemes, but building these correctly is hard. As a result, these custom schemes frequently have flaws in areas such as logout, password management, timeouts, remember me, secret question, account update, etc. Finding such flaws can sometimes be difficult, as each implementation is unique.</p>

<p Class="message">
  <font color="Black">Question 1</font> – What is Broken Authentication and Session Management?
</p>
<br>**Ans**:- 

* A Vulnerability that allows the capture or bypass of authentication methods used to protect against unauthorized access.
* Most Common Authentication Schema is the use of a Username & Password.
* Approximately 23% of all application tested are Vulnerable to Broken Authentication & Session Management.

<p Class="message">
  <font color="Black">Question 2</font> – What are the steps that are performed when logging into a web application?
</p>
<br>**Ans**:- 

* First, the user is asked to provide login credentials which usually consists of username & password.

  <br>( e.g. Username = Teck, Password = Teck@123 )

* This information is submitted to the application & a session ID is generated which is liked to the Credentials.

  <br>( e.g Sessionid = lnKXXeiqJacQlUGvPsgqi0EanMZviPZrPwd7DP2b71 )

<p Class="message">
  <font color="Black">Question 3</font> – What are the ways a web application can fail to protect the Username, Password & Session ID Values?
</p>
<br>**Ans**:- 

* Unencrypted Connections.
* Predictable Login Credentials.
* Session Value does not timeout or does not get validated after logout.
* User authentication Credentials are not protected when stored.
* Session IDs are used in the URL.

<br>Example:- Unencrypted Connections.
* Reason for Vulnerability:
  <br>All information that you are Sending/Receiving between yourself & the web application can be intercepted without your knowledge.
* Fails to protect:
  <br>Username, Password & Session ID values.
* Preventing this weakness:
  <br>Enable encryption on requests that contain sensitive information.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
