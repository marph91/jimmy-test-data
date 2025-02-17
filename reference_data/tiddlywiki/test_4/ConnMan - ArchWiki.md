https://wiki.archlinux.org/title/ConnMan

# ConnMan

-   [Page](https://wiki.archlinux.org/title/ConnMan/title/ConnMan "View the content page [alt-shift-c]")
-   [Discussion](https://wiki.archlinux.org/title/ConnMan/title/Talk:ConnMan "Discussion about the content page [alt-shift-t]")

English

-   [Read](https://wiki.archlinux.org/title/ConnMan/title/ConnMan)
-   [View source](https://wiki.archlinux.org/title/ConnMan/index.php?title=ConnMan&action=edit "This page is protected.
    You can view its source [alt-shift-e]")
-   [View history](https://wiki.archlinux.org/title/ConnMan/index.php?title=ConnMan&action=history "Past revisions of this page [alt-shift-h]")

More

-   [Read](https://wiki.archlinux.org/title/ConnMan/title/ConnMan)
-   [View source](https://wiki.archlinux.org/title/ConnMan/index.php?title=ConnMan&action=edit)
-   [View history](https://wiki.archlinux.org/title/ConnMan/index.php?title=ConnMan&action=history)

From ArchWiki

Related articles

-   [Network configuration](https://wiki.archlinux.org/title/ConnMan/title/Network_configuration "Network configuration")
-   [Wireless network configuration](https://wiki.archlinux.org/title/ConnMan/title/Wireless_network_configuration "Wireless network configuration")

[ConnMan](https://web.archive.org/web/20210224075615/https://01.org/connman) is a command-line network manager designed for use with embedded devices and fast resolve times. It is modular through a [plugin architecture](https://git.kernel.org/cgit/network/connman/connman.git/tree/plugins), but has native [DHCP](https://en.wikipedia.org/wiki/DHCP "wikipedia:DHCP") and [NTP](https://wiki.archlinux.org/title/ConnMan/title/NTP "NTP") support.[\[1\]](https://git.kernel.org/cgit/network/connman/connman.git/tree/src/)

## Installation

[Install](https://wiki.archlinux.org/title/ConnMan/title/Install "Install") the [connman](https://archlinux.org/packages/?name=connman) package. [wpa\_supplicant](https://archlinux.org/packages/?name=wpa_supplicant), [bluez](https://archlinux.org/packages/?name=bluez), and [openvpn](https://archlinux.org/packages/?name=openvpn) are optional dependencies required for Wi-Fi, Bluetooth, and VPN functionality respectively.

Before [enabling](https://wiki.archlinux.org/title/ConnMan/title/Enabling "Enabling") `connman.service`, ensure any existing [network configuration](https://wiki.archlinux.org/title/ConnMan/title/Network_configuration "Network configuration") is disabled.

ConnMan comes with the [connmanctl(1)](https://man.archlinux.org/man/connmanctl.1) CLI, there are various [\#Front-ends](https://wiki.archlinux.org/title/ConnMan#Front-ends) available.

### Front-ends

-   **cmst** — Qt GUI for ConnMan.

[https://github.com/andrew-bibb/cmst](https://github.com/andrew-bibb/cmst) \|\| [cmst](https://aur.archlinux.org/packages/cmst/)^AUR^

-   **connman-ncurses** — Simple ncurses UI for ConnMan; not all of connman functionality is implemented, but usable (with X or from terminal without X), see the [wiki](https://github.com/eurogiciel-oss/connman-json-client/wiki).

[https://github.com/eurogiciel-oss/connman-json-client](https://github.com/eurogiciel-oss/connman-json-client) \|\| [connman-ncurses-git](https://aur.archlinux.org/packages/connman-ncurses-git/)^AUR^

-   **ConnMan-UI** — GTK3 client applet.

[https://github.com/tbursztyka/connman-ui](https://github.com/tbursztyka/connman-ui) \|\| [connman-ui-git](https://aur.archlinux.org/packages/connman-ui-git/)^AUR^

-   **connman\_dmenu** — Client/frontend for dmenu.

[https://github.com/taylorchu/connman\_dmenu](https://github.com/taylorchu/connman_dmenu) \|\| [connman\_dmenu-git](https://aur.archlinux.org/packages/connman_dmenu-git/)^AUR^

-   **rofi-connman** — rofi/dmenu-powered frontend

[https://github.com/sourcemage/rofi-connman](https://github.com/sourcemage/rofi-connman) \|\| [rofi-connman](https://aur.archlinux.org/packages/rofi-connman/)^AUR^

-   **Econnman** — Enlightenment desktop panel applet.

[https://www.enlightenment.org](https://www.enlightenment.org) \|\| [econnman](https://aur.archlinux.org/packages/econnman/)^AUR^

-   **LXQt-Connman-Applet** — LXQt desktop panel applet.

[https://github.com/lxqt/lxqt-connman-applet](https://github.com/lxqt/lxqt-connman-applet) \|\| [lxqt-connman-applet](https://aur.archlinux.org/packages/lxqt-connman-applet/)^AUR^

-   **connman-gtk** — GTK client.

[https://github.com/jgke/connman-gtk](https://github.com/jgke/connman-gtk) \|\| [connman-gtk](https://aur.archlinux.org/packages/connman-gtk/)^AUR^

-   **gnome-extension-connman** — Gnome3 extension for connman; it contains only some of the functionality without installing connman-gtk.

[https://github.com/jgke/gnome-extension-connman](https://github.com/jgke/gnome-extension-connman) \|\| [https://extensions.gnome.org/extension/981/connman-extension/](https://extensions.gnome.org/extension/981/connman-extension/)

## Usage

[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/ConnMan/title/File:Tango-view-fullscreen.png)**This article or section needs expansion.**[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/ConnMan/title/File:Tango-view-fullscreen.png)

**Reason:** Only Wired and Wi-Fi plugins are described. (Discuss in [Talk:ConnMan](https://wiki.archlinux.org/title/Talk:ConnMan))

ConnMan comes with the `connmanctl` command-line interface, see [connmanctl(1)](https://man.archlinux.org/man/connmanctl.1).
If you do not provide any commands `connmanctl` starts as an interactive shell.

*ConnMan* automatically handles wired connections.

### Wi-Fi

#### Enabling and disabling wifi

To check if wifi is enabled you can run `connmanctl technologies` and check for the line that says `Powered: True/False`.
To power the wifi on you can run `connmanctl enable wifi` or if you need to disable it you can run `connmanctl disable wifi`.
Other ways to enable wifi could include using the `Fn` keys on the laptop to turn it on or running `ip link set up`.

#### Connecting to an open access point

To scan the network `connmanctl` accepts simple names called *technologies*. To scan for nearby Wi-Fi networks:

    $ connmanctl scan wifi

To list the available networks found after a scan run (example output):

```
$ connmanctl services
```

```
*AO MyNetwork               wifi_dc85de828967_68756773616d_managed_psk
    OtherNET                wifi_dc85de828967_38303944616e69656c73_managed_psk 
    AnotherOne              wifi_dc85de828967_3257495245363836_managed_wep
    FourthNetwork           wifi_dc85de828967_4d7572706879_managed_wep
    AnOpenNetwork           wifi_dc85de828967_4d6568657272696e_managed_none
```

To connect to an open network, use the second field beginning with `wifi_`:

    $ connmanctl connect wifi_dc85de828967_4d6568657272696e_managed_none

**Tip:** Network names can be tab-completed.

You should now be connected to the network. Check using `connmanctl state` or `ip addr`.

#### Connecting to a protected access point

For protected access points you will need to provide some information to the ConnMan daemon, at the very least a password or a passphrase.

The commands in this section show how to run `connmanctl` in interactive mode, it is required for running the `agent` command. To start interactive mode simply type:

    $ connmanctl

You then proceed almost as above, first scan for any Wi-Fi *technologies*:

    connmanctl> scan wifi

To list services:

    connmanctl> services

Now you need to register the agent to handle user requests. The command is:

    connmanctl> agent on

You now need to connect to one of the protected services. To do this easily, just use tab completion for the wifi\_ service. If you were connecting to OtherNET in the example above you would type:

    connmanctl> connect wifi_dc85de828967_38303944616e69656c73_managed_psk

The agent will then ask you to provide any information the daemon needs to complete the connection. The
information requested will vary depending on the type of network you are connecting to. The agent
will also print additional data about the information it needs as shown in the example below.

    Agent RequestInput wifi_dc85de828967_38303944616e69656c73_managed_psk
      Passphrase = [ Type=psk, Requirement=mandatory ]
      Passphrase?  

Provide the information requested, in this example the passphrase, and then type:

    connmanctl> quit

If the information you provided is correct you should now be connected to the protected access point.

#### Using iwd instead of wpa\_supplicant

ConnMan can use [iwd](https://archlinux.org/packages/?name=iwd) to connect to wireless networks. The package which is available in community already supports using [iwd](https://archlinux.org/packages/?name=iwd) for connecting to wireless networks. As [connman](https://archlinux.org/packages/?name=connman) will start [wpa\_supplicant](https://archlinux.org/packages/?name=wpa_supplicant) when it finds it, it is recommended to uninstall [wpa\_supplicant](https://archlinux.org/packages/?name=wpa_supplicant).

Note that ConnMan is probably unnecessary for IWD users, as IWD can [handle its own network configuration](https://wiki.archlinux.org/title/ConnMan/title/Iwd#Enable_built-in_network_configuration "Iwd"), in which case `connmand` should be stopped.

Currently the `-i`-option of [iwd](https://archlinux.org/packages/?name=iwd) seems to cause that the WiFi-interface gets hidden from [connman](https://archlinux.org/packages/?name=connman).

Create the following service file which should cause [connman](https://archlinux.org/packages/?name=connman) to use [iwd](https://archlinux.org/packages/?name=iwd) to connect to wireless networks, regardless if [wpa\_supplicant](https://archlinux.org/packages/?name=wpa_supplicant) is installed.

```
/etc/systemd/system/connman_iwd.service
```

```
[Unit]
Description=Connection service
DefaultDependencies=false
Conflicts=shutdown.target
RequiresMountsFor=/var/lib/connman
After=dbus.service network-pre.target systemd-sysusers.service iwd.service
Before=network.target multi-user.target shutdown.target
Wants=network.target
Requires=iwd.service

[Service]
Type=dbus
BusName=net.connman
Restart=on-failure
ExecStart=/usr/bin/connmand –wifi=iwd_agent -n 
StandardOutput=null
CapabilityBoundingSet=CAP_NET_ADMIN CAP_NET_BIND_SERVICE CAP_NET_RAW CAP_SYS_TIME CAP_SYS_MODULE
ProtectHome=true
ProtectSystem=true

[Install]
WantedBy=multi-user.target
```

Then [enable](https://wiki.archlinux.org/title/ConnMan/title/Enable "Enable")/[start](https://wiki.archlinux.org/title/ConnMan/title/Start "Start") the `connman_iwd` service.

Advantage of using [iwd](https://archlinux.org/packages/?name=iwd) instead of [wpa\_supplicant](https://archlinux.org/packages/?name=wpa_supplicant) is, that the ping times seem to be much more consistent and the connection seems to be more reliable.

### Settings

Settings and profiles are automatically created for networks the user connects to often. They contain fields for the passphrase, essid and other information. Profile settings are stored in directories under `/var/lib/connman/` by their service name. To view all network profiles run this command from [root shell](https://wiki.archlinux.org/title/ConnMan/title/Help:Reading#Regular_user_or_root "Help:Reading"):

    # cat /var/lib/connman/*/settings

**Note:** VPN settings can be found in `/var/lib/connman-vpn/`.

### Technologies

Various hardware interfaces are referred to as *Technologies* by ConnMan.

To list available *technologies* run:

    $ connmanctl technologies

To get just the types by their name one can use this one liner:

    $ connmanctl technologies | awk '/Type/ { print $NF }'

**Note:** The field `Type = tech_name` provides the technology type used with `connmanctl` commands

To interact with them one must refer to the technology by type. *Technologies* can be toggled on/off with:

    $ connmanctl enable technology_type

and:

    $ connmanctl disable technology_type

For example to toggle off wifi:

    $ connmanctl disable wifi

**Warning:** connman grabs rfkill events. It is most likely impossible to use `rfkill` or `bluetoothctl` to (un)block devices, yet hardware keys may still work.[\[2\]](https://git.kernel.org/cgit/network/connman/connman.git/tree/doc/overview-api.txt#n406) Always use `connmanctl enable|disable`

## Tips and tricks

### Avoid changing the hostname

By default, ConnMan changes the transient hostname (see [hostnamectl(1)](https://man.archlinux.org/man/hostnamectl.1)) on a per network basis. This can create problems with X authority: If ConnMan changes your hostname to something else than the one used to generate the xauth magic cookie, then it will become impossible to create new windows. Symptoms are error messages like `No protocol specified` and `Can't open display: :0.0`. Manually resetting the host name fixes this, but a permanent solution is to prevent ConnMan from changing your host name in the first place. This can be accomplished by adding the following to `/etc/connman/main.conf`:

    [General]
    AllowHostnameUpdates=false

Make sure to [restart](https://wiki.archlinux.org/title/ConnMan/title/Restart "Restart") the `connman.service` after changing this file.

For testing purposes it is recommended to watch the [systemd journal](https://wiki.archlinux.org/title/ConnMan/title/Systemd_journal "Systemd journal") and plug the network cable a few times to see the action.

### Prefer ethernet to wireless

By default ConnMan does not prefer ethernet over wireless, which can lead to it deciding to stick with a slow wireless network even when ethernet is available. You can tell connman to prefer ethernet adding the following to `/etc/connman/main.conf`:

    [General]
    PreferredTechnologies=ethernet,wifi

### Exclusive connection

ConnMan allows you to be connected to both ethernet and wireless at the same time. This can be useful as it allows programs that established a connection over wifi to stay connected even after you connect to ethernet. But some people prefer to have only a single unambiguous connection active at a time. That behavior can be activated by adding the following to `/etc/connman/main.conf`:

    [General]
    SingleConnectedTechnology=true

### Connecting to eduroam (802.1X)

[WPA2 Enterprise](https://wiki.archlinux.org/title/ConnMan/title/WPA2_Enterprise "WPA2 Enterprise") networks such as eduroam require a separate configuration file before [connecting](https://wiki.archlinux.org/title/ConnMan#Wi-Fi) to the network. For example, create `/var/lib/connman/eduroam.config`:

```
eduroam.config
```

```
[service_eduroam]
Type=wifi
Name=eduroam
EAP=peap
CACertFile=/etc/ssl/certs/certificate.cer
Phase2=MSCHAPV2
Identity=user@foo.edu
AnonymousIdentity=anonymous@foo.edu
Passphrase=password
```

[Restart](https://wiki.archlinux.org/title/ConnMan/title/Restart "Restart") `wpa_supplicant.service` and `connman.service` to connect to the new network.

**Note:**

-   Options are case-sensitive, e.g. `EAP = ttls` instead of `EAP = TTLS`.[\[3\]](https://together.jolla.com/question/55969/connman-fails-due-to-case-sensitive-settings/)
-   Consult the institution hosting the eduroam network for various settings such as username, password, `EAP`, `Phase2output`, and needed certificates.

For more information, see [connman-service.config(5)](https://man.archlinux.org/man/connman-service.config.5) and [Wireless network configuration#eduroam](https://wiki.archlinux.org/title/ConnMan/title/Wireless_network_configuration#eduroam "Wireless network configuration").

### Avoiding conflicts with local DNS server

If you are running a local DNS server, it will likely have problems binding to port 53 (TCP and/or UDP) after installing Connman. This is because Connman includes its own DNS proxy which also tries to bind to those ports. If you see log messages from [BIND](https://wiki.archlinux.org/title/ConnMan/title/BIND "BIND") or [dnsmasq](https://wiki.archlinux.org/title/ConnMan/title/Dnsmasq "Dnsmasq") like

    named[529]: could not listen on UDP socket: address in use

this could be the problem. To verify which application is listening on the ports, you can execute `ss -tulpn` as root.

To fix this connmand can be started with the options `-r` or `–nodnsproxy` by [overriding](https://wiki.archlinux.org/title/ConnMan/title/Systemd#Editing_provided_units "Systemd") the systemd service file. Create the folder `/etc/systemd/system/connman.service.d/` and add the file `disable_dns_proxy.conf`:

```
/etc/systemd/system/connman.service.d/disable_dns_proxy.conf
```

```
[Service]
ExecStart=
ExecStart=/usr/bin/connmand -n –nodnsproxy
```

Make sure to [reload](https://wiki.archlinux.org/title/ConnMan/title/Reload "Reload") the systemd daemon and [restart](https://wiki.archlinux.org/title/ConnMan/title/Restart "Restart") the `connman.service`, and your DNS proxy, after adding this file.

### /etc/resolv.conf

If you want to know the DNS servers received from DHCP while keeping a custom `/etc/resolv.conf`, then append `RuntimeDirectory=connman` to the above file (clear the `ExecStart` lines if not needed). Now connman will write them to `/var/run/connman/resolv.conf` instead.

### Blacklist interfaces

If something like [Docker](https://wiki.archlinux.org/title/ConnMan/title/Docker "Docker") is creating virtual interfaces Connman may attempt to connect to one of these instead of your physical adapter if the connection drops. A simple way of avoiding this is to blacklist the interfaces you do not want to use. Connman will by default blacklist interfaces starting with `vmnet`, `vboxnet`, `virbr` and `ifb`, so those need to be included in the new blacklist as well.

Blacklisting interface names is also useful to avoid a race condition where connman may access `eth#` or `wlan#` before systemd/udev can change it to use a [Predictable Network Interface Names](https://systemd.io/PREDICTABLE_INTERFACE_NAMES/) like `enp4s0`. Blacklisting the conventional (and unpredictable) interface prefixes makes connman wait until they are renamed.

If it does not already exist, create `/etc/connman/main.conf`:

    [General]
    NetworkInterfaceBlacklist=vmnet,vboxnet,virbr,ifb,docker,veth,eth,wlan

Once `connman.service` has been [restarted](https://wiki.archlinux.org/title/ConnMan/title/Systemd#Using_units "Systemd") this will also hide all the `veth#######` interfaces from GUI tools like Econnman.

## Troubleshooting

### Error /net/connman/technology/wifi: Not supported

Currently, connman does not support scanning for WiFi networks with [iwd](https://archlinux.org/packages/?name=iwd), at the moment this functionality is available with `wpa_supplicant` only (see [\[4\]](https://lists.01.org/pipermail/connman/2018-August/022915.html)). To connect to wifi with iwd, [enable](https://wiki.archlinux.org/title/ConnMan/title/Enable "Enable")/[start](https://wiki.archlinux.org/title/ConnMan/title/Start "Start") `iwd.service` and then either follow instructions in [Iwd](https://wiki.archlinux.org/title/ConnMan/title/Iwd "Iwd") to connect to the wifi or you can also use any of the [\#Front-ends](https://wiki.archlinux.org/title/ConnMan#Front-ends). In order to have Wifi Scanning support from within connman, install [wpa\_supplicant](https://archlinux.org/packages/?name=wpa_supplicant) and then [restart](https://wiki.archlinux.org/title/ConnMan/title/Restart "Restart") `connman.service` after you stop `iwd.service`.

### Error /net/connman/technology/wifi: No carrier

You have enabled your wifi with:

    $ connmanctl enable wifi

If wireless scanning leads to above error, this may be due to an unresolved bug.[\[5\]](https://01.org/jira/browse/CM-670)^\[[dead\ link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot")\ 2022-09-17 ⓘ\]^
If it does not resolve even though wireless [preconditions](https://lists.01.org/pipermail/connman/2014-December/019203.html) are met, try again after disabling competing network managers and rebooting.

This may also simply be caused by the wireless interface being blocked by [rfkill](https://wiki.archlinux.org/title/ConnMan/title/Rfkill "Rfkill"), which can occur after restarting wpa\_supplicant. Use `rfkill list` to check.

### "Not registered", or "Method "Connect" with signature ... doesn't exist"

When issuing commands, you may see errors like the following:

From a `connmanctl` prompt:

```
connmanctl> connect service_id
```

```
Error /net/connman/service/SSID: Method "Connect" with signature "" on interface "net.connman.Service" doesn't exist
```

From the shell:

```
# connmanctl connect service_id
```

```
Error /net/connman/service/service_id: Not registered
```

These errors are produced because the agent is not running. Start the agent from a `connmanctl` prompt with `agent on`, and try again.

### Error Failed to set hostname/domainname

connman can failed to set hostname or domainname due to lack of `CAP_SYS_ADMIN`.

You will need to [edit](https://wiki.archlinux.org/title/ConnMan/title/Edit "Edit") `connman.service` (and other like `connman-vpn.service` , etc ...) to modify the `CapabilityBoundingSet` line to add `CAP_SYS_ADMIN`.

See `EPERM` under [sethostname(2) § ERRORS](https://man.archlinux.org/man/sethostname.2#ERRORS) or [setdomainname(2) § ERRORS](https://man.archlinux.org/man/setdomainname.2#ERRORS) for more details.

### Unknown route on connection

A log entry for an unknown route appears each time a connect is done. For example:

    ...
    connmand[473]: wlp2s0 {add} route 82.165.8.211 gw 10.20.30.4 scope 0 
    connmand[473]: wlp2s0 {del} route 82.165.8.211 gw 10.20.30.4 scope 0 
    ...

It likely is Connman performing a connectivity check to the ipv4.connman.net host (which resolves to the IP address `82.165.8.211` at current).[\[6\]](https://01.org/jira/browse/CM-657)^\[[dead\ link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot")\ 2022-09-17 ⓘ\]^ See the [Connman README](https://git.kernel.org/pub/scm/network/connman/connman.git/tree/README#n388) for more information on why and what - apart from the connecting IP - it transmits.
This behaviour can be prevented by adding the following to `/etc/connman/main.conf`:

    [General]
    EnableOnlineCheck=false

This setting will cause that the default device will not switch to ONLINE, but stay in READY state.[connman.conf(5)](https://man.archlinux.org/man/connman.conf.5) However, the connection will still be functional.

The connection itself is also functional (unless behind a captive portal) if the check is blocked by a firewall rule:

    # ip6tables -A OUTPUT -d ipv6.connman.net -j REJECT
    1. iptables -A OUTPUT -d ipv4.connman.net,ipv6.connman.net -j REJECT

### File /proc/net/pnp doesn't exist

If you see this in your error log it is caused by bug in connman [\[7\]](https://bbs.archlinux.org/viewtopic.php?id=227689#p1766928) and can be ignored. [Bug Report](https://01.org/jira/browse/CM-690)^\[[dead\ link](https://en.wikipedia.org/wiki/Wikipedia:Link_rot "wikipedia:Wikipedia:Link rot")\ 2022-09-17 ⓘ\]^

## See also

-   [Git repository documentation](https://git.kernel.org/cgit/network/connman/connman.git/tree/doc) — for further detailed documentation