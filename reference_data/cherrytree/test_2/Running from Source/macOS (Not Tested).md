
# macOS (Not Tested)


	Cherrytree is not supported for macOS but can be installed from source using [Homebrew](https://brew.sh/).
	
	1. Install [Python 2.7](https://www.python.org/downloads/mac-osx/).

	2. Install [Homebrew](https://brew.sh/).

	3. Install Cherrytree’s core dependencies using Homebrew and the following commands:
	
	
```sh
brew install gtk-mac-integration
```

	
	
```sh
brew install pygtksourceview
```

	
	
```sh
brew install dbus
```

	
	
```sh
brew install dbus-glib
```

	
	4. (**Optional**) Install dependencies for additional functionality using **PIP** (a package manager for Python):
	
		-  For multiple instances centralization. (Double-clicking a file that is already open displays the open document instead of opening another instance of that file.)
		
		
```sh
python2 -m pip install dbus-python
```

		
		-  For spell check functionality.
		
		
```sh
python2 -m pip install pyenchant
```

		
		-  For better decoding support of imported and pasted text.
		
		

	5. 
```sh
python2 -m pip install chardet
```
[Clone](https://git-scm.com/docs/git-clone) or download the [Cherrytree repository](https://github.com/giuspen/cherrytree).

	6. Open a terminal, change to the directory containing your local copy of Cherrytree, and run:
	
	
	
	
```sh
python2 cherrytree
```
**NOTE:** View [this discussion](https://github.com/giuspen/cherrytree/issues/176) for more information about building Cherrytree on macOS.
