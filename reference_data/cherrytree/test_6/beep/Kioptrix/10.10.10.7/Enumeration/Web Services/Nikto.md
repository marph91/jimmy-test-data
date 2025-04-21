nikto -h target -p 80,443
---
- Nikto v2.1.6
---------------------------------------------------------------------------
+ No web server found on target:443
---------------------------------------------------------------------------
+ Target IP:          10.10.10.7
+ Target Hostname:    target
+ Target Port:        80
+ Start Time:         2020-05-29 14:56:53 (GMT-4)
---------------------------------------------------------------------------
+ Server: Apache/2.2.3 (CentOS)
+ The anti-clickjacking X-Frame-Options header is not present.
+ The X-XSS-Protection header is not defined. This header can hint to the user agent to protect against some forms of XSS
+ The X-Content-Type-Options header is not set. This could allow the user agent to render the content of the site in a different fashion to the MIME type
+ Root page / redirects to: <https://target/>
+ Apache/2.2.3 appears to be outdated (current is at least Apache/2.4.37). Apache 2.2.34 is the EOL for the 2.x branch.
+ OSVDB-877: HTTP TRACE method is active, suggesting the host is vulnerable to XST
+ OSVDB-3268: /icons/: Directory indexing found.
+ Server may leak inodes via ETags, header found with file /icons/README, inode: 884871, size: 4872, mtime: Thu Jun 24 15:46:08 2010
+ OSVDB-3233: /icons/README: Apache default file found.
+ 8494 requests: 0 error(s) and 8 item(s) reported on remote host
+ End Time:           2020-05-29 15:06:30 (GMT-4) (577 seconds)
---------------------------------------------------------------------------
+ 1 host(s) tested
