---
layout: post
title: XML\XPath Injection (Login Form)
categories:
  - Web-Pentesting
---

<br>**XML:-**XML Injection testing is when a tester tries to inject an XML doc to the application. If the XML parser fails to contextually validate data, then the test will yield a positive result.
<br>**XPATH:-**Similar to SQL Injection, XPath Injection attacks occur when a web site uses user-supplied information to construct an XPath query for XML data. By sending intentionally malformed information into the web site, an attacker can find out how the XML data is structured, or access data that he may not normally have access to. He may even be able to elevate his privileges on the web site if the XML data is being used for authentication (such as an XML based user file).
  
  * Querying XML is done with XPath, a type of simple descriptive statement that allows the XML query to locate a piece of information. Like SQL, you can specify certain attributes to find, and patterns to match. When using XML for a web site it is common to accept some form of input on the query string to identify the content to locate and display on the page. This input must be sanitized to verify that it doesn't mess up the XPath query and return the wrong data.
  
  * XPath is a standard language; its notation/syntax is always implementation independent, which means the attack may be automated. There are no different dialects as it takes place in requests to the SQL databases. Because there is no level access control it's possible to get the entire document. We won't encounter any limitations as we may know from SQL injection attacks.

![176](https://teckk2.github.io/assets/images/Web%20Pentest/A1/176.png)
![177](https://teckk2.github.io/assets/images/Web%20Pentest/A1/177.png)
![178](https://teckk2.github.io/assets/images/Web%20Pentest/A1/178.png)
<br>**Error**
![179](https://teckk2.github.io/assets/images/Web%20Pentest/A1/179.png)
![180](https://teckk2.github.io/assets/images/Web%20Pentest/A1/180.png)

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
