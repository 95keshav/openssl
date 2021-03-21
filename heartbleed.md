# Heartbleed Exploit on OpenSSL  (CVE 2014-0160)

## What is Heartbleed Exploit
### Why is this exploit called Heartbleed?

* It is named after the extension protocol which SSL/TLS protocols used called Heartbeat Extension

* While TLS handshaking it sends packet called heartbeat packet to another system to keep TLS connection up every time so that it save time that initialization of TLS take. It sends it multiple time nonstop.

### Why It Happens?

* There is programming mistake in OpenSSL Library called libssl which handles the execution of SSL/TSL protocol

### How Big it is?

* OpenSSL is mostly used by opensource webservers like Apache and nginx. So combined market share of just these on inter is 66% as per [Netcraft's April 2014 Web Server Survey](https://news.netcraft.com/archives/2014/04/02/april-2014-web-server-survey.html)[1]

### Who found it?

* It was found by group of security engineers while working on SafeGuard feature in Codenomicon's Defensics [security testing tools](https://www.synopsys.com/software-integrity/security-testing.html) [2]

* They reported this bug to NCSC-FI(National Cyber Security Center Finland) to take further action and tell OpenSSL

* 3rd of April 2014, [NCSC-FI](https://www.kyberturvallisuuskeskus.fi/en) [3] took up the task of verifying it, analyzing it further and reaching out to the authors of OpenSSL, software, operating system and appliance vendors, which were potentially affected.

### What versions are affected?

* Bug was introduced to OpenSSL in December 2011 and has been out in the wild since

* OpenSSL release 1.0.1 on 14th of March 2012.

### Is it is Solved Now?

* OpenSSL 1.0.1g released on 7th of April 2014 fixes the bug

## How Heartbleed Exploit  Works

* Normally the system sends the heatbeat extension packet of 65536 bytes with some payload to another system to keep TLS connection active . In return another system send back same payload with some padding. This packet goes to and fro multiple time just to keep TSL active to save time taken by TLS to initialise so that fast communication can be done.
![alt text](https://raw.githubusercontent.com/95keshav/openssl/main/Figure%202.%20SSL%20Client-Server%20communication.png)
* But there is flow in the code of OpenSSL it does not check the lenght of packet.
* Hackers use this flow to exploit the packet, They send packet with just 1 byte of data and keep other bytes empty, System do not confirm the lenght and save it in memory. When System sends back response it does not know that packet size was only of 1 byte. and it copy 65536 bytes from memory and sent back to hacker
* That data from memroy may contain SSL private keys, User credentials, System Memory address.
[To Get more information on Heartbleed click here](https://www.youtube.com/watch?v=WgrBrPW_Zn4)

## What Data is being leaked?
* Data being leaked comes under 4 categories

	1. Primary Key material

		* Encryption keys

	2. Secondary Key  material

		* Username and  Password

	3. Protected content

		* Financial Data

		* Private Communication e.g. email

		* Documents worth protected

	4. Collateral

		* Leaked  Memory  Content

		* Memory Addresses

		* Security measures  used  e.g. canaries used for overflow



## Affects of Heartbleed Exploit
1. [Millions of Vulnerable Systems Unpatched for Severe Bugs Including BlueKeep and Heartbleed Despite NSA Warnings](https://www.cpomagazine.com/cyber-security/millions-of-vulnerable-systems-unpatched-for-severe-bugs-including-bluekeep-and-heartbleed-despite-nsa-warnings/)
2. [Heartbleed bug crisis hit more government computers than previously disclosed](https://www.cbc.ca/news/politics/heartbleed-bug-cyberattack-canada-government-departments-1.3355993)
3. [900 SINs stolen due to Heartbleed bug: Canada Revenue Agency](https://globalnews.ca/news/1269168/900-sin-numbers-stolen-due-to-heartbleed-bug-canada-revenue-agency/)
4. [Devastating Heartbleed Flaw Was Used in Hospital Hack](https://time.com/3148773/report-devastating-heartbleed-flaw-was-used-in-hospital-hack/)
5. [Heartbleed](https://heartbleed.com/)
