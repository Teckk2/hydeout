---
layout: post
tittle: OSCP Tools and commands
---


**Nmap scan**
  * nmap -Pn -T2 -sV –randomize-hosts IP1,IP2
  * nmap –script smb-check-vulns.nse -p445 target (using NSE scripts)
  * nmap -sU -P0 -T Aggressive -p123 target (Aggresive Scan T1-T5)
  * nmap -sA -PN -sN target
  * nmap -sS -sV -T5 -F -A -O target (version detection)
  * nmap -sU -v (IP) (Udp)
  * nmap -sU -P0 (Udp)
  * nmap -sC (IP) (all scan default)
