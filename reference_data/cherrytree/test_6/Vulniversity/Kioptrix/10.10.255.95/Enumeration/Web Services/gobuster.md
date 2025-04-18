gobuster dir -u [http://target:3333](http://<ip>:3333) -w /usr/share/dirb/wordlists/big.txt
gobuster dir -u <http://10.10.255.95:3333> -w dirbuster/directory-list-2.3.medium.txt
/usr/share/wordlists has many lists
---
GoBuster flag	Description
-e	Print the full URLs in your console
-u	The target URL
-w	Path to your wordlist
-U and -P	Username and Password for Basic Auth
-p <x>	Proxy to use for requests
-c <http cookies>	Specify a cookie for simulating your auth
---
user@kalisi:/usr/share/wordlists$ gobuster dir -u <http://10.10.255.95:3333> -w dirbuster/directory-list-2.3.medium.txt
===============================================================
Gobuster v3.0.1
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@_FireFart_)
===============================================================
[+] Url:            <http://10.10.255.95:3333>
[+] Threads:        10
[+] Wordlist:       dirbuster/directory-list-2.3.medium.txt
[+] Status codes:   200,204,301,302,307,401,403
[+] User Agent:     gobuster/3.0.1
[+] Timeout:        10s
===============================================================
2020/05/22 08:08:50 Starting gobuster
===============================================================
/images (Status: 301.
/css (Status: 301.
/js (Status: 301.
/fonts (Status: 301.
/internal (Status: 301.

*internal has a file upload feature