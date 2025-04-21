enum4linux -v target
---
[V] Dependent program "nmblookup" found in /usr/bin/nmblookup
[V] Dependent program "net" found in /usr/bin/net
[V] Dependent program "rpcclient" found in /usr/bin/rpcclient
[V] Dependent program "smbclient" found in /usr/bin/smbclient
[V] Dependent program "polenum" found in /usr/bin/polenum
[V] Dependent program "ldapsearch" found in /usr/bin/ldapsearch
Starting enum4linux v0.8.9 ( <http://labs.portcullis.co.uk/application/enum4linux/> ) on Wed Apr 22 11:52:23 2020

 ========================== 
|    Target Information    |
 ========================== 
Target ........... kioptrix1
RID Range ........ 500-550,1000-1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ================================================= 
|    Enumerating Workgroup/Domain on kioptrix1    |
 ================================================= 
[V] Attempting to get domain name with command: nmblookup -A 'kioptrix1'
[+] Got domain/workgroup name: MYGROUP

 ========================================= 
|    Nbtstat Information for kioptrix1    |
 ========================================= 
Looking up status of 192.168.16.129
	KIOPTRIX        <00> -         B <ACTIVE>  Workstation Service
	KIOPTRIX        <03> -         B <ACTIVE>  Messenger Service
	KIOPTRIX        <20> -         B <ACTIVE>  File Server Service
	..__MSBROWSE__. <01> - <GROUP> B <ACTIVE>  Master Browser
	MYGROUP         <00> - <GROUP> B <ACTIVE>  Domain/Workgroup Name
	MYGROUP         <1d> -         B <ACTIVE>  Master Browser
	MYGROUP         <1e> - <GROUP> B <ACTIVE>  Browser Service Elections

	MAC Address = 00-00-00-00-00-00

 ================================== 
|    Session Check on kioptrix1    |
 ================================== 
[V] Attempting to make null session using command: smbclient -W 'MYGROUP' //'kioptrix1'/ipc$ -U''%'' -c 'help' 2>&1
[+] Server kioptrix1 allows sessions using username '', password ''

 ======================================== 
|    Getting domain SID for kioptrix1    |
 ======================================== 
[V] Attempting to get domain SID with command: rpcclient -W 'MYGROUP' -U''%'' kioptrix1 -c 'lsaquery' 2>&1
Domain Name: MYGROUP
Domain Sid: (NULL SID)
[+] Can't determine if host is part of domain or part of a workgroup

 =================================== 
|    OS information on kioptrix1    |
 =================================== 
[V] Attempting to get OS info with command: smbclient -W 'MYGROUP' //'kioptrix1'/ipc$ -U''%'' -c 'q' 2>&1
[+] Got OS info for kioptrix1 from smbclient: Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.1a]
[V] Attempting to get OS info with command: rpcclient -W 'MYGROUP' -U''%'' -c 'srvinfo' 'kioptrix1' 2>&1
[+] Got OS info for kioptrix1 from srvinfo:
	KIOPTRIX       Wk Sv PrQ Unx NT SNT Samba Server
	platform_id     :	500
	os version      :	4.5
	server type     :	0x9a03

 ========================== 
|    Users on kioptrix1    |
 ========================== 
[V] Attempting to get userlist with command: rpcclient -W 'MYGROUP' -c querydispinfo -U''%'' 'kioptrix1' 2>&1
Use of uninitialized value $users in print at ./enum4linux.pl line 874.
Use of uninitialized value $users in pattern match (m//) at ./enum4linux.pl line 877.

[V] Attempting to get userlist with command: rpcclient -W 'MYGROUP' -c enumdomusers -U''%'' 'kioptrix1' 2>&1
Use of uninitialized value $users in print at ./enum4linux.pl line 888.
Use of uninitialized value $users in pattern match (m//) at ./enum4linux.pl line 890.

 ====================================== 
|    Share Enumeration on kioptrix1    |
 ====================================== 
[V] Attempting to get share list using authentication
WARNING: The "syslog" option is deprecated
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.1a]
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.1a]

	Sharename       Type      Comment
	---------       ----      -------
	IPC$            IPC       IPC Service (Samba Server)
	ADMIN$          IPC       IPC Service (Samba Server)

	Server               Comment
	---------            -------
	KIOPTRIX             Samba Server

	Workgroup            Master
	---------            -------
	MYGROUP              KIOPTRIX

[+] Attempting to map shares on kioptrix1
[V] Attempting map to share //kioptrix1/IPC$ with command: smbclient -W 'MYGROUP' //'kioptrix1'/'IPC$' -U''%'' -c dir 2>&1
//kioptrix1/IPC$	[E] Can't understand response:
WARNING: The "syslog" option is deprecated
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.1a]
NT_STATUS_NETWORK_ACCESS_DENIED listing \*
[V] Attempting map to share //kioptrix1/ADMIN$ with command: smbclient -W 'MYGROUP' //'kioptrix1'/'ADMIN$' -U''%'' -c dir 2>&1
//kioptrix1/ADMIN$	[E] Can't understand response:
WARNING: The "syslog" option is deprecated
Domain=[MYGROUP] OS=[Unix] Server=[Samba 2.2.1a]
tree connect failed: NT_STATUS_WRONG_PASSWORD

 ================================================= 
|    Password Policy Information for kioptrix1    |
 ================================================= 
[V] Attempting to get Password Policy info with command: polenum '':''@'kioptrix1' 2>&1
[E] Unexpected error from polenum:
Traceback (most recent call last):
  File "/usr/bin/polenum", line 33, in <module>
    from impacket.dcerpc import dcerpc_v4, dcerpc, transport, samr
ImportError: cannot import name dcerpc_v4[V] Attempting to get Password Policy info with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c "getdompwinfo" 2>&1

[+] Retieved partial password policy with rpcclient:

Password Complexity: Disabled
Minimum Password Length: 0


 =========================== 
|    Groups on kioptrix1    |
 =========================== 
[V] Getting builtin groups with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'enumalsgroups builtin' 2>&1

[+] Getting builtin groups:
group:[Administrators] rid:[0x220]
group:[Users] rid:[0x221]
group:[Guests] rid:[0x222]
group:[Power Users] rid:[0x223]
group:[Account Operators] rid:[0x224]
group:[System Operators] rid:[0x225]
group:[Print Operators] rid:[0x226]
group:[Backup Operators] rid:[0x227]
group:[Replicator] rid:[0x228]

[+] Getting builtin group memberships:
[V] Running command: net rpc group members 'Users' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Users' (RID: 545) has member: Couldn't find group Users
[V] Running command: net rpc group members 'Power Users' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Power Users' (RID: 547) has member: Couldn't find group Power Users
[V] Running command: net rpc group members 'Guests' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Guests' (RID: 546) has member: Couldn't find group Guests
[V] Running command: net rpc group members 'Account Operators' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Account Operators' (RID: 548) has member: Couldn't find group Account Operators
[V] Running command: net rpc group members 'Replicator' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Replicator' (RID: 552) has member: Couldn't find group Replicator
[V] Running command: net rpc group members 'System Operators' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'System Operators' (RID: 549) has member: Couldn't find group System Operators
[V] Running command: net rpc group members 'Print Operators' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Print Operators' (RID: 550) has member: Couldn't find group Print Operators
[V] Running command: net rpc group members 'Administrators' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Administrators' (RID: 544) has member: Couldn't find group Administrators
[V] Running command: net rpc group members 'Backup Operators' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Backup Operators' (RID: 551) has member: Couldn't find group Backup Operators
[V] Getting local groups with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'enumalsgroups domain' 2>&1

[+] Getting local groups:
group:[sys] rid:[0x3ef]
group:[tty] rid:[0x3f3]
group:[disk] rid:[0x3f5]
group:[mem] rid:[0x3f9]
group:[kmem] rid:[0x3fb]
group:[wheel] rid:[0x3fd]
group:[man] rid:[0x407]
group:[dip] rid:[0x439]
group:[lock] rid:[0x455]
group:[users] rid:[0x4b1]
group:[slocate] rid:[0x413]
group:[floppy] rid:[0x40f]
group:[utmp] rid:[0x415]

[+] Getting local group memberships:
[V] Running command: net rpc group members 'dip' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'disk' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'wheel' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'lock' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'floppy' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'tty' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'mem' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'users' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'man' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'kmem' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'utmp' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'slocate' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Running command: net rpc group members 'sys' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

[V] Getting domain groups with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c "enumdomgroups" 2>&1

[+] Getting domain groups:
group:[Domain Admins] rid:[0x200]
group:[Domain Users] rid:[0x201]

[+] Getting domain group memberships:
[V] Running command: net rpc group members 'Domain Users' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Domain Users' (RID: 513) has member: Couldn't find group Domain Users
[V] Running command: net rpc group members 'Domain Admins' -W 'MYGROUP' -I 'kioptrix1' -U''%'' 2>&1

Group 'Domain Admins' (RID: 512) has member: Couldn't find group Domain Admins

 ==================================================================== 
|    Users on kioptrix1 via RID cycling (RIDS: 500-550,1000-1050)    |
 ==================================================================== 
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames administrator' 2>&1
[V] Assuming that user "administrator" exists
[V] User "administrator" doesn't exist.  User enumeration should be possible, but SID needed...
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames guest' 2>&1
[V] Assuming that user "guest" exists
[V] User "guest" doesn't exist.  User enumeration should be possible, but SID needed...
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames krbtgt' 2>&1
[V] Assuming that user "krbtgt" exists
[V] User "krbtgt" doesn't exist.  User enumeration should be possible, but SID needed...
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames domain admins' 2>&1
[V] Assuming that user "domain admins" exists
[V] User "domain admins" doesn't exist.  User enumeration should be possible, but SID needed...
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames root' 2>&1
[V] Assuming that user "root" exists
[I] Found new SID: S-1-5-21-4157223341-3243572438-1405127623
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames bin' 2>&1
[V] Assuming that user "bin" exists
[V] Attempting to get SID from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c 'lookupnames none' 2>&1
[V] Assuming that user "none" exists
[V] User "none" doesn't exist.  User enumeration should be possible, but SID needed...
[V] Attempting to get SIDs from kioptrix1 with command: rpcclient -W 'MYGROUP' -U''%'' 'kioptrix1' -c lsaenumsid 2>&1
[+] Enumerating users using SID S-1-5-21-4157223341-3243572438-1405127623 and logon username '', password ''
S-1-5-21-4157223341-3243572438-1405127623-500 KIOPTRIX\
                                                        (0)
S-1-5-21-4157223341-3243572438-1405127623-501 KIOPTRIX\ (0)
S-1-5-21-4157223341-3243572438-1405127623-502 KIOPTRIX\unix_group.2147483399 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-503 KIOPTRIX\unix_group.2147483399 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-504 KIOPTRIX\unix_group.2147483400 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-505 KIOPTRIX\unix_group.2147483400 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-506 KIOPTRIX\unix_group.2147483401 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-507 KIOPTRIX\unix_group.2147483401 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-508 KIOPTRIX\unix_group.2147483402 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-509 KIOPTRIX\unix_group.2147483402 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-510 KIOPTRIX\unix_group.2147483403 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-511 KIOPTRIX\unix_group.2147483403 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-512 KIOPTRIX\Domain Admins (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-513 KIOPTRIX\Domain Users (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-514 KIOPTRIX\Domain Guests (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-515 KIOPTRIX\unix_group.2147483405 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-516 KIOPTRIX\unix_group.2147483406 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-517 KIOPTRIX\unix_group.2147483406 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-518 KIOPTRIX\unix_group.2147483407 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-519 KIOPTRIX\unix_group.2147483407 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-520 KIOPTRIX\unix_group.2147483408 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-521 KIOPTRIX\unix_group.2147483408 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-522 KIOPTRIX\unix_group.2147483409 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-523 KIOPTRIX\unix_group.2147483409 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-524 KIOPTRIX\unix_group.2147483410 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-525 KIOPTRIX\unix_group.2147483410 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-526 KIOPTRIX\unix_group.2147483411 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-527 KIOPTRIX\unix_group.2147483411 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-528 KIOPTRIX\unix_group.2147483412 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-529 KIOPTRIX\unix_group.2147483412 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-530 KIOPTRIX\unix_group.2147483413 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-531 KIOPTRIX\unix_group.2147483413 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-532 KIOPTRIX\unix_group.2147483414 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-533 KIOPTRIX\unix_group.2147483414 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-534 KIOPTRIX\unix_group.2147483415 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-535 KIOPTRIX\unix_group.2147483415 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-536 KIOPTRIX\unix_group.2147483416 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-537 KIOPTRIX\unix_group.2147483416 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-538 KIOPTRIX\unix_group.2147483417 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-539 KIOPTRIX\unix_group.2147483417 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-540 KIOPTRIX\unix_group.2147483418 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-541 KIOPTRIX\unix_group.2147483418 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-542 KIOPTRIX\unix_group.2147483419 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-543 KIOPTRIX\unix_group.2147483419 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-544 KIOPTRIX\unix_group.2147483420 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-545 KIOPTRIX\unix_group.2147483420 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-546 KIOPTRIX\unix_group.2147483421 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-547 KIOPTRIX\unix_group.2147483421 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-548 KIOPTRIX\unix_group.2147483422 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-549 KIOPTRIX\unix_group.2147483422 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-550 KIOPTRIX\unix_group.2147483423 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1000 KIOPTRIX\root (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1001 KIOPTRIX\root (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1002 KIOPTRIX\bin (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1003 KIOPTRIX\bin (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1004 KIOPTRIX\daemon (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1005 KIOPTRIX\daemon (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1006 KIOPTRIX\adm (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1007 KIOPTRIX\sys (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1008 KIOPTRIX\lp (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1009 KIOPTRIX\adm (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1010 KIOPTRIX\sync (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1011 KIOPTRIX\tty (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1012 KIOPTRIX\shutdown (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1013 KIOPTRIX\disk (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1014 KIOPTRIX\halt (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1015 KIOPTRIX\lp (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1016 KIOPTRIX\mail (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1017 KIOPTRIX\mem (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1018 KIOPTRIX\news (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1019 KIOPTRIX\kmem (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1020 KIOPTRIX\uucp (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1021 KIOPTRIX\wheel (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1022 KIOPTRIX\operator (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1023 KIOPTRIX\unix_group.11 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1024 KIOPTRIX\games (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1025 KIOPTRIX\mail (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1026 KIOPTRIX\gopher (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1027 KIOPTRIX\news (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1028 KIOPTRIX\ftp (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1029 KIOPTRIX\uucp (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1030 KIOPTRIX\unix_user.15 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1031 KIOPTRIX\man (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1032 KIOPTRIX\unix_user.16 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1033 KIOPTRIX\unix_group.16 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1034 KIOPTRIX\unix_user.17 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1035 KIOPTRIX\unix_group.17 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1036 KIOPTRIX\unix_user.18 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1037 KIOPTRIX\unix_group.18 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1038 KIOPTRIX\unix_user.19 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1039 KIOPTRIX\floppy (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1040 KIOPTRIX\unix_user.20 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1041 KIOPTRIX\games (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1042 KIOPTRIX\unix_user.21 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1043 KIOPTRIX\slocate (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1044 KIOPTRIX\unix_user.22 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1045 KIOPTRIX\utmp (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1046 KIOPTRIX\squid (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1047 KIOPTRIX\squid (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1048 KIOPTRIX\unix_user.24 (Local User)
S-1-5-21-4157223341-3243572438-1405127623-1049 KIOPTRIX\unix_group.24 (Local Group)
S-1-5-21-4157223341-3243572438-1405127623-1050 KIOPTRIX\unix_user.25 (Local User)

 ========================================== 
|    Getting printer info for kioptrix1    |
 ========================================== 
[V] Attempting to get printer info with command: rpcclient -W 'MYGROUP' -U''%'' -c 'enumprinters' 'kioptrix1' 2>&1
No printers returned.


enum4linux complete on Wed Apr 22 11:52:37 2020