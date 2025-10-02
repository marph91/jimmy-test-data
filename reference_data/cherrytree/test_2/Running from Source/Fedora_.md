
# Fedora

This only works in Fedora 30 and earlier. PYGtkSourceView2, one of Cherrytree's dependencies, is obsolete and removed from Fedora in version 31 and later.

	1. Install Python2
	
	
```sh
sudo dnf install python2
```


	2. Install Cherrytree’s core dependencies with the command:

	
```sh
sudo dnf install pygtk2 pygtksourceview p7zip p7zip-plugins
```


	3. (**Optional**) Install dependencies for additional functionality:

		- To use an appindicator in systray instead of the standard systray.
		   
				
```sh
sudo dnf install python-appindicator
```


		- For multiple instances centralization. (Double-clicking a file that is already open displays the open document instead of opening another instance of that file.)
		
				
```sh
sudo dnf install python-dbus
```


		- For spell check fuctionality.
		   
				
```sh
sudo dnf install python-enchant
```


		- For better decoding support of imported and pasted text.
		   
				
```sh
sudo dnf install python-chardet
```


	4. [Clone](https://git-scm.com/docs/git-clone) or download the [Cherrytree repository](https://github.com/giuspen/cherrytree).

	5. Open a terminal, change to the directory containing your local copy of Cherrytree, and run:
	
	
	
```sh
python2 cherrytree
```
