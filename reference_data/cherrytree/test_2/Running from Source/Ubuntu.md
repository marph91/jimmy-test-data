
# Ubuntu


	1. Cherrytree requires Python 2.7. Open a terminal and check your current version of Python using the command:
	
	
```sh
python2 --version
```

	
	2. If a variant of **`Python 2.7`** is not returned, install it by running the following command then check the version again:
	
	
```sh
sudo apt install python2.7 python-pip
```

	
	3. Install Cherrytree’s core dependencies with the command:
	
	
```sh
sudo apt install python-gtk2 python-gtksourceview2 p7zip-full libcanberra-gtk-module
```

	
	4. (**Optional**) Install dependencies for additional functionality:
	
		-  To use an appindicator in systray instead of the standard systray.
	
	   
```sh
sudo apt install python-appindicator
```

	
		-  For multiple instances centralization. (Double-clicking a file that is already open displays the open document instead of opening another instance of that file.)
	
		
```sh
	sudo apt install python-dbus
```

	
		-  For spell check fuctionality.
	
		
```sh
sudo apt install python-enchant
```

	
		-  For better decoding support of imported and pasted text.
	
		

	5. 
```sh
sudo apt install python-chardet
```
[Clone](https://git-scm.com/docs/git-clone) or download the [Cherrytree repository](https://github.com/giuspen/cherrytree).

	6. Open a terminal, change to the directory containing your local copy of Cherrytree, and run:
	
	
	
```sh
python2 cherrytree
```
