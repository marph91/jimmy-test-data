
# Fedora


 ## Fedora 30 and EarlierFedora 30 and Earlier

How to install Cherrytree in Fedora 30 and earlier:

	1. Download the latest installer that has a** .rpm **extension from the [downloads webpage](https://www.giuspen.com/cherrytree/#downl).

	2. Open a terminal and change to the directory containing your installation file.

	3. Enter the following command, replacing **cherrytree.rpm** with the name of your installation file:



	4. Provide your password when prompted to complete the installation


 ## Fedora 31 and LaterFedora 31 and Later

How to install Cherrytree in Fedora 31 and later:

    1. Enable the Cherrytree COPR repository.
      
      
      
    2. Install Cherrytree
    
    
```sh
sudo rpm -Uvh --force cherrytree.rpm
```

```sh
sudo dnf copr enable bcotton/cherrytree
```

```sh
sudo dnf install cherrytree
```
