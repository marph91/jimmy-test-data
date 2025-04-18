enum4linux -v (or -a) target
nmblookup -A target
rpcclient -U “” target
---
user@kalisi:~$ enum4linux -v target
[V] Dependent program "nmblookup" found in /usr/bin/nmblookup
[V] Dependent program "net" found in /usr/bin/net
[V] Dependent program "rpcclient" found in /usr/bin/rpcclient
[V] Dependent program "smbclient" found in /usr/bin/smbclient
[V] Dependent program "polenum" found in /usr/bin/polenum
[V] Dependent program "ldapsearch" found in /usr/bin/ldapsearch
Starting enum4linux v0.8.9 ( <http://labs.portcullis.co.uk/application/enum4linux/> ) on Wed Jun  3 15:04:51 2020

 ========================== 
|    Target Information    |
 ========================== 
Target ........... target
RID Range ........ 500.550,1000.1050
Username ......... ''
Password ......... ''
Known Usernames .. administrator, guest, krbtgt, domain admins, root, bin, none


 ============================================== 
|    Enumerating Workgroup/Domain on target    |
 ============================================== 
[V] Attempting to get domain name with command: nmblookup -A 'target'
[E] Can't find workgroup/domain


 ====================================== 
|    Nbtstat Information for target    |
 ====================================== 
Looking up status of 10.10.10.11
No reply from 10.10.10.11

 =============================== 
|    Session Check on target    |
 =============================== 
Use of uninitialized value $global_workgroup in concatenation (.) or string at ./enum4linux.pl line 437.
[V] Attempting to make null session using command: smbclient -W '' //'target'/ipc$ -U''%'' -c 'help' 2.&1
[E] Server doesn't allow session using username '', password ''.  Aborting remainder of tests.
---
user@kalisi:~$ nmblookup -A target
Looking up status of 10.10.10.11
No reply from 10.10.10.11
---
user@kalisi:~$ rpcclient -U "" target
Enter WORKGROUP\'s password: 
Cannot connect to server.  Error was NT_STATUS_IO_TIMEOUT
---
