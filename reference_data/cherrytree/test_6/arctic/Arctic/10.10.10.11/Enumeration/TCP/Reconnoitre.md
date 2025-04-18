### [Reconnoitre](https://github.com/codingo/Reconnoitre)

```sh
# Scan a single host, create file structure & discover services
python reconnoitre.py -t 192.168.1.5 -o /root/Documents/labs/ --services

# Discover live hosts & hostnames within a range
python reconnoitre.py -t 192.168.1.1-252 -o /root/Documents/testing/ --pingsweep --hostnames
    
# Discover live hosts within a range and then do a quick probe for services
python reconnoitre.py -t 192.168.1.1-252 -o /root/Documents/testing/ --pingsweep --services --quick    
    
# Discover live hosts w/in a range & probe all ports (tcp & udp) for services
python reconnoitre.py -t 192.168.1.1-252 -o /root/Documents/testing/ --pingsweep --services
```
