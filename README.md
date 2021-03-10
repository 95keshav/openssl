# Securing Network with  OpenSSL

## What is SSL

- SSL stands for Secure Socket Layer
- Network Protocol which runs on in between presentation layer and Transport layer
- Now SSL has  successor which is  called  TLS  stands for Transport Layer Security
![image](https://raw.githubusercontent.com/95keshav/openssl/main/Figure1.%20OSI%20Layers%20and%20Protocols%20used.png)


## Why We need SSL/TLS

- SSL/TLS is used for securing connection between systems so that they can share important information and no one other can read or modify it.

- SSL/TLS basically use encryption algorithms to encrypt that data and share keys only to system who are communicating with each other
![alt text](https://raw.githubusercontent.com/95keshav/openssl/main/Figure%202.%20SSL%20Client-Server%20communication.png) <br />
[To Get more information on SSL click here](https://www.youtube.com/watch?v=iQsKdtjwtYI)

## How To Get SSL Certificate?

Its Easy, as there are many companies which sell SSL encryption certificate service.
1. [Go daady](https://ca.godaddy.com/offers/ssl-certificate/month?isc=sshl5ca18&countryview=1&currencytype=CAD&gclid=Cj0KCQiA1pyCBhCtARIsAHaY_5c0At-wdCdfLCOA5i0WMMxTheGqqBCbsLGrQLa4z-5VjQnd03dQJLsaAlPtEALw_wcB&gclsrc=aw.ds)
2. [Comodo SSl](https://comodosslstore.com/promoads/cheap-comodo-ssl-certificates.aspx?gclid=Cj0KCQiA1pyCBhCtARIsAHaY_5e4SS0meZ14zKfxrpohuZkCtUGKtH9eKy7dR2JhFINq5N28rm2yQkwaAh4ZEALw_wcB)
3. [Digicert](https://www.digicert.com/tls-ssl/compare-certificates?ef_id=Cj0KCQiA1pyCBhCtARIsAHaY_5eLOU_wn5_iGycf_FAMDTZnA3NFnWhCFkLvcjKr2sZqpop_mak2bSUaArzWEALw_wcB:G:s&s_kwcid=AL!6100!3!389968107068!e!!g!!digicert&campaignid=197469053&adgroupid=13418307173&gclid=Cj0KCQiA1pyCBhCtARIsAHaY_5eLOU_wn5_iGycf_FAMDTZnA3NFnWhCFkLvcjKr2sZqpop_mak2bSUaArzWEALw_wcB)
4. [Entrust Datacard](https://www.entrust.com/digital-security/certificate-solutions/products/digital-certificates/tls-ssl-certificates/advantage-ssl)
5. [ssl.com](https://www.ssl.com/certificates/premiumssl/)

## Various Open-Source SSL certificate Service
- All these come under open-source license.
- Can be commercially used for free
- No hidden charges
1. [OpenSSL](https://www.openssl.org/source/)
2. [Let's Crypt](https://letsencrypt.org/)
3. [zero SSL](https://zerossl.com/)
4. [Certbot](https://certbot.eff.org/)
5. [SSL for free](https://www.sslforfree.com/)


## What is OpenSSL

- It is open-source cryptographic library.
- Written  in C, Assembly and Perl
- It  is  used  for  data  encryption
- It  has  various encryption algorithm and provide many encryption tools
- SSL/TLS  is  one  of  encryption tool provided by OpenSSL <br />
[for more information click here](https://www.openssl.org/)

## History Of OpenSSL

- Released on 23 December 1998 by OpenSSL Project Team
- In  2019  OpenSSL  is  managed  by  OpenSSL  management  committee
- This project budget is around one million per year which primarily completed by donations <br />
[Get more information on wikipedia](https://en.wikipedia.org/wiki/OpenSSL)

## How OpenSSL is Work
Open SSL architecture is divided into 4 parts
1. libcrypto
2. libssl
3. Engine
4. Application Component

### Libcrypto
- It is general purpose cryptographic library which contains all various cryptographic services used in OpenSSL
- It  also  provide supporting services which are used by libssl  which  handle  SSL/TLS  in  OpenSSL
![image](https://raw.githubusercontent.com/95keshav/openssl/main/supporting%20services.png)
### Libssl
- This library depends upon libcrypto
- It handle the TLS protocols and its execution
![image](https://raw.githubusercontent.com/95keshav/openssl/main/libssl.png)

### Engine
- They are Dynamically modules registered with libcrypto to help it to run cryptographic algorithms
- It is  the  hardware and software implementations  used to run cryptographic algorithms
- Used  as  hardware accelerator for these algorithms

### Application Component
*“Applications are  set  of  command  –line tools  that  use  the  underlaying  libcrypto and libssl components to provide cryptographic and other features like*[[1]](#1)

1. *Key and parameter generation and inspection*
2.  *Certificate  generation and inspection*
3.  *SSL/TSL test  tools*
4. *ASN.1 Inspection”*


## OpenSSL Module
![image](https://raw.githubusercontent.com/95keshav/openssl/main/openssl%20modules.png) <br />
[Get more information on OpenSSL Architechture](https://www.openssl.org/docs/OpenSSLStrategicArchitecture.html)
+
## OpenSSL installation

#### on Windows

[Downloading URL](https://slproweb.com/products/Win32openssl.html)

[InstalltionTurorial](https://www.youtube.com/watch?v=jSkQ27sTto0&ab_channel=TechDeepDive)

(*Since windows version package is not available on OpenSSL website, I found an URL in third party website and check that it is virus-free via https://www.virustotal.com/*)



#### On Ubuntu

__Type commands in Ubuntu Terminal:__

~~~
$ sudo apt-get install openssl
$ sudo apt-get install libssl-dev
~~~

(libssl-dev is OpenSSL development package)



## Technical presentation on Ubuntu

#### OpenSSL Generating Keys & Encryption & Decryption in RSA algorithm



**Generating  private key**:

~~~
/tmp/Alice$ openssl genrsa -out A_private.key 2048
/tmp/Bob$ openssl genrsa -out B_private.key 2048
~~~



**Generating public key**: 

~~~
/tmp/Alice$ openssl rsa -in A_private.key -out A_public.key -pubout
/tmp/Bob$ openssl rsa -in B_private.key -out B_public.key -pubout
~~~

(*.pem is either ok to be generated and used the same function with .key*)

(*use $ openssl rsa -in A.key -text to get parameters like modulus, primes, exponents and coefficient in RSA algorithms*)



**Exchanging keys**: 

Simulating by copying or linking using  'ln -s' or commands in Ubuntu file system.

~~~
/tmp/Alice$ ln -s /tmp/Bob/B_public.key
/tmp/Bob$ ln -s /tmp/Alice/A_public.key
~~~



**Typing a Message**:

~~~
/tmp/Alice$ echo"Hi Bob! This is Alice." > A_msg
~~~



**Scenario1:**

**Encryption**:

~~~
/tmp/Alice$ openssl rsautl -encrypt -in A_msg -out ciphertext -inkey B_public.key -pubin
~~~

**Massage-passing**:

~~~
/tmp/Bob$ ln -s /tmp/Alice/ciphertext
~~~

**Decryption**: 

~~~
/tmp/Bob$  openssl rsautl -decrypt -inkey B_private.key -in ciphertext -out B_msg
~~~



**Scenario2**:

**Sign**:

~~~
/tmp/Alice$ openssl rsautl -inkey A_private.key  -sign -in msg -out A_signed_msg
~~~

**Massage-passing**:

~~~
/tmp/Bob$ ln -s /tmp/Alice/A_signed_msg
~~~

**Verify**:

~~~
/tmp/Bob$ openssl rsautl -verify -inkey A_public.key -in A_signed_msg -out B_verified_msg -pubin
~~~

Then only by using Alice’s public key can Bob decrypt the message. In this method Bob can verify that the message can only be from Alice, which is non-repudiation. 

Eve who wants to eavesdrop the messages is not introduced here, because the RSA algorithm guarantees the unbreakability from the theory of Math and CS. If the length of the private key is long enough and well kept, Eve won’t be able to decipher unless she revolutionizes mathematics or, she makes quantum computer come true. 

Thanks to the Cryptographers who created such mighty algorithms, and thanks to the engineers who contributed to open source communities like OpenSSL that made these algorithms accessible to everyone, thus making our privacy well protected. You know without their fighting, such algorithms maybe exclusive to American government and military use for many more years. That’s another story about Phil Zimmerman and crypto wars.



#### OpenSSL CSR generating

（CSR is short for Certificate Signing Request, which can be authenticated by a CA to be a Certificate）

~~~
$ openssl req -out mydomain.csr -new -newkey rsa:2048 -nodes -keyout mydomain.key
~~~

And then fill in information as requested.

<img src="C:\Users\sihang\AppData\Roaming\Typora\typora-user-images\image-20210304154146261.png" alt="image-20210304154146261"  />

（*use $ openssl req -in mydomain.csr -text to check the details of the csr file*）



### Apply OpenSSL on Windows



 [Tutorial of Encryption and Decryption in AES algorithm](https://www.youtube.com/watch?v=4lgcElJWxVM)

[Tutoroal of generating RSA keys](https://www.youtube.com/watch?v=iHb3nFtzFoc)



## References
https://www.openssl.org/docs<br />
“<a id="1">[1]</a>.” https://www.openssl.org, https://www.openssl.org/docs/OpenSSLStrategicArchitecture.html.<br />
“Figure1. OSI Layers and Protocols used.” https://thecybersecuritymancom.com, https://thecybersecuritymancom.files.wordpress.com/2017/11/84433547__web.png.<br />
“Figure 2. SSL Client-Server communication.” https://www.manageengine.com/, https://www.manageengine.com/key-manager/information-center/what-is-ssl-certificate-management.html.<br />
https://www.sciencedirect.com/topics/engineering/layered-architecture<br />
+
“<a id="1">[2]</a>.” https://www.youtube.com/watch?v=-nEh7X4dtuw&t=58s

“<a id="1">[3]</a>.” https://support.globalsign.com/ssl/ssl-certificates-installation/generate-csr-openssl

“<a id="1">[4]</a>.” https://www.digicert.com/kb/ssl-support/openssl-quick-reference-guide.htm

“<a id="1">[5]</a>.” https://en.wikipedia.org/wiki/Crypto_Wars

“<a id="1">[6]</a>.” https://en.wikipedia.org/wiki/Phil_Zimmermann

