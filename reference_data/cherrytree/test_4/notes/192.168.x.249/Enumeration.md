On port 8000 we have default XAMPP page.
We can access phpinfo on <http://192.168.215.249:8000/dashboard/phpinfo.php>.


| Server Root | C:/xampp/apache |
| --- | --- |


We find the following directories:

```sh
200      GET      167l      649w     7577c http://192.168.215.249:8000/dashboard/
200      GET        7l       39w     2010c http://192.168.215.249:8000/CMS/templates/images/ritecms-powered.png
200      GET       31l      117w     1462c http://192.168.215.249:8000/CMS/
200      GET        7l       57w     2442c http://192.168.215.249:8000/dashboard/images/fastly-logo.png
403      GET       11l       47w      426c http://192.168.215.249:8000/phpmyadmin
200      GET       17l       21w      177c http://192.168.215.249:8000/bitnami.css
200      GET       79l      250w     3607c http://192.168.215.249:8000/applications.html
200      GET      167l      649w     7577c http://192.168.215.249:8000/dashboard/index.html
200      GET        8l       76w     4088c http://192.168.215.249:8000/dashboard/images/fastly-logo@2x.png
200      GET      131l      390w     6021c http://192.168.215.249:8000/dashboard/howto.html
200      GET      523l     3762w    31751c http://192.168.215.249:8000/dashboard/faq.html
200      GET      889l     4751w    78149c http://192.168.215.249:8000/dashboard/phpinfo.php
200      GET     9147l    36448w   481698c http://192.168.215.249:8000/dashboard/stylesheets/all.css
200      GET        7l       39w     2010c http://192.168.215.249:8000/cms/templates/images/ritecms-powered.png
200      GET       31l      117w     1462c http://192.168.215.249:8000/cms/
503      GET       11l       44w      407c http://192.168.215.249:8000/examples
200      GET        6l      434w    71670c http://192.168.215.249:8000/favicon.ico
200      GET        5l        9w      694c http://192.168.215.249:8000/img/module_table_top.png
200      GET        3l       16w     1549c http://192.168.215.249:8000/img/module_table_bottom.png
200      GET       17l       73w     1221c http://192.168.215.249:8000/img/
403      GET       11l       47w      426c http://192.168.215.249:8000/licenses
403      GET       11l       47w      426c http://192.168.215.249:8000/server-info
403      GET       11l       47w      426c http://192.168.215.249:8000/server-status
403      GET       11l       47w      426c http://192.168.215.249:8000/webalizer
200      GET       15l       52w      776c http://192.168.215.249:8000/xampp/
200      GET        3l       16w     1549c http://192.168.215.249:8000/IMG/module_table_bottom.png
200      GET        5l        9w      694c http://192.168.215.249:8000/IMG/module_table_top.png
200      GET       17l       73w     1221c http://192.168.215.249:8000/IMG/
200      GET        5l        9w      694c http://192.168.215.249:8000/Img/module_table_top.png
200      GET        3l       16w     1549c http://192.168.215.249:8000/Img/module_table_bottom.png
200      GET       17l       73w     1221c http://192.168.215.249:8000/Img/
200      GET       79l      250w     3607c http://192.168.215.249:8000/Applications.html
200      GET      167l      649w     7577c http://192.168.215.249:8000/Dashboard/
200      GET       15l       52w      784c http://192.168.215.249:8000/Webalizer/
200      GET        7l       39w     2010c http://192.168.215.249:8000/Cms/templates/images/ritecms-powered.png
200      GET       31l      117w     1462c http://192.168.215.249:8000/Cms/
200      GET       79l      250w     3607c http://192.168.215.249:8000/APPLICATIONS.html
200      GET       15l       52w      784c http://192.168.215.249:8000/WEBALIZER/
```


On */cms* we find **RiteCMS version v3**.
We can login into the administrator via **admin:admin** credentials.

On port 80, endpoint */Orchard*, we find an Orchard instance

In *C:/staging*, we find a repository:

```sh
commit 8b430c17c16e6c0515e49c4eafdd129f719fde74 (HEAD -> master)
Author: damian <damian>
Date:   Thu Oct 20 02:07:42 2022 -0700

    Email config not required anymore

commit 967fa71c359fffcbeb7e2b72b27a321612e3ad11
Author: damian <damian>
Date:   Thu Oct 20 02:06:37 2022 -0700
```
