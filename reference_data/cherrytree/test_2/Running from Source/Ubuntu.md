
# Ubuntu


	1. Cherrytree requires Python 2.7. Open a terminal and check your current version of Python using the command:
	
	
	
	2. If a variant of **`Python 2.7`** is not returned, install it by running the following command then check the version again:
	
	
	
	3. Install Cherrytree’s core dependencies with the command:
	
	
	
	4. (**Optional**) Install dependencies for additional functionality:
	
		-  To use an appindicator in systray instead of the standard systray.
	
	   
	
		-  For multiple instances centralization. (Double-clicking a file that is already open displays the open document instead of opening another instance of that file.)
	
		
	
		-  For spell check fuctionality.
	
		
	
		-  For better decoding support of imported and pasted text.
	
		

	5. [Clone](https://git-scm.com/docs/git-clone) or download the [Cherrytree repository](https://github.com/giuspen/cherrytree).

	6. Open a terminal, change to the directory containing your local copy of Cherrytree, and run:
	
	
	
```sh
python2 --version
```

```sh
sudo apt install python2.7 python-pip
```

```sh
sudo apt install python-gtk2 python-gtksourceview2 p7zip-full libcanberra-gtk-module
```

```sh
sudo apt install python-appindicator
```

```sh
	sudo apt install python-dbus
```

```sh
sudo apt install python-enchant
```

```sh
sudo apt install python-chardet
```

```sh
python2 cherrytree
```
