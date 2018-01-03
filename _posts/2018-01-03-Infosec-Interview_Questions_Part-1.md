---
layout: post
title: InfoSec Interview Questions (Part-1)
categories:
  - Misc
---

<p>This Post is all about Topics/Question which we had or could face in the Interview, This may not be the perfect but I tried to allign all the important Topic in this.</p>
<br>Speacial Thanx to my friend [Ajay](https://twitter.com/ajaysingri) for hellping me find these question.

<p Class="message">
  <font color="Black">Question 1</font> – What is CSRF ?
</p>
<br>**Ans**:- Cross site request forgery (CSRF), also known as XSRF, Sea Surf or Session Riding, is an attack vector that tricks a web browser into executing an unwanted action in an application to which a user is logged in.
<br>A successful CSRF attack can be devastating for both the business and user. It can result in damaged client relationships, unauthorized fund transfers, changed passwords and data theft—including stolen session cookies.

<p Class="message">
  <font color="Black">Question 2</font> – what is OWASP TOP 10 ?
</p>
<br>**Ans**:- The OWASP Top 10 is a powerful awareness document for web application security. It represents a broad consensus about the most critical security risks to web applications. Project members include a variety of security experts from around the world who have shared their expertise to produce this list.

<br>The current OWASP top is 2017 version which includes :-
  *	A1:2017-Injection
  *	A2:2017-Broken Authentication
  *	A3:2017-Sensitive Data Exposure
  *	A4:2017-XML External Entities (XXE) [NEW]
  *	A5:2017-Broken Access Control [Merged]
  *	A6:2017-Security Misconfiguration
  *	A7:2017-Cross-Site Scripting (XSS)
  *	A8:2017-Insecure Deserialization [NEW, Community]
  *	A9:2017-Using Components with Known Vulnerabilities
  *	A10:2017-Insufficient_Logging&Monitoring [NEW, Community]
  
<p Class="message">
  <font color="Black">Question 3</font> – Difference between OWASP Top 10 2013 and 2017 ?
</p>
<br>**Ans**:- ![owasp](https://teckk2.github.io/assets/images/owasp%20top%2010.PNG)
  
  * The Vulnerability A4 (Insecure Direct Object Reference) and A7 (Missing Function Level Access Control) in the 2013 list have been merged into single vulnerability A5 (Broken Access Control) of 2017. 
  * The vulnerability A10 (Unvalidated Redirects and Forwards) from 2013, has been dropped out in the new list of 2017.
  * The Three new vulnerabilities which has been added in the new list are :- 
    * A4 (XML External Entities {XXE})
    * A8 (Insecure Deserialization)
    * A10 (Insufficient_Logging&Monitoring) 

<p Class="message">
  <font color="Black">Question 4</font> – What is Cross site Flashing ?
</p>
<br>**Ans**:- 

* Cross Site Flashing similar to Cross Site Scripting.
* Cross Site Flashing is an incredibly common vulnerability. It occurs due to the presence of flash content embedded inside a Web Application which tries to load flash content from another domain based on user’s input without any validation.
* Through this vulnerability the attacker may able to change the user interface of a web application to trick the user into providing his sensitive details.
* The attacker can leverage the fact that his flash content would run with similar privilege as that of the legitimate flash content on the vulnerable web application only if the application is vulnerable to cross site flashing.
* The attacker can also exploit to bypass access controls and perform harmful actions like stealing confidential data, installing malware, etc.
* This attack can also be used as an ‘enabler’ vulnerability to execute Cross-Site Scripting or Clickjacking attacks on the Web application.

<p Class="message">
  <font color="Black">Question 5</font> – What is (XXE) ?
</p>
<br>**Ans**:- An XML External Entity attack is a type of attack against an application that parses XML input. This attack occurs when XML input containing a reference to an external entity is processed by a weakly configured XML parser. This attack may lead to the disclosure of confidential data, denial of service, server side request forgery, port scanning from the perspective of the machine where the parser is located, and other system impacts.

<p Class="message">
  <font color="Black">Question 6</font> – How SQLi can lead to Remote Code Execution?
</p>
<br>**Ans**:- Well SQL has a built in function to write a file for example:- in mysql using which You can save SQL results into an output of your choosing. So, lets say, 1 quote union select 2, and then we are going to type in a php string which we want to write into a file, using the output file mysql function, which we can then hopefully have the apache/php server execute for us. Lets just write this to /tmp/teck.php for now.
<p>/blog.php?id=1' UNION select 2, "&lt;?php system($_REQUEST['cmd']); ?>" INTO OUTFILE '/tmp/teck.php</p>
<br>As you can see down here, the mysql server happily executed our command. Lets just quickly take a look at the file. Okay, so what about if we had an uploads directory on our blog to allow users to upload pictures or something. Maybe we do not have the most secure permissions because we do not know any better. Lets create an uploads directory under /var/www/html/ and make it world writable. So, lets try and write our php file using the SQL injection vulnerability into /var/www/html/uploads/.
<p>/blog.php?id=1' UNION select 2, "&lt;?php system($_REQUEST['cmd']); ?>" INTO OUTFILE '/var/www/html/uploads/teck.php</p>
<br>Looks like it worked! Our SQL statement, took the php code we provided, and wrote it into a file. Lets head over to the uploads directory and have a look. Our files exists and works. Lets try and run a couple commands, like ls -l / for example, or what about the id command, as you can see we are running commands as the apache user now.
<p>http://localhost:8080/uploads/c.php?cmd=ls -l /</p>
