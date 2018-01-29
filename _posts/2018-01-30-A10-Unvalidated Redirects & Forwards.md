---
layout: post
title: (OWASP) A10-Unvalidated Redirects & Forwards
categories:
  - Web-Pentesting
---

<p>We can Consider this vulnerabilty as anyone who can trick your users into submitting a request to your website. Any website or other HTML feed that your users use could do this.
Attacker links to unvalidated redirect and tricks victims into clicking it. Victims are more likely to click on it, since the link is to a valid site. Attacker targets unsafe forward to bypass security checks.</p>
<br>Applications frequently redirect users to other pages, or use internal forwards in a similar manner. Sometimes the target page is specified in an unvalidated parameter, allowing attackers to choose the destination page.
Detecting unchecked redirects is easy. Look for redirects where you can set the full URL. Unchecked forwards are harder, because they target internal pages.

<p Class="message">
  <font color="Black">Question 1</font> – What is Unvalidated Redirects & forwards?
</p>
<br>**Ans**:- 

*	A situation where a user can central which site you are redirected to by altering a user supplied parameter.
*	In this, the redirect URL parameter is not validated & the user will be redirected to another site.

<p Class="message">
  <font color="Black">Question 2</font> – How to prevent yourself from this Vulnerability?
</p>
<br>**Ans**:- 

*	If you can avoid using redirects based on user parameters, this is the best method to use.
*	If you must use redirects, avoid using any user-supplied data to determine the redirect.
*	Create a Function to Verify the Target URL & Verify that the user does in fact need to be redirected.

<h1 Class="message">
  DEMO - Comming Soon!
</h1>

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script> 
