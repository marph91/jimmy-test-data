[linux](broken-link linux)

https://superuser.com/questions/181733/how-can-i-restore-grub-without-a-live-cd

I managed to boot using the grub rescue prompt with the help of the [Ubuntu grub2 reference](https://help.ubuntu.com/community/Grub2) using these commands:

1.  ls
2.  set prefix=(hdX,Y)/boot/grub
3.  set root=(hdX,Y)
4.  set
5.  ls /boot
6.  insmod /boot/grub/linux.mod
7.  linux /vmlinuz root=/dev/sdXY ro
8.  initrd /initrd.img
9.  boot