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
  DEMO
</h1>
  * [HTML Injection -Reflected (GET)](https://teckk2.github.io/web-pentesting/2018/02/07/HTML-Injection-Reflected(GET).html)
  * [HTML Injection -Reflected (POST)](https://teckk2.github.io/web-pentesting/2018/02/07/HTML-Injection-Reflected(POST).html)
  * [HTML Injection -Reflected (URL)](https://teckk2.github.io/web-pentesting/2018/02/07/HTML-Injection-Reflected(URL).html)
  * [HTML Injection -Stored (Blog)](https://teckk2.github.io/web-pentesting/2018/02/07/HTML-Injection-Stored(Blog).html)
  * [iFrame Injection](https://teckk2.github.io/web-pentesting/2018/02/07/iFrame-Injection.html)
  * [OS Command Injection](https://teckk2.github.io/web-pentesting/2018/02/07/OS-Command-Injection.html)
  * [OS Command Injection –Blind](https://teckk2.github.io/web-pentesting/2018/02/07/OS-Command-Injection-Blind.html)
  * [PHP Code Injection](https://teckk2.github.io/web-pentesting/2018/02/07/PHP-Code-Injection.html)
  * [Server-Side Includes (SSI) Injection](https://teckk2.github.io/web-pentesting/2018/02/07/Server-Side-Includes-(SSI)-Injection.html)
  * [SQL Injection (Search/GET)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-(Search-GET).html)
  * [SQL Injection (Select/GET)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection(Select-GET).html)
  * [SQL Injection (Search/POST)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection(Search-POST).html)
  * [SQL Injection (POST/Select)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-(POST-Select).html)
  * [SQL Injection (AJAX/JSON/jQuery)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection(AJAX-JSON-jQuery).html)
  * [SQL Injection (CAPTCHA)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection(CAPTCHA).html)
  * [SQL Injection (Login Form/Hero)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-(Login-Form-Hero).html)
  * [SQL Injection (Login Form/User)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-(Login-Form-User).html)
  * [SQL Injection (SQLite)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-(SQLite).html)
  * [SQL Injection (Drupal)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-(Drupal).html)
  * [SQL Injection -Stored (Blog)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-Stored-(Blog).html)
  * [SQL Injection -Stored (SQLite)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-Stored-(SQLite).html)
  * [SQL Injection -Stored (User-Agent)](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-Stored-(User-Agent).html)
  * [SQL Injection -Blind -Boolean-Based](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-Blind-Boolean-Based.html)
  * [SQL Injection -Blind -Time-Based](https://teckk2.github.io/web-pentesting/2018/02/07/SQL-Injection-Blind-Time-Based.html)
  * [XML/XPath Injection (Login Form)](https://teckk2.github.io/web-pentesting/2018/02/07/XML-XPath-Injection-(Login-Form).html)
  * [XML/XPath Injection (Search)](https://teckk2.github.io/web-pentesting/2018/02/07/XML-XPath-Injection-(Search).html)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>

