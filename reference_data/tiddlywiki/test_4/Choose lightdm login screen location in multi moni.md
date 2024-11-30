https://askubuntu.com/questions/234930/choose-lightdm-login-screen-location-in-multi-monitor-setup

At least with Ubuntu 16.04, which includes **lightdm-gtk-greeeter 2.0.1**, the following entry in `/etc/lightdm/lightdm-gtk-greeter.conf` can be used to fix the initial position of the login dialog on a certain monitor:

    [greeter]
    active-monitor=0

https://askubuntu.com/questions/234930/choose-lightdm-login-screen-location-in-multi-monitor-setup

This did the trick for me. Find out your primary screen:

    $ xrandr

And create the file **/usr/bin/dualmon.sh** with the following command:

    xrandr –output DVI-0 –primary

\*\*Change DVI-0 for your primary screen.\*

Make it executable:

    sudo chmod +x /usr/bin/dualmon.sh.

And add it to **/etc/lightdm/lightdm.conf** file:

    [SeatDefaults]
    display-setup-script=/usr/bin/dualmon.sh
    session-setup-script=/usr/bin/dualmon.sh

https://askubuntu.com/questions/234930/choose-lightdm-login-screen-location-in-multi-monitor-setup

**/etc/lightdm/lightdm.conf**

Search for the line "display-setup-script" and change it to read:

    display-setup-script=xrandr –output HDMI-1 –primary

Obviously replacing "HDMI-1" with your desired monitor, eg. "DVI-1" or "DP-1" for DVI or DisplayPort if not HDMI.

I currently use **lightdm-webkit2-greeter** so I don't have this option, but if you use the **lightdm-gtk-greeter** then you can do the following instead:

    [greeter]
    active-monitor=0

In the file **/etc/lightdm/lightdm-gtk-greeter.conf**