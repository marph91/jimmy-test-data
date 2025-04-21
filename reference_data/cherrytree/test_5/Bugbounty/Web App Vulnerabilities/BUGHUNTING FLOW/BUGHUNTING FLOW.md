
**Use proper ReadMe file in vscode to track the progress**

**Framework :** 
			1. Magic Recon
			2.ars0n-framework
			3. FinalRecon
			4. MagicRecon
			5. reconftw
			6. spyhunt


- Find Subdomains.
      - Subfinder
      - Assetfinder
      - sublister
      - crtsh
         - Navigate to crtsh node and use the code to extract subdomains from the site
      - Amass  
         - amass enum -active -d target.com -brute -w /home/zero/Desktop/Payloads/SecLists-master/Discovery/DNS/deepmagic.com-prefixes-top50000.txt -ip -config /root/amass/config.yaml -o amass_subdomains.txt


- Use Spyhunt tools
      - Subdomain enumeration
         - python3 spyhunt.py -s yahoo.com --shodan API_KEY --save filename.txt
      -  Technology detection
      -  DNS record scanning
      - 


- Find Active Domains
      - httpx    :  **cat subs.txt |  httpx  -sc -ip  -title**
      - hhtprobe

- Aggregate all Subdomains
      - Catogorize based on status code   :   **cat  subs.txt | grep “200”**   >>200links.txt => **cat 200links.txt | awk ‘{print $1}’**  
      - Port Scanning  **>>>>**   Spyhunt  ||  NMAP  || RustScan

- Fetch  URLS 
      - Paramspider   -   fetch with FUZZ keywords ->we can replace the fuzz with payload using qsreplace tool
      - katana
      -** gau
      - hakcrawler
      - subjs**
      - waybackurls
      - Spyhunt 
                  - Web crawling and URL extraction
                  - JavaScript file discovery
                  - Domain information gathering
                  - API endpoint fuzzing
                  - Shodan integration for additional recon
                  - Google dorking
                  - JavaScript file scanning for sensitive info
                  - API Fuzzing
                  - AWS S3 Bucket Enumeration
                  - JSON Web Token Scanning
                  -Web Server Detection
                  
                  
- Use commands to aggregate all ulrs
      - anew

- Direcory Brueforce
      - wfuzz
      - ffuf
      - Dirbuster
      - dirsearch
      - Spy Hunt
                  - Directory and file brute-forcing

- Secret Finder 
      - Use Secret finder to find sensitive content from Js files

- Bypass 403 domains 
      - Bypass-403
