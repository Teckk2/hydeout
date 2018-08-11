---
layout: post
title: WPA/WPA2-ENTERPRISE Best Practice Guide
categories:
  - Wifi Pentesting
---

<br>1)	**Policy**: – Before we start designing our network or create our corporate policy we need to make sure some key things in mind: -
<br>•	**Policies on using WLAN**: - First we need to outline appropriate and inappropriate use of WLAN environment and possible outcome for noncompliance. We also need to have an End-User agreement which user should sign and agree upon all the policies for wireless use. And we have to create and mention all the policies like what services a user is permitted to do, Policies on (VPN) and Hot-spot use of the internet access.
<br>•	**Authorized WLAN installation from different Source**: - In the Policy we need to mention that which part of the organization is authorized to provide WLAN service in the vicinity.
<br>This will help organization from rouge access point, For Example:  Take a scenario The organization is spread in 3 building blocks A, B and C in which A, B is well connected to the WLAN network, but C is not connected to WLAN access because of some restriction, so if one user of A or B have some work in building C of the organization, and as there is no WLAN access, he may try to host a rouge WLAN access pointing towards C by creating a Hot-Spot and use the same WLAN access in building C also bypassing all the restriction. 
<br>So we should also mention this in the Policy that If a user found with such activity or a (Rouge AP) Device, then the particular Organization have full Right to Seize such device in their premises. 
<br>•	**Allowed Hardware**: - If the organization require some specific sort of hardware then it should be mentioned in the Policy, and it is also advised not to use personally owned hardware.
<br>•	**Wireless IDS**: - We need to create a Document for deploying wireless IDS to monitor the organization WLAN Environment. Even the organization don’t have a WLAN Environments they still supposed to have a Policy regarding this, so they can ensure no user can start providing its own WLAN access, The Policy should also provide the organization an official backing while removing unauthorized access points.
<br>.
<br>2) **WLAN Architecture Design**: - While deploying WLAN Enterprise we have to look for overall architecture which includes creating standardization for hardware and configuration for WLAN if it is being deployed in multiple sites. And we can also allow components like authentication server to reuse from WLAN back-end.
<br>We also need to consider some Key things while designing WLAN Architecture: -
<br>•	What is the best place to deploy the WLAN in an organization, In regards to connectivity?
<br>•	Should we deploy WLAN in an internal network backbone, or in the DMZ or should it be deployed in a non-sensitive area only?
<br>•	Should we allow a VPN Connection to perform over 802.11?
<p>These are some key things to consider for an organization which need to be consider before deploying a WLAN Environment, As the Answer will change for Such Scenarios as Every Organization have different set of tolerance, budget, support capability and regulatory requirements.</p>
<p>The Next step while creating the WLAN Architecture we should also consider some More things which will help us securing the WLAN Environment
<br>•	What Authentication and Encryption method should we use? This also depends upon organization and local requirements, but we should document all these which will help us reusing the components while installing the multiple WLAN in future, especially the backend authentication servers.
<br>•	We should also determine and give access to only few people to access and maintain the Access Point not only virtually but Physically or Hardware of WLAN Environment. And we also need to make sure the physical security of Access Point and also securing its wiring closets or the place where the access point is mounted.
<br>•	To ensure additional security and a choke point between the WLAN and the Enterprise LAN backbone, we should consider and design the WLAN Architecture in such a way that the Wireless network should be separated from the LAN through the use of Segmentation devices.
<br>•	The organization should also consider on allowing the clients on using VPN over WLAN or not. It again depends upon organization to organization demands, requirements and their needs, if they allow using VPN over WLAN then for additional security which should they use
<br>o	VPN concentrator or 
<br>o	Enterprise Encryption Gateway.</p>

<br>3) **Configuration Management System**: - While designing the WLAN architecture we also need to make sure to deploy a system for Configuration management and that should be used for changing any configuration on the Access Point. A Document should be created to test and record all changes to use it in future for fault isolation.
The organization should also test the AP configuration periodically against the configuration recorded in the configuration management system to detect unauthorized modifications.
<br>.
<br>4) **Performing Proper site survey**: - The organization need to make sure a proper site survey is performed before deploying a WLAN Environment which includes:
<br>•	Placement of Access points which is important while providing adequate data rate to associated clients which may also cause a lot of signal to spread beyond the boundary of the building itself. They should also look for the opportunity to shape the RF (Radio Frequency) footprint by controlling the power level and using of directional antenna to minimize the RF in areas outside the physical control of the organization.
<br>•	This is also an ideal time to take plan for security concerns while the time you are placing your Access point, Identify the location for placing Wireless IDS sensors. Even if you are not planning to deploy a wireless IDS now, you can save time and money later by doing some of the planning now.

<br>5) **End User Training**: - To ensure the security to the max End user training is really important in which they should learn and trained about:
<p>•	How to use all security feature of the Enterprise WLAN
<br>•	They need to be trained about proper and improper use of the Enterprise wireless network they are using.
<br>The Training course should also specify the Corporate Policy which can be reinforced if needed on use of Hot Spots and personal wireless network in the Organization vicinity.</p>

<br>6) **Security of all WLAN Clients**: - The Organization is liable to ensure the security of all its WLAN Clients, to make sure they can follow these things:
<p>•	Proper patch level should be maintained.
<br>•	An Anti-Virus client needs to be installed, running, and regularly updated.
<br>•	Make sure a personal firewall is installed and active on the wireless connection.
<br>•	Make sure an appropriate system security settings are in place.
<br>•	Make sure that the supplicant does not have the setting “Validate server certificate” disabled. If this is disabled, you can lose all of the security of the connection as any certificate presented can be trusted.</p>

<br>7) **Strong Authentication and Encryption on WLAN**: - The organization should need to ensure a strong authentication and Encryption method on their WLAN, because this is the topic which attracts most of the attention while talking about Wireless Technology. 
While planning the Wireless Network this is the most important decision an organization network team make to choose between different encryption and authentication schemes.
<p>This Checklist cannot cover all the issues involved in selection of an appropriate mechanism for your enterprise since every enterprise has unique requirements, but in this will try to raise some of the main issues you need to consider in your selection process.</p>

<p>Make sure to use the strongest encryption practical, 128 bits should be considered
the minimum acceptable level.
<br>• Make Use of AES encryption with WPA2 if possible.
<br>• Make sure to Select a mechanism that uses centralized authentication.
<br>• Make sure to Select a mechanism that supports PKI certificates if you have the
infrastructure to support it.
<br>• If you are using EAP look to your vendors to comply with RFC3748
which obsoletes RFC2284. RFC3748 calls for binding the inner and
outer authentication protocols to help mitigate Man-in-the-middle
attacks.
<br>• Make Use of a scheme that allows for mutual authentication if possible.
<br>• Assume that WEP provides no real protection, and should not be use or only use it as a last resort.
<br>• Try to Avoid using authentication protocols that have been broken.</p>

<br>8) **Default Password**: - This is the Most common security practice which all System/Network Admin should follow, All the access point in the market comes with default password setup by the manufacturer, it should be changed ASAP or while deploying the environment, because default password is already known to the attacker or can be easily searched on the Internet depending on the Manufacturer company, which can lead to a complete compromise of the network.

<br>9) **Default Configuration Setting**: - This is another common security practice which all Admins should follow, All Access Point in the market comes with preconfigured default setting for SSID and the administrative password. This is well known to the attacker and can’t be ignored and should be changed before connecting to any APs to your production Network. Or it could lead to Complete compromise of the Network.  

<br>10)	**Configure device on Non-Production network**: - Before Deploying the WLAN components it is a good practice to configure it on an Isolated Configuration LAN because of the well-known default settings. This could reduce the risk in the case of an attack, the attacker can try to exploit its default configuration, and even if the attacker could succeed he will not get access to anything critical.

<br>11)	**Disable all unused management interface**: - All access point with enterprise class comes with multiple management interface. So any interface which is not being used actively should be disabled or it could lead to prime origin of attack.

<br>12)	**Manage the APs Out-of-band if possible**: – Access Point should be managed by using out-of-band or a separate VLAN, which could further protect the management interface from attack. 

<br>13)	**Construction of SSID**: - While creating the SSID for the WLAN network there is some key things to know: 
<br>•	We should not use the name of the company, the address, phone number in the SSID.
<br>•	We should stick to the things what will not giveaway excess information about whose WLAN the SSID is from. Like “Room 212” is a reasonable SSID as it is not giving too much information.
<br>•	SSID should not be like “Account Department” as this is not a good choice as it’s telling anyone in the range that exactly what network it is connecting to.
<br>•	Also avoid using the name of the individuals as this information could lead to a social engineering attack.
<br>•	Not broadcasting the SSID is not a full proof security measure because an attacker can still obtain the SSID easily using toll like Airodum-ng, etc...
<br>•	So it is good to keep the SSID something that you do not mind the attacker to know.

<br>14)	**Do no broadcast the SSID**: - Not broadcasting the SSID is not a full proof measure, but cut down the risk on availability of the information. It is a good idea to not broadcast your SSID information and simply configure your corporate clients with the correct information in their profile.

<br>15)	**Monitoring and Logging**: -  
<br>•	Most of the enterprise level network have mechanism in place for both remote logging and for monitoring of the network device already. 
<br>•	These may be the same tool, as with a SNMP manager or it may be separate solutions for logging to a syslog server and monitoring health with a SNMP manager
<br>•	In regards to WLAN, some sort of answer for both requirement is important.
<br>•	Monitoring health of WLAN in real time can alert you to the problems that is happening.
<br>•	But being able to refer to logs of past events is often needed to diagnose issues such as persistent authentication failures.

<br>16)	**Wireless (IDS/IPS)**: - There are few Enterprise network which are working without an IDS/IPS for security monitoring. On the other hand, many organizations have deployed some form of IDS(WIDS) or IPS(WIPS) solution to ensure the safety of RF environment for their enterprise class WLAN environment.
We can deploy WIDS solution in two methods:

<br>•	The Overlay network- Dedicated WIDS sensors needs to deploy that should be separate from the wireless LAN. These sensors will send alert back message to a central manager for event de-duplication and alerting.
<br>•	The Integrated Solution- The integrated solution uses the AP’s
themselves as sensors, this saves the cost of a separate sensor network
deployment and generally uses the same management interface as the
WLAN management application to monitor security. 
<br>  * There are a whole range of variable features within these deployment options. 
<br>  * These include IPS capabilities, Policy based station/AP suppression,
Performance monitoring, and security monitoring.
<br>  * Each deployment mode has its own strengths and weaknesses, all of which need to be given careful consideration as part of the evaluation process to ensure the system you select most fully meets your needs.

<br>17)	**Institute a Session timeout**: - We need to set a reasonable session timeout, to help and mitigate the risk of abandoned authenticated session being hijacked.

<br>18)	**Isolation of Wireless Clients**: - Wireless client isolation should be enable, until unless there is a valid business reason to allow wireless station to communicate directly to one another.




