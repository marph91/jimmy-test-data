https://www.redpill-linpro.com/techblog/2021/05/31/better-bluetooth-headset-audio-with-msbc.html

### Enabling mSBC support

Support for the mSBC codec is unfortunately disabled by default in Pipewire, because not all Bluetooth adapters and headsets support it. In order to enable it, create the file `~/.config/pipewire/media-session.d/bluez-monitor.conf` (or `/etc/pipewire/media-session.d/bluez-monitor.conf`) with the following contents:

``` highlight
properties = {
    bluez5.msbc-support = true
}
```

Afterwards, restart Pipewire with `systemctl –user restart pipewire.service`.

To confirm that it now works, connect your Bluetooth headset and open the *Audio* pane in *GNOME Settings* (from the command line: `gnome-control-center sound`). If everything is in order, HSP with mSBC should be available choices in the *Configuration* drop-down lists:

[![Figure 1: Audio pane in GNOME Settings](https://www.redpill-linpro.com/techblog/images/posts/better-bluetooth-headset-audio-with-msbc/GNOME_Settings.png)](https://www.redpill-linpro.com/techblog/2021/05/31/better-bluetooth-headset-audio-with-msbc.html/techblog/images/posts/better-bluetooth-headset-audio-with-msbc/GNOME_Settings.png)

Figure 1: Audio pane in GNOME Settings

### mSBC and CVSD compared

How much better does mSBC sound, compared to CVSD? I will try to demonstrate by recording audio while switching back and forth between the codecs every five seconds.

I start out with CVSD, so if the seconds counter in your audio player ends with 0-4, you are listing to CVSD; if the seconds counter ends with 5-9, you are listening to mSBC.

Do note that the microphones I use are not exactly studio quality. Therefore, the recordings are unable to fully capture the *actual* difference in quality between the codecs. Nevertheless I hope that they give you a fairly good idea of how different they sound.

#### Recording

In this recording I simply talk while wearing my [Sony WH-1000XM3](https://www.sony.com/ug/electronics/headband-headphones/wh-1000xm3) headset. This headset is not known for having very a very good microphone, but the difference is nevertheless very clear to me.

-   [CVSD vs mSBC - recording](https://www.redpill-linpro.com/techblog/2021/05/31/better-bluetooth-headset-audio-with-msbc.html/techblog/images/posts/better-bluetooth-headset-audio-with-msbc/CVSD_vs_mSBC_recording.mp3)

#### Playback

This recording was performed by placing the microphone of the standard wired earbuds that came with my phone over my ear before putting my headset on over it. I then play back audio from our [IT Talks podcast](https://ittalks.libsyn.com) while alternating the codecs.

-   [CVSD vs mSBC - playback](https://www.redpill-linpro.com/techblog/2021/05/31/better-bluetooth-headset-audio-with-msbc.html/techblog/images/posts/better-bluetooth-headset-audio-with-msbc/CVSD_vs_mSBC_playback.mp3)

### Related tips and tricks

#### The SBC-XQ codec

Pipewire also comes with support for the SBC-XQ codec for A2DP, which supposedly is an improvement over the standard SBC codec (but not over other codecs like AAC and LDAC, as far as I know). In any case, I have trouble telling the difference – all the A2DP codecs sound good to me.

SBC-XQ can be enabled in the pretty much same way as mSBC is. Just edit the `bluez-monitor.conf` file and add another line so it reads:

``` highlight
properties = {
    bluez5.msbc-support = true
    bluez5.sbc-xq-support = true
}
```

After restarting PipeWire you should now find the SBC-XQ codec in the Output *Configuration* drop-down list in *Audio* pane the *GNOME Settings* application.

#### Battery level reporting

Having Pipewire report the battery level requires manually enabling an experimental API in the [BlueZ](http://www.bluez.org/) Bluetooth stack. This can be done by running `sudo systemctl edit bluetooth.service` and entering the following lines where the comments prompt you to:

``` highlight
[Service]
ExecStart=
ExecStart=/usr/libexec/bluetooth/bluetoothd –experimental
```

Afterwards, restart BlueZ with `sudo systemctl restart bluetooth.service`. Now you should be able to see your headset’s battery level in the *Power* pane of *GNOME Settings* (from the command line: `gnome-control-center power`).