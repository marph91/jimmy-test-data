nmap -A target
(-O for just OS, -sV for just service)
---
nmap -A 10.10.10.7
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020.05.29 14:43 EDT
Nmap scan report for 10.10.10.7
Host is up (0.036s latency).
Not shown: 988 closed ports
PORT      STATE SERVICE    VERSION
22/tcp    open  ssh        OpenSSH 4.3 (protocol 2.0.
| ssh-hostkey: 
|   1024 ad:ee:5a:bb:69:37:fb:27:af:b8:30:72:a0:f9:6f:53 (DSA)
|_  2048 bc:c6:73:59:13:a1:8a:4b:55:07:50:f6:65:1d:6d:0d (RSA)
25/tcp    open  smtp       Postfix smtpd
|_smtp-commands: beep.localdomain, PIPELINING, SIZE 10240000, VRFY, ETRN, ENHANCEDSTATUSCODES, 8BITMIME, DSN, 
80/tcp    open  http       Apache httpd 2.2.3
|_http-server-header: Apache/2.2.3 (CentOS)
|_http-title: Did not follow redirect to <https://10.10.10.7/>
|_https-redirect: ERROR: Script execution failed (use -d to debug)
110/tcp   open  pop3       Cyrus pop3d 2.3.7.Invoca-RPM-2.3.7.7.el5_6.4
|_pop3.capabilities: TOP USER UIDL RESP-CODES STLS AUTH-RESP-CODE IMPLEMENTATION(Cyrus POP3 server v2. APOP PIPELINING LOGIN-DELAY(0. EXPIRE(NEVER)
111/tcp   open  rpcbind    2 (RPC #100000.
143/tcp   open  imap       Cyrus imapd 2.3.7.Invoca-RPM-2.3.7.7.el5_6.4
|_imap-capabilities: LIST-SUBSCRIBED ANNOTATEMORE NO ATOMIC RENAME IMAP4 OK UIDPLUS LISTEXT ID URLAUTHA0001 STARTTLS THREAD=REFERENCES X-NETSCAPE RIGHTS=kxte IMAP4rev1 IDLE QUOTA MAILBOX-REFERRALS SORT=MODSEQ CHILDREN SORT CONDSTORE Completed MULTIAPPEND ACL THREAD=ORDEREDSUBJECT BINARY NAMESPACE LITERAL+ UNSELECT CATENATE
443/tcp   open  ssl/https?
|_ssl-date: 2020.05.29T18:48:28+00:00; +1m55s from scanner time.
993/tcp   open  ssl/imap   Cyrus imapd
|_imap-capabilities: CAPABILITY
995/tcp   open  pop3       Cyrus pop3d
3306/tcp  open  mysql      MySQL (unauthorized)
4445/tcp  open  upnotifyp?                                                                    
10000/tcp open  http       MiniServ 1.570 (Webmin httpd)                                      
|_http-title: Site doesn't have a title (text/html; Charset=iso-8859.1..                      
Service Info: Hosts:  beep.localdomain, 127.0.0.1, example.com                                
                                                                                              
Host script results:                                                                          
|_clock-skew: 1m54s                                                                           
                                                                                              
Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .
Nmap done: 1 IP address (1 host up) scanned in 349.35 seconds 
