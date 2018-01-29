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

p Class="message">
  <font color="Black">Question 2</font> – What are the steps that are performed when logging into a web application?
</p>
<br>**Ans**:- 

* First, the user is asked to provide login credentials which usually consists of username & password.

  <br>( e.g. Username = Teck, Password = Teck@123 )

* This information is submitted to the application & a session ID is generated which is liked to the Credentials.

  <br>( e.g Sessionid = lnKXXeiqJacQlUGvPsgqi0EanMZviPZrPwd7DP2b71 )
