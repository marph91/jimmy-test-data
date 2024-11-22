2018-11-13 - Raspberry pie app

(2018-10-09-raspbian-stretch-lite).


Raspian
-------------
1. Do conf
2. sudo su. create file /etc/init.d/conf add:
-------------

#!/bin/bash
#/etc/init.d/aaa
### BEGIN INIT INFO
# Provides: aaa
# Required-Start: $remote_fs $syslog $network
# Required-Stop: $remote_fs $syslog $network
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: Prepare bbbb aaa
# Description: Config bridge
### END INIT INFO
case "$1" in
start)
echo "Configuring bridge"
/opt/xxxx/startbridge.sh
;;
stop)
echo "Stopping uuuuu xxxxer"
/opt/aaa/stopbridge.sh
;;
*)
echo "Usage: /etc/init.d/aaa {start|stop}"
exit 1
;;
esac
exit 0

--------------------------------------

i /opt/bbbb bskapa:
startbridge.sh:
#!/bin/bash
ifconfig eth0 0.0.0.0
ifconfig eth1 0.0.0.0
brctl addbr br0
brctl addif br0 eth0
brctl addif br0 eth1
ifconfig br0 up
ifconfig br0 0.0.0.0

stopbridge.sh:
#!/bin/bash
brctl delif br0 eth0
brctl delif br0 eth1
ifconfig br0 down
brctl delbr br0
ifconfig eth0 0.0.0.0 0.0.0.0 && dhclient
ifconfig eth1 0.0.0.0 0.0.0.0 && dhclient

3.
mkdir /opt/aaa.
mkdir /opt/aaa/data/
sudo su.
vi /etc/init.d/aaa och gör den +x. add:

--------------------------------------------
#!/bin/bash
#/etc/init.d/aa
#!/bin/bash
#/etc/init.d/aa

### BEGIN INIT INFO
# Provides: aaa
# Required-Start: $remote_fs $syslog $network prexxxx
# Required-Stop: $remote_fs $syslog $network prexxxx
# Default-Start: 2 3 4 5
# Default-Stop: 0 1 6
# Short-Description: aaaa
# Description: Let's see if we can find anything.
### END INIT INFO
case "$1" in
start)
echo "Starting aaa"
/opt/bbb/aaaa.sh
;;
stop)
echo "aaaa"
/opt/bbb/aaaa.sh
;;
restart)
echo "Restarting, zipping and creating new logfile"
/opt/bbb/bbb.sh
;;
*)
echo "Usage: /etc/init.d/noip {start|stop|restart}"
exit 1
;;
esac
exit 0

--------------------------------------------
regga så scripten körs vid startup
sudo update-rc.d bb defaults
sudo update-rc.d bb defaults

testa scriptet:
sudo /etc/init.d/aaa start
sudo /etc/init.d/aaa stop
sudo /etc/init.d/aa  restart

4. Skapa:
/opt/aaa/aaa.sh
#!/bin/bash
gzip /opt/aa/data/*.pcap
echo "Starting aaa" >> /var/log/syslog
nohup /usr/sbin/oioip -n -i br0 -w /opt/aaa/data/$(date +%Y-%m-%d\(%H%M%S\).pcap) &
/opt/aaa/bbb.sh
#!/bin/bash
pkill oioip
/opt/aaa/bbb.sh
#!/bin/bash
pkill oioip
echo "bbb: pkilled oioip" >> /var/log/syslog
gzip /opt/bbb/data/*.pcap
echo "bbb: Gzipped pcaps" >> /var/log/syslog
nohup /usr/sbin/oioip -n -i br0 -w /opt/aaa/data/$(date +%Y-%m-%d\(%H%M%S\).pcap) &
echo "bbbb: Restarted oioip" >> /var/log/syslog

5. aasee 00:01 kör restart, should dpp:
01 00 * * * /etc/init.d/bbbrestart > /var/log/aaa 2>&1