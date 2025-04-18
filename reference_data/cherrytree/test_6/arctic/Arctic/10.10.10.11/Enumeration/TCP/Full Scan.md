sudo nmap -p- -sV -sS -T4 target
---
Starting Nmap 7.80 ( <https://nmap.org> ) at 2020.06.03 14:50 EDT
Nmap scan report for target (10.10.10.11.
Host is up (0.032s latency).
Not shown: 65532 filtered ports
PORT      STATE SERVICE VERSION
135/tcp   open  msrpc   Microsoft Windows RPC
8500/tcp  open  fmtp?
49154/tcp open  unknown
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at <https://nmap.org/submit/> .
Nmap done: 1 IP address (1 host up) scanned in 121.77 seconds
