Initially, we are *relia\jim*.
We have keepass installed.

We will find: *Users\jim\Documents\Database.kdbx*
We will crack the password using john:

```sh
keepass2john Database.kdbx > Keepasshash.txt
john --wordlist=/usr/share/wordlists/rockyou.txt Keepasshash.txt
```

Password found: **mercedes1**.

Pwned using internaladmin credentials.