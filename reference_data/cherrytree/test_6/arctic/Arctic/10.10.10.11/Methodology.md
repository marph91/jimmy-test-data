**++Network Scanning++**

   - [ ]  nmap -sn 10.11.1.*
   - [ ]  nmap -sL 10.11.1.*
   - [ ]  nbtscan -r 10.11.1.0/24
   - [ ]  [smbtree](broken-link 70)

**++Individual Host Scanning++**

   - [ ]  nmap  --top-ports 20 --open -iL iplist.txt
   - [ ]  nmap -sS -A -sV -O -p- ipaddress
   - [ ]  nmap -sU ipaddress

**++Service Scanning++**

    **WebApp**
      - [ ]   [Nikto](../../../beep/Kioptrix/10.10.10.7/Methodology.md)
      - [ ]   [dirb](broken-link 52)
      - [ ]   dirbuster
      - [ ]   [wpscan](broken-link 71)
      - [ ]   dotdotpwn
      - [ ]   view source 
      - [ ]   davtest\cadevar
      - [ ]   droopscan
      - [ ]   joomscan
      - [ ]   LFI\RFI Test
      
    **Linux\Windows**
      - [ ]   snmpwalk -c public -v1 *ipaddress* 1
      - [ ]   smbclient -L //ipaddress
      - [ ]   showmount -e ipaddress port
      - [ ]   rpcinfo
      - [ ]   Enum4Linux
    
    **Anything Else**
      - [ ]   [nmap scripts](broken-link 72) (locate *nse* | grep servicename)
      - [ ]   [hydra](broken-link 73)
      - [ ]   MSF Aux Modules
      - [ ]   Download the softward

**++Exploitation++**
   - [ ]   Gather Version Numbes
   - [ ]   Searchsploit
   - [ ]   Default Creds
   - [ ]   Creds Previously Gathered
   - [ ]   Download the software

**++Post Exploitation++**

    **Linux**
      - [ ]   linux-local-enum.sh
      - [ ]   linuxprivchecker.py
      - [ ]   linux-exploit-suggestor.sh
      - [ ]   unix-privesc-check.py

    **Windows**
      - [ ]   wpc.exe
      - [ ]   windows-exploit-suggestor.py
      - [ ]   [windows_privesc_check.py](https://github.com/pentestmonkey/windows-privesc-check/blob/master/windows_privesc_check.py)
      - [ ]  	windows-privesc-check2.exe

**++Priv Escalation++**
   - [ ]  [acesss internal services (portfwd)](broken-link 74)
   - [ ]  add account

**Windows**
   - [ ]  List of exploits

**Linux**
   - [ ]  sudo su 
   - [ ]  KernelDB
   - [ ]  Searchsploit

**++Final++**
   - [ ]  Screenshot of IPConfig\WhoamI
   - [ ]  Copy proof.txt
   - [ ]  Dump hashes 
   - [ ]  Dump SSH Keys
   - [ ]  Delete files