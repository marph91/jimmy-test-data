nmap -Pn --script vuln,nmap-vulners,vulscan target
---
Starting Nmap 7.60 ( <https://nmap.org> ) at 2020.04.01 08:43 EDT
Nmap scan report for 192.168.16.129
Host is up (0.00029s latency).
Not shown: 994 closed ports
PORT     STATE SERVICE
22/tcp   open  ssh
80/tcp   open  http
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|   /test.php: Test page
|   /icons/: Potentially interesting directory w/ listing on 'apache/1.3.20'
|   /manual/: Potentially interesting directory w/ listing on 'apache/1.3.20'
|_  /usage/: Potentially interesting folder
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-trace: TRACE is enabled
111/tcp  open  rpcbind
139/tcp  open  netbios-ssn
443/tcp  open  https
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
| ssl-ccs-injection: 
|   VULNERABLE:
|   SSL/TLS MITM vulnerability (CCS Injection)
|     State: VULNERABLE
|     Risk factor: High
|       OpenSSL before 0.9.8za, 1.0.0 before 1.0.0m, and 1.0.1 before 1.0.1h
|       does not properly restrict processing of ChangeCipherSpec messages,
|       which allows man-in-the-middle attackers to trigger use of a zero
|       length master key in certain OpenSSL-to-OpenSSL communications, and
|       consequently hijack sessions or obtain sensitive information, via
|       a crafted TLS handshake, aka the "CCS Injection" vulnerability.
|           
|     References:
|       <http://www.cvedetails.com/cve/2014-0224>
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0224>
|_      <http://www.openssl.org/news/secadv_20140605.txt>
| ssl-dh-params: 
|   VULNERABLE:
|   Transport Layer Security (TLS) Protocol DHE_EXPORT Ciphers Downgrade MitM (Logjam)
|     State: VULNERABLE
|     IDs:  OSVDB:122331  CVE:CVE-2015.4000
|       The Transport Layer Security (TLS) protocol contains a flaw that is
|       triggered when handling Diffie-Hellman key exchanges defined with
|       the DHE_EXPORT cipher. This may allow a man-in-the-middle attacker
|       to downgrade the security of a TLS session to 512.bit export-grade
|       cryptography, which is significantly weaker, allowing the attacker
|       to more easily break the encryption and monitor or tamper with
|       the encrypted stream.
|     Disclosure date: 2015.5.19
|     Check results:
|       EXPORT-GRADE DH GROUP 1
|             Cipher Suite: TLS_DHE_RSA_EXPORT_WITH_DES40_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: mod_ssl 2.0.x/512.bit MODP group with safe prime modulus
|             Modulus Length: 512
|             Generator Length: 8
|             Public Key Length: 512
|     References:
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2015-4000>
|       <https://weakdh.org>
|       <http://osvdb.org/122331>
|   
|   Diffie-Hellman Key Exchange Insufficient Group Strength
|     State: VULNERABLE
|       Transport Layer Security (TLS) services that use Diffie-Hellman groups
|       of insufficient strength, especially those using one of a few commonly
|       shared groups, may be susceptible to passive eavesdropping attacks.
|     Check results:
|       WEAK DH GROUP 1
|             Cipher Suite: TLS_DHE_RSA_WITH_DES_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: mod_ssl 2.0.x/1024.bit MODP group with safe prime modulus
|             Modulus Length: 1024
|             Generator Length: 8
|             Public Key Length: 1024
|     References:
|_      <https://weakdh.org>
| ssl-poodle: 
|   VULNERABLE:
|   SSL POODLE information leak
|     State: VULNERABLE
|     IDs:  OSVDB:113251  CVE:CVE-2014.3566
|           The SSL protocol 3.0, as used in OpenSSL through 1.0.1i and other
|           products, uses nondeterministic CBC padding, which makes it easier
|           for man-in-the-middle attackers to obtain cleartext data via a
|           padding-oracle attack, aka the "POODLE" issue.
|     Disclosure date: 2014.10.14
|     Check results:
|       TLS_RSA_WITH_3DES_EDE_CBC_SHA
|     References:
|       <https://www.imperialviolet.org/2014/10/14/poodle.html>
|       <https://www.openssl.org/~bodo/ssl-poodle.pdf>
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566>
|_      <http://osvdb.org/113251>
| sslv2.drown: 
|   ciphers: 
|     SSL2_DES_64_CBC_WITH_MD5
|     SSL2_RC4_128_EXPORT40_WITH_MD5
|     SSL2_RC4_128_WITH_MD5
|     SSL2_DES_192_EDE3_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_WITH_MD5
|     SSL2_RC2_128_CBC_EXPORT40_WITH_MD5
|     SSL2_RC4_64_WITH_MD5
|   vulns: 
|     CVE-2016.0703: 
|       title: OpenSSL: Divide-and-conquer session key recovery in SSLv2
|       state: VULNERABLE
|       ids: 
|         CVE:CVE-2016.0703
|       description: 
|               The get_client_master_key function in s2_srvr.c in the SSLv2 implementation in
|       OpenSSL before 0.9.8zf, 1.0.0 before 1.0.0r, 1.0.1 before 1.0.1m, and 1.0.2 before
|       1.0.2a accepts a nonzero CLIENT-MASTER-KEY CLEAR-KEY-LENGTH value for an arbitrary
|       cipher, which allows man-in-the-middle attackers to determine the MASTER-KEY value
|       and decrypt TLS ciphertext data by leveraging a Bleichenbacher RSA padding oracle, a
|       related issue to CVE-2016.0800.
|     
|       refs: 
|         <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0703>
|         <https://www.openssl.org/news/secadv/20160301.txt>
|     CVE-2016.0800: 
|       title: OpenSSL: Cross-protocol attack on TLS using SSLv2 (DROWN)
|       state: VULNERABLE
|       ids: 
|         CVE:CVE-2016.0800
|       description: 
|               The SSLv2 protocol, as used in OpenSSL before 1.0.1s and 1.0.2 before 1.0.2g and
|       other products, requires a server to send a ServerVerify message before establishing
|       that a client possesses certain plaintext RSA data, which makes it easier for remote
|       attackers to decrypt TLS ciphertext data by leveraging a Bleichenbacher RSA padding
|       oracle, aka a "DROWN" attack.
|     
|       refs: 
|         <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2016-0800>
|_        <https://www.openssl.org/news/secadv/20160301.txt>
1024/tcp open  kdm
MAC Address: 00:0C:29:70:63:17 (VMware)

Host script results:
|_samba-vuln-cve-2012.1182: Could not negotiate a connection:SMB: ERROR: Server returned less data than it was supposed to (one or more fields are missing); aborting [14]
| smb-vuln-cve2009.3103: 
|   VULNERABLE:
|   SMBv2 exploit (CVE-2009.3103, Microsoft Security Advisory 975497.
|     State: VULNERABLE
|     IDs:  CVE:CVE-2009.3103
|           Array index error in the SMBv2 protocol implementation in srv2.sys in Microsoft Windows Vista Gold, SP1, and SP2,
|           Windows Server 2008 Gold and SP2, and Windows 7 RC allows remote attackers to execute arbitrary code or cause a
|           denial of service (system crash) via an & (ampersand) character in a Process ID High header field in a NEGOTIATE
|           PROTOCOL REQUEST packet, which triggers an attempted dereference of an out-of-bounds memory location,
|           aka "SMBv2 Negotiation Vulnerability."
|           
|     Disclosure date: 2009.09.08
|     References:
|       <http://www.cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2009-3103>
|_      <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2009-3103>
|_smb-vuln-ms10.054: false
|_smb-vuln-ms10.061: Could not negotiate a connection:SMB: ERROR: Server returned less data than it was supposed to (one or more fields are missing); aborting [14]
