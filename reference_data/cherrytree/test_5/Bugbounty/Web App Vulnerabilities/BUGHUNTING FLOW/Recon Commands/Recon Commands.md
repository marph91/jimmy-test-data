


-dirsearch -u “target.com”  -x 301,403,404,500,400,502,503,302,429  --random-agent  --deep-recursive
-dirsearch -u target.txt -e php,html,js,txt,json,log,env,sql,ini,bak,config,zip,tar.gz,rar,old,tmp,orig,csv,xml,yaml,yml,md,xls,xlsx,doc,docx,pdf,db,sqlite,mdb,asp,aspx,jsp,py,rb,java,pl,css,map,sh,bat,cmd,exe,htpasswd,htaccess,crt,key,pem,pfx,p12,asc,conf,backup,smp,inc,jar,lock,sql.gz,wdl --deep-recursive --random-agent --exclude-sizes=0 --plain-text-report=output.txt
-  dirsearch -l Subdomains_firstcry.com.txt \
-e php,html,js,txt,json,log,env,sql,ini,bak,config,zip,tar.gz,rar,old,tmp,orig,csv,xml,yaml,yml,md,xls,xlsx,doc,docx,pdf,db,sqlite,mdb,asp,aspx,jsp,py,rb,java,pl,css,map,sh,bat,cmd,exe,htpasswd,htaccess,crt,key,pem,pfx,p12,asc,conf,backup,smp,inc,jar,lock,sql.gz,wdl \
--deep-recursive --random-agent --exclude-sizes=0 --output=output.txt




waybackurl 