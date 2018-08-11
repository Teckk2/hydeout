---
layout: post
title: WPA/WPA2-ENTERPRISE Best Practice Guide
categories:
  - Wifi Pentesting
---

<br>1)	**Policy**: – Before we start designing our network or create our corporate policy we need to make sure some key things in mind: 

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

<br>19)	**Radius Server Security**: - If your organization authentication infrastructure includes a radius server then there are some security concerns which we need to keep in mind:

<br>•	Use a strong Radius shared secret at least 16-character long.
<br>•	 Don’t use the same Radius secret for all the devices on the network, either you should set the shared secret as per devices or at minimum per group of devices.
<br>•	Ensure only the authentication type(s) being used is enabled on the Radius server to help mitigate man-in-the-middle attack.

<br>20)	**Regular security assessment for WLAN**: - We need to make sure a regular security assessment is being performed which should include regular audits of the configurations and security mechanism in WLAN. Make sure to keep up in development of WLAN authentication schemes, and replace schemes that become broken

<p Class="message">
Some Key Things to Know while Installing WPA2 Enterprise
</p>

<br>1) **WPA2-Enterprise deployment** includes installing a RADIUS server (or establishing an outsourced service), configuring access points with the encryption and RADIUS server information, configuring your operating system with the encryption and IEEE 802.1x settings, and then connecting to your secure wireless enterprise.

<br>2) **RADIUS Server Options**: - Once you decide on which of the following RADIUS server options to use, you will set it up in the corresponding EAP, AP, and user settings.
<br>a) Windows Server - If you have a Windows Server set up, you can use either the Internet Authentication Service (IAS) or the Network Policy Server (NPS).
<br>b) FreeRADIUS - This server is a free open source project and the preferred choice of advanced IT personnel. It is available for the Linux, Mac OS X, and Windows platforms.
<br>c) Outsourced Services - If you have multiple offices or lack technical IT expertise, a hosting service is a good option. Many services provide more than just RADIUS server hosting. They can also help with the setup process, do user on-boarding, and provide real-time reporting functionality. In addition, many companies offer mobile applications that make configuring mobile devices quick and painless for Apple iOS, Android, and Kindle Fire users. 

<br>3) **Enterprise Authentication and Communication**: The RADIUS Server and EAP
The standard for passing EAP over a network is IEEE 802.1x. In this authentication framework, the user who wants to be authenticated is the supplicant. The RADIUS (remote authentication dial-in user service) server doing the authentication is the authentication server, and the device at the AP, such as a laptop or smartphone, is the authenticator.
<br>**EAP Options**:
<br>Your EAP choice depends on the level of security you need and your server/client specs. Although there are more than ten EAP types, these three are the most popular:
<br>a) **PEAP (Protected EAP)** - This protocol authenticates users through the usernames and passwords they enter when connecting to the network. It is one of the easiest EAP types to implement.
<br>b) **TLS (Transport Layer Security)** - Although this EAP type requires more time to implement and maintain, TLS is very secure because both client and server validation is done with SSL (secure socket layer) certificates. Instead of connecting to the network with usernames and passwords, end-user devices or computers must have an SSL certificate file. You control the certificate authority and distribute the client certificates.
<br>c) **TTLS (Tunneled TLS)** - This version of TLS doesn't require security certificates and reduces network management time. However, because TTLS doesn't have native support in Microsoft Windows, it requires a third-party client.

<br>The steps for configuring the APs with the encryption and RADIUS server information - and for configuring your operating system with the IEEE 802.1x setting - depend on your server and client specs.

<br>4) **Create a certificate authority (CA)**, so you can issue and install a digital certificate onto the RADIUS server, which may be done as a part of the RADIUS server installation and configuration. Alternatively, you could purchase a digital certificate from a public CA, such as GoDaddy or Verisign, so you don’t have to install the server certificate on all the clients. If using EAP-TLS, you’d also create digital certificates for each end-user.

<br>5)	On the server, populate the RADIUS client database with the IP address and shared secret for each AP.

<br>6)	On the server, populate user data with usernames and passwords for each end-user.

<br>7)	On each AP, configure the security for WPA/WPA2-Enterprise and input the RADIUS server IP address and the shared secret you created for that particular AP.

<br>8)	On each Wi-Fi computer and device, configure the security for WPA/WPA2-Enterprise and set the 802.1X authentication settings.

<p Class="message">
WPA2-Enterprise Challenges
</p>

<p>The average WPA2-Enterprise network suffers from some combination of these 4 problems:</p>

<br>1) **DEVICE VARIATION**: - When IEEE created the 802.1X protocol in 2001, there were not a lot of devices that networks had to deal with in regards to wireless access. Since then, the number of device manufacturers has exploded with the rise of mobile computing. To put it in perspective, there are more flavors of Android today than there were entire operating systems in 2001.
Support for 802.1X is inconsistent across devices, even of the same OS. And each device has unique characteristics that can make them behave unpredictably. This problem is made worse by drivers and software installed on the device.

<br>2) **MITM AND DELIVERING CERTIFICATES**: - While WPA2 sets up a very secure connection, you also have to be sure that the users will only connect to the official network. A secure connection is meaningless if it’s to a honeypot or imposter signal. Institutions often sweep for and detect rogue access points, including Man-in-the-Middle attacks, but users can still be vulnerable off-site. A person with a laptop can quietly gather user credentials at a bus stop, coffee shop, or anywhere devices might pass through and try to auto-connnect.
<br>Even if the server has a certificate properly configured, there’s no guarantee that users won’t connect to a rouge SSID and accept any certificates presented to them. The best practice is to actually install the public key on the user’s device to automatically verify the certificates presented by the server.

<br>3) **THE PASSWORD CHANGE PROBLEM**: - Networks that have set up passwords to expire on a regular basis face additional burden with WPA2-Enterprise. Each device will lose connectivity until reconfigured. This was less of a burden in eras when each user was only issued one device, but in today’s modern BYOD setting, users have multiple devices which all will want to connect to the internet. Depending on how the password changes are rolled out or the users’ abilities to manage passwords, this can be a burden on some helpdesks.
<br>It’s even worse on networks that have unexpected password changes due to data breaches or security vulnerabilities. In addition to having to roll out new credentials site-wide, IT has to deal with the influx of help desk tickets related to Wi-Fi.

<br>4) **CHANGING USER EXPECTATION**: - The hardest part about WPA2-Enterprise, by far, is training the users. Users today have incredibly high expectations for ease of use. They also have more options than ever before to work around official access. If the network is too hard to use, they’ll use data. If the certificate is bad, they will ignore it. If they can’t access something they want, they will use a proxy.
<br>For WPA2-Enterprise to work, you need to make it as easy to use as everything else users out there are used to, without sacrificing security.


<p class="message">
  ~ Hack the World and Stay Noob
</p>

[Twitter](https://twitter.com/Teck__K2) / [Hack The Box](https://www.hackthebox.eu/profile/966) / [CTF Team](https://ctftime.org/team/20102) /
[Teck_N00bs Community Telegram](https://t.me/Teck_N00bs)

<script src="https://www.hackthebox.eu/badge/966"> </script>
