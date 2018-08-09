---
layout: post
title: WPA/WPA2-ENTERPRISE Best Practice Guide
categories:
  - Wifi Pentesting
---

<br>1)	**Policy**: – Before we start designing our network or create our corporate policy we need to make sure some key things in mind: -
<br>   •	Policies on using WLAN: - First we need to outline appropriate and inappropriate use of WLAN environment and possible outcome for noncompliance. We also need to have an End-User agreement which user should sign and agree upon all the policies for wireless use. And we have to create and mention all the policies like what services a user is permitted to do, Policies on (VPN) and Hot-spot use of the internet access.
<br>  * **Policies on using WLAN**: - First we need to outline appropriate and inappropriate use of WLAN environment and possible outcome for noncompliance. We also need to have an End-User agreement which user should sign and agree upon all the policies for wireless use. And we have to create and mention all the policies like what services a user is permitted to do, Policies on (VPN) and Hot-spot use of the internet access.
<br>  * **Authorized WLAN installation from different Source**: - In the Policy we need to mention that which part of the organization is authorized to provide WLAN service in the vicinity.
This will help organization from rouge access point, For Example:  Take a scenario The organization is spread in 3 building blocks A, B and C in which A, B is well connected to the WLAN network, but C is not connected to WLAN access because of some restriction, so if one user of A or B have some work in building C of the organization, and as there is no WLAN access, he may try to host a rouge WLAN access pointing towards C by creating a Hot-Spot and use the same WLAN access in building C also bypassing all the restriction. So we should also mention this in the Policy that If a user found with such activity or a (Rouge AP) Device, then the particular Organization have full Right to Seize such device in their premises. 
<br>  * **Allowed Hardware**: - If the organization require some specific sort of hardware then it should be mentioned in the Policy, and it is also advised not to use personally owned hardware.
<br>  **Wireless IDS**: - We need to create a Document for deploying wireless IDS to monitor the organization WLAN Environment. Even the organization don’t have a WLAN Environments they still supposed to have a Policy regarding this, so they can ensure no user can start providing its own WLAN access, The Policy should also provide the organization an official backing while removing unauthorized access points.
