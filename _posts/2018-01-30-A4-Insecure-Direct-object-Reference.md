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
