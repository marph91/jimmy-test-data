
# Debian


How to install Cherrytree in Debian:

    1. Install wget and Cherrytree dependencies.
    
    
```sh
sudo apt install wget python-dbus python-chardet python-enchant libcanberra-gtk-module libgtksourceview2.0-0 libgtksourceview2.0-common python-cairo python-gobject-2 python-gtk2 python-numpy
```

    
    2. Download python-gtksourceview2.
    
    
```sh
wget http://ftp.br.debian.org/debian/pool/main/p/pygtksourceview/python-gtksourceview2_2.10.1-3_amd64.deb 
```

    
    3. Install python-gtksourceview2.
    
    
```sh
sudo dpkg -i python-gtksourceview2_2.10.1-3_amd64.deb 
```

    
    4. Download Cherrytree.
    
    
```sh
wget http://www.giuspen.com/software/cherrytree_0.38.9-0_all.deb 
```

    
    5. Install Cherrytree
    
    
```sh
sudo dpkg -i cherrytree_0.38.9-0_all.deb
```
