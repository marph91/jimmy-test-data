nmap -Pn --script vuln,nmap-vulners,vulscan target
---
sudo nmap -Pn --script vuln 10.10.10.7                    
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020.05.29 14:56 EDT                               
Nmap scan report for target (10.10.10.7.                                                      
Host is up (0.035s latency).                                                                  
Not shown: 988 closed ports                                                                   
PORT      STATE SERVICE                                                                       
22/tcp    open  ssh
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
25/tcp    open  smtp
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
| smtp-vuln-cve2010.4344: 
|_  The SMTP server is not Exim: NOT VULNERABLE
|_sslv2.drown: 
80/tcp    open  http
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-enum: 
|_  /icons/: Potentially interesting directory w/ listing on 'apache/2.2.3 (centos)'
|_http-passwd: ERROR: Script execution failed (use -d to debug)
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007.6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009.09.17
|     References:
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750>
|_      <http://ha.ckers.org/slowloris/>
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-trace: TRACE is enabled
110/tcp   open  pop3
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_sslv2.drown: 
111/tcp   open  rpcbind
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
143/tcp   open  imap
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_sslv2.drown: 
443/tcp   open  https
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_http-aspnet-debug: ERROR: Script execution failed (use -d to debug)
|_http-csrf: Couldn't find any CSRF vulnerabilities.
|_http-dombased-xss: Couldn't find any DOM based XSS.
| http-slowloris-check: 
|   VULNERABLE:
|   Slowloris DOS attack
|     State: LIKELY VULNERABLE
|     IDs:  CVE:CVE-2007.6750
|       Slowloris tries to keep many connections to the target web server open and hold
|       them open as long as possible.  It accomplishes this by opening connections to
|       the target web server and sending a partial request. By doing so, it starves
|       the http server's resources causing Denial Of Service.
|       
|     Disclosure date: 2009.09.17
|     References:
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2007-6750>
|_      <http://ha.ckers.org/slowloris/>
|_http-stored-xss: Couldn't find any stored XSS vulnerabilities.
|_http-vuln-cve2014.3704: ERROR: Script execution failed (use -d to debug)
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
|       <http://www.openssl.org/news/secadv_20140605.txt>
|_      <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0224>
| ssl-dh-params: 
|   VULNERABLE:
|   Diffie-Hellman Key Exchange Insufficient Group Strength
|     State: VULNERABLE
|       Transport Layer Security (TLS) services that use Diffie-Hellman groups
|       of insufficient strength, especially those using one of a few commonly
|       shared groups, may be susceptible to passive eavesdropping attacks.
|     Check results:
|       WEAK DH GROUP 1
|             Cipher Suite: TLS_DHE_RSA_WITH_DES_CBC_SHA
|             Modulus Type: Safe prime
|             Modulus Source: mod_ssl 2.2.x/1024.bit MODP group with safe prime modulus
|             Modulus Length: 1024
|             Generator Length: 8
|             Public Key Length: 1024
|     References:
|_      <https://weakdh.org>
| ssl-poodle: 
|   VULNERABLE:
|   SSL POODLE information leak
|     State: VULNERABLE
|     IDs:  BID:70574  CVE:CVE-2014.3566
|           The SSL protocol 3.0, as used in OpenSSL through 1.0.1i and other
|           products, uses nondeterministic CBC padding, which makes it easier
|           for man-in-the-middle attackers to obtain cleartext data via a
|           padding-oracle attack, aka the "POODLE" issue.
|     Disclosure date: 2014.10.14
|     Check results:
|       TLS_RSA_WITH_AES_128_CBC_SHA
|     References:
|       <https://www.openssl.org/~bodo/ssl-poodle.pdf>
|       <https://www.imperialviolet.org/2014/10/14/poodle.html>
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566>
|_      <https://www.securityfocus.com/bid/70574>
|_sslv2.drown: 
993/tcp   open  imaps
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_ssl-ccs-injection: No reply from server (TIMEOUT)
|_sslv2.drown: 
995/tcp   open  pop3s
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_ssl-ccs-injection: No reply from server (TIMEOUT)
|_sslv2.drown: 
3306/tcp  open  mysql
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
|_mysql-vuln-cve2012.2122: ERROR: Script execution failed (use -d to debug)
4445/tcp  open  upnotifyp
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
10000/tcp open  snet-sensor-mgmt
|_clamav-exec: ERROR: Script execution failed (use -d to debug)
| http-vuln-cve2006.3392: 
|   VULNERABLE:
|   Webmin File Disclosure
|     State: VULNERABLE (Exploitable)
|     IDs:  CVE:CVE-2006.3392
|       Webmin before 1.290 and Usermin before 1.220 calls the simplify_path function before decoding HTML.
|       This allows arbitrary files to be read, without requiring authentication, using "..%01" sequences
|       to bypass the removal of "../" directory traversal sequences.
|       
|     Disclosure date: 2006.06.29
|     References:
|       <http://www.rapid7.com/db/modules/auxiliary/admin/webmin/file_disclosure>
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2006-3392>
|_      <http://www.exploit-db.com/exploits/1997/>
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
|       <http://www.openssl.org/news/secadv_20140605.txt>
|_      <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-0224>
| ssl-poodle: 
|   VULNERABLE:
|   SSL POODLE information leak
|     State: VULNERABLE
|     IDs:  BID:70574  CVE:CVE-2014.3566
|           The SSL protocol 3.0, as used in OpenSSL through 1.0.1i and other
|           products, uses nondeterministic CBC padding, which makes it easier
|           for man-in-the-middle attackers to obtain cleartext data via a
|           padding-oracle attack, aka the "POODLE" issue.
|     Disclosure date: 2014.10.14
|     Check results:
|       TLS_RSA_WITH_AES_128_CBC_SHA
|     References:
|       <https://www.openssl.org/~bodo/ssl-poodle.pdf>
|       <https://www.imperialviolet.org/2014/10/14/poodle.html>
|       <https://cve.mitre.org/cgi-bin/cvename.cgi?name=CVE-2014-3566>
|_      <https://www.securityfocus.com/bid/70574>
|_sslv2.drown: ERROR: Script execution failed (use -d to debug)

Nmap done: 1 IP address (1 host up) scanned in 441.86 seconds
