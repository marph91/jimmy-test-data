nmap -A target
(-O for just OS, -sV for just service)
---
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020-05-27 07:24 EDT            
Nmap scan report for 10.10.223.62                                          
Host is up (0.20s latency).                                                
Not shown: 991 closed ports                                                
PORT      STATE SERVICE            VERSION                                 
135/tcp   open  msrpc              Microsoft Windows RPC                   
139/tcp   open  netbios-ssn        Microsoft Windows netbios-ssn           
445/tcp   open  microsoft-ds       Windows 7 Professional 7601 Service Pack 1 microsoft-ds (workgroup: WORKGROUP)                                        
3389/tcp  open  ssl/ms-wbt-server?                                         
|_ssl-date: 2020-05-27T11:26:22+00:00; 0s from scanner time.               
49152/tcp open  msrpc              Microsoft Windows RPC                   
49153/tcp open  msrpc              Microsoft Windows RPC                   
49154/tcp open  msrpc              Microsoft Windows RPC                   
49158/tcp open  msrpc              Microsoft Windows RPC                   
49159/tcp open  msrpc              Microsoft Windows RPC                   
Service Info: Host: JON-PC; OS: Windows; CPE: cpe:/o:microsoft:windows     
                                                                           
Host script results:                                                       
|_clock-skew: mean: 1h14m59s, deviation: 2h30m00s, median: 0s              
|_nbstat: NetBIOS name: JON-PC, NetBIOS user: <unknown>, NetBIOS MAC: 02:e1:fb:3b:d8:b6 (unknown)                                                        
| smb-os-discovery:                                                        
|   OS: Windows 7 Professional 7601 Service Pack 1 (Windows 7 Professional 6.1)
|   OS CPE: cpe:/o:microsoft:windows_7::sp1:professional
|   Computer name: Jon-PC
|   NetBIOS computer name: JON-PC\x00
|   Workgroup: WORKGROUP\x00
|_  System time: 2020-05-27T06:26:16-05:00
| smb-security-mode: 
|   account_used: guest
|   authentication_level: user
|   challenge_response: supported
|_  message_signing: disabled (dangerous, but default)
| smb2-security-mode: 
|   2.02: 
|_    Message signing enabled but not required
| smb2-time: 
|   date: 2020-05-27T11:26:15
|_  start_date: 2020-05-27T11:23:22

Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .
Nmap done: 1 IP address (1 host up) scanned in 147.41 seconds
