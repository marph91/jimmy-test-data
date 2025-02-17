https://tgarc.github.io/2015/03/24/connecting-to-a-bluetooth-speaker-with-pulseaudio/

# Intro

This post is a summary of the steps that were necessary for me to set up an A2DP
interface to a bluetooth speaker using pulseaudio. This setup was completed
using the original BeagleBone with Linaro Ubuntu 14.04 but should apply for any
debian based distribution.

# Beaglebone USB issues

If you’re using a USB bluetooth dongle you will have to supply the board with an
external power supply. I also found that, even with the proper external power
supply, if the dongle was connected before the beaglebone had finished starting
up the dongle wouldn’t be detected by the OS.

A workaround that typically worked in these cases was to simply run

    sudo lsusb -v

In most cases the bluetooth dongle would immediately turn on and be detected
properly with this command. (If you can shed any light on why this works I would
be hugely thankful). The other workaround is just to make sure you don’t connect
the USB dongle until the board has finished starting up.

# Onwards

Firstly, we install the necessary packages for handling bluetooth

    $ sudo apt-get install bluez pulseaudio-module-bluetooth python-gobject python-gobject-2 bluez-tools

Now, make sure your bluetooth dongle is connected and shows up in the lsusb listing.

    $ lsusb
    Bus 001 Device 004: ID 0a12:0001 Cambridge Silicon Radio, Ltd Bluetooth Dongle (HCI mode)

Let’s add our user to the pulse audio group (lp) so user can play audio through
it (replace pi with your user name)

    sudo usermod -a -G lp pi

Now, turn on the bluetooth speaker and put it in pairing mode. Then scan for it with

    $ hcitool scan
    Scanning ...
        00:11:67:8C:17:80   H163

This gives us the bluetooth’s MAC address for use in later step. Now create a
file `/etc/asound.conf` with the following content

    pcm.bluetooth {
        type bluetooth
        device 00:11:67:8C:17:80 # change this MAC address to the one you wrote down
    }

Modify your bluetooth audio config appropriately so that your Enable line
includes *Headset* and *Sink* at least. I used

    Enable=Source,Sink,Headset

You may need to add this additional line if you have trouble

    Disable=Socket

Restart the Bluetooth service to put these changes into effect

    $ sudo service bluetooth restart

Now, we have to make a minor modification the pulseaudio daemon config file.

    $ sudo nano /etc/pulse/daemon.conf

Look for this line

    resample-method = speex-float-3

and replace it with

    ; resample-method = speex-float-3

Then, add this line underneath it

    resample-method = trivial

Exit and save. Now we can start the pulseaudio daemon

    $ pulseaudio –start

Now to pair the device we use bluez-simple-agent. Make sure to put bluetooth speaker in pairing
mode first.

    $ bluez-simple-agent hci0 00:11:67:8C:17:80

Finally, we’ll connect to the bluetooth speaker using the MAC address you
obtained earlier

    $ bluez-test-audio connect 00:11:67:8C:17:80

Verify you’re connected with hcitool. You should get something like below

    $ hcitool con
    Connections:
            < ACL 00:11:67:8C:17:80 handle 70 state 1 lm MASTER AUTH ENCRYPT

Great, now a bluetooth sink should be available for pulseaudio

    $ pactl list sinks short
    1       bluez_sink.00:11:67:8C:17:80    module-bluetooth-device.c       s16le 2ch 44100Hz       RUNNING

If you have other audio devices you should set the default sink to our new
bluetooth sink (make sure to replace bluez\_sink.00:11:67:8C:17:80 with your own
bluetooth sink id)

    pacmd set-default-sink bluez_sink.00:11:67:8C:17:80

# Sources

<http://stackoverflow.com/questions/24580155/pulseaudio-not-detecting-bluetooth-headset>

<http://blog.whatgeek.com.pt/2014/04/raspberry-pi-bluetooth-wireless-speaker/>

<http://www.instructables.com/id/Turn-your-Raspberry-Pi-into-a-Portable-Bluetooth-A/?ALLSTEPS>