https://wiki.libreelec.tv/configuration/wireguard

# WireGuard

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE4cHg7IGhlaWdodDogMThweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgZGF0YS1ybndpYnV0dG9uLTFibmowMTgtaG92ZXItZm9jdXM9InRydWUiIHByZXNlcnZlYXNwZWN0cmF0aW89InhNaWRZTWlkIG1lZXQiIGZpbGw9Im5vbmUiIHZpZXdib3g9IjAgMCAxNiAxNiI+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTggNGExIDEgMCAxMDAtMiAxIDEgMCAwMDAgMnpNOCA4Ljc1YTEgMSAwIDEwMC0yIDEgMSAwIDAwMCAyek04IDEzLjVhMSAxIDAgMTAwLTIgMSAxIDAgMDAwIDJ6IiAvPjwvc3ZnPg==)

LibreELEC can be configured as a WireGuard VPN client allowing you to accessing media in a remote location or tunnel traffic to avoid local inspection of network activity. This guide assumes configuration of a single WireGuard tunnel that is persistent, i.e. activated on device boot so that Kodi network traffic is routed through the WireGuard VPN tunnel.

WireGuard tunnels are managed by a ConnMan VPN plugin (connman-vpn.service) that acts as a companion to the network connection manager daemon (connman.service). The VPN plugin watches `/storage/.config/wireguard/*.config` and definea ConnMan services from auto-discovered configuration files. Once a valid WireGuard .config has been imported it can be connected manually using `connmanctl` from the SSH console or scripted from a systemd service that runs on boot. Connections can also be managed using the network 'Connections' tab in the LibreELEC settings add-on which controls ConnMan via d-bus.

## 

Sample Config[![](data:image/svg+xml;base64,PHN2ZyBkYXRhLWRhcmtyZWFkZXItaW5saW5lLXN0cm9rZSBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDIwcHg7IGhlaWdodDogMjBweDsg4oCTZGFya3JlYWRlci1pbmxpbmUtc3Ryb2tlOmN1cnJlbnRDb2xvcjsiIHJvbGU9InByZXNlbnRhdGlvbiIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZT0iY3VycmVudENvbG9yIiBmaWxsPSJub25lIiB2aWV3Ym94PSIwIDAgMjQgMjQiPjxwYXRoIGQ9Ik00IDloMTZNNCAxNWgxNk0xMCAzTDggMjFNMTYgM2wtMiAxOCIgLz48L3N2Zz4=)](https://wiki.libreelec.tv/configuration/wireguard#sample-config)

ConnMan uses its own configuration file format (see below) so you cannot import/use the files exported from WireGuard server tools and third-party VPN services - the format is different. Those files will contain everything you need, but you must manually transpose the information into the ConnMan format:

\[provider\_wireguard\]

Type = WireGuard

Name = WireGuard (Home)

Host = 185.210.30.121

WireGuard.Address = 10.2.0.2/24

WireGuard.ListenPort = 51820

WireGuard.PrivateKey = qKIj010hDdWSjQQyVCnEgthLXusBgm3I6HWrJUaJymc=

WireGuard.PublicKey = zzqUfWGIil6QxrAGz77HE5BGUEdD2PgHYnCg3CDKagE=

WireGuard.PresharedKey = DfEYeVs04HS9XhKGM4/ZXHG3Qc4MFK2AJd8XouYDbRQ=

WireGuard.DNS = 8.8.8.8, 1.1.1.1

WireGuard.AllowedIPs = 0.0.0.0/0

WireGuard.EndpointPort = 51820

WireGuard.PersistentKeepalive = 25

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

Name = AnythingYouLike Host = IP of the WireGuard **server** WireGuard.Address = The internal IP of the **client** node, e.g. a /24 address WireGuard.ListenPort = The **client** listen port (optional) WireGuard.PrivateKey = The **client** private key WireGuard.PublicKey = The **server** public key WireGuard.PresharedKey = The **server** pre-shared key (optional) WireGuard.DNS = Nameserver to be used with the connection (optional) WireGuard.AllowedIPs = Subnets accessed via the tunnel, 0.0.0.0/0 is "route all traffic" WireGuard.EndpointPort = The **server** ListenPort WireGuard.PersistentKeepalive = Periodic keepalive in seconds (optional)

## 

Creating Keys[![](data:image/svg+xml;base64,PHN2ZyBkYXRhLWRhcmtyZWFkZXItaW5saW5lLXN0cm9rZSBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDIwcHg7IGhlaWdodDogMjBweDsg4oCTZGFya3JlYWRlci1pbmxpbmUtc3Ryb2tlOmN1cnJlbnRDb2xvcjsiIHJvbGU9InByZXNlbnRhdGlvbiIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZT0iY3VycmVudENvbG9yIiBmaWxsPSJub25lIiB2aWV3Ym94PSIwIDAgMjQgMjQiPjxwYXRoIGQ9Ik00IDloMTZNNCAxNWgxNk0xMCAzTDggMjFNMTYgM2wtMiAxOCIgLz48L3N2Zz4=)](https://wiki.libreelec.tv/configuration/wireguard#creating-keys)

If you need to create some, run `wg-keygen` from the SSH console and `/storage/.cache/wireguard` will contain new publickey, privatekey, and preshared files with keys inside. Most users will not need to generate WireGuard keys as they will be in the configuration file provided by a VPN service provider.

## 

Testing Connections[![](data:image/svg+xml;base64,PHN2ZyBkYXRhLWRhcmtyZWFkZXItaW5saW5lLXN0cm9rZSBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDIwcHg7IGhlaWdodDogMjBweDsg4oCTZGFya3JlYWRlci1pbmxpbmUtc3Ryb2tlOmN1cnJlbnRDb2xvcjsiIHJvbGU9InByZXNlbnRhdGlvbiIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZT0iY3VycmVudENvbG9yIiBmaWxsPSJub25lIiB2aWV3Ym94PSIwIDAgMjQgMjQiPjxwYXRoIGQ9Ik00IDloMTZNNCAxNWgxNk0xMCAzTDggMjFNMTYgM2wtMiAxOCIgLz48L3N2Zz4=)](https://wiki.libreelec.tv/configuration/wireguard#testing-connections)

Once you have saved a configuration file, check it is valid:

RPi4:~ \# connmanctl services

\* R home vpn\_185\_210\_30\_121

\*AO Wired ethernet\_dca622135939\_cable

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

In the above example `vpn_185_210_30_121` was created (vpn\_host) as the ConnMan service name. Test the service will connect using:

RPi4:~ \# connmanctl connect vpn\_185\_210\_30\_121

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

ConnMan will create a new network interface, so `ifconfig` will show `wg0` or sometimes a higer number like `wg1` or `wg2`:

RPi4:~ \# ifconfig

eth0 Link encap:Ethernet HWaddr DC:A6:32:13:26:3b

inet addr:192.168.10.25 Bcast:192.168.10.255 Mask:255.255.255.0

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:3136938 errors:0 dropped:40816 overruns:0 frame:0

TX packets:242506 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:1000

RX bytes:310409413 (296.0 MiB) TX bytes:22433323 (21.3 MiB)

​

lo Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0.0

inet6 addr: ::1/128 Scope:Host

UP LOOPBACK RUNNING MTU:65536 Metric:1

RX packets:6109 errors:0 dropped:0 overruns:0 frame:0

TX packets:6109 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:1000

RX bytes:415013 (405.2 KiB) TX bytes:415013 (405.2 KiB)

​

wg0 Link encap:UNSPEC HWaddr 00-00-00-00-00-00-00-00-00-00-00-00-00-00-00-00

inet addr:10.2.0.2 P-t-P:10.2.0.2 Mask:255.255.255.0

UP POINTOPOINT RUNNING NOARP MTU:1420 Metric:1

RX packets:13744 errors:0 dropped:0 overruns:0 frame:0

TX packets:11080 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueuelen:1000

RX bytes:13775220 (13.1 MiB) TX bytes:1232552 (1.1 MiB)

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

You should be able to `ping` the remote (server) side of the WireGuard VPN tunnel. In our example this is 10.2.0.1:

RPi4:~ \# ping 10.2.0.1

PING 10.2.0.1 (10.2.0.1): 56 data bytes

64 bytes from 10.2.0.1: seq=0 ttl=64 time=147.936 ms

64 bytes from 10.2.0.1: seq=1 ttl=64 time=147.955 ms

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

The routing table will show normal traffic routed to the wg0 interface:

RPi4:~ \# route

Kernel IP routing table

Destination Gateway Genmask Flags Metric Ref Use Iface

default \* 0.0.0.0 U 0 0 0 wg0

1.1.1.1 \* 255.255.255.255 UH 0 0 0 wg0

8.8.8.8 \* 255.255.255.255 UH 0 0 0 wg0

10.2.0.0 \* 255.255.255.0 U 0 0 0 wg0

192.168.10.0 \* 255.255.255.0 U 0 0 0 eth0

192.168.10.1 \* 255.255.255.255 UH 0 0 0 eth0

185.210.30.121 192.168.10.1 255.255.255.255 UGH 0 0 0 eth0

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

To disconnect the ConnMan service:

RPi4:~ \# connmanctl disconnect vpn\_185\_210\_30\_121

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

Check `ifconfig` again and the WireGuard interface will be gone.

## 

Configuring Systemd[![](data:image/svg+xml;base64,PHN2ZyBkYXRhLWRhcmtyZWFkZXItaW5saW5lLXN0cm9rZSBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDIwcHg7IGhlaWdodDogMjBweDsg4oCTZGFya3JlYWRlci1pbmxpbmUtc3Ryb2tlOmN1cnJlbnRDb2xvcjsiIHJvbGU9InByZXNlbnRhdGlvbiIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZT0iY3VycmVudENvbG9yIiBmaWxsPSJub25lIiB2aWV3Ym94PSIwIDAgMjQgMjQiPjxwYXRoIGQ9Ik00IDloMTZNNCAxNWgxNk0xMCAzTDggMjFNMTYgM2wtMiAxOCIgLz48L3N2Zz4=)](https://wiki.libreelec.tv/configuration/wireguard#configuring-systemd)

Create a systemd wireguard.service file to start the connection automatically on boot, after the network starts, and before Kodi is launched. The sample wireguard.service file looks like:

\[Unit\]

Description=WireGuard VPN Service

After=network-online.target nss-lookup.target wait-time-sync.service connman-vpn.service

Before=kodi.service

​

\[Service\]

Type=oneshot

RemainAfterExit=yes

ExecStart=/usr/bin/connmanctl connect vpn\_service\_name\_goes\_here

ExecStop=/usr/bin/connmanctl disconnect vpn\_service\_name\_goes\_here

​

\[Install\]

WantedBy=multi-user.target

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

Copy the sample wireguard.service file to `/storage/.config/system.d/wireguard.service`

cp /storage/.config/system.d/wireguard.service.sample /storage/.config/system.d/wireguard.service

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

Replace **vpn\_service\_name\_goes\_here** with your service name, e.g. `vpn_185_210_30_121` using nano. Use `ctrl+o` to save changes and `ctrl+x` to exit nano:

nano /storage/.config/system.d/wireguard.service

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

Now we can enable and start the service:

RPi4:~ \# systemctl enable /storage/.config/system.d/wireguard.service

Created symlink /storage/.config/system.d/multi-user.target.wants/wireguard.service → /storage/.config/system.d/wireguard.service.

RPi4:~ \# systemctl start wireguard.service

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

Check the WireGuard tunnel is active using "ifconfig" and "ping" and if all is good, reboot to test the WireGuard tunnel comes up automatically on boot.

## 

Known Issues[![](data:image/svg+xml;base64,PHN2ZyBkYXRhLWRhcmtyZWFkZXItaW5saW5lLXN0cm9rZSBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDIwcHg7IGhlaWdodDogMjBweDsg4oCTZGFya3JlYWRlci1pbmxpbmUtc3Ryb2tlOmN1cnJlbnRDb2xvcjsiIHJvbGU9InByZXNlbnRhdGlvbiIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgc3Ryb2tlLWxpbmVqb2luPSJyb3VuZCIgc3Ryb2tlLWxpbmVjYXA9InJvdW5kIiBzdHJva2Utd2lkdGg9IjIiIHN0cm9rZT0iY3VycmVudENvbG9yIiBmaWxsPSJub25lIiB2aWV3Ym94PSIwIDAgMjQgMjQiPjxwYXRoIGQ9Ik00IDloMTZNNCAxNWgxNk0xMCAzTDggMjFNMTYgM2wtMiAxOCIgLz48L3N2Zz4=)](https://wiki.libreelec.tv/configuration/wireguard#known-issues)

ConnMan makes wg0 route all traffic over the WireGuard tunnel by default, no matter what `WireGuard.AllowedIPs` configuration you set. To route only specific networks via the tunnel the ConnMan service order (which influences routing order) must be changed.

Note the`sleep` and `connmanctl move-after` and `route add` commands used in the following tweaked systemd service file:

\[Unit\]

Description=WireGuard VPN Service

After=network-online.target nss-lookup.target connman.service connman-vpn.service bluetooth.service

Wants=network-online.target nss-lookup.target connman.service connman-vpn.service bluetooth.service

​

\[Service\]

Type=oneshot

RemainAfterExit=yes

ExecStart=/bin/sleep 5

ExecStart=/usr/bin/connmanctl connect vpn\_X\_klaus

ExecStart=/usr/bin/connmanctl move-after vpn\_X\_klaus ethernet\_b827eb10c45a\_cable

ExecStart=/usr/bin/connmanctl move-after vpn\_X\_klaus ethernet\_b827eb10c45a\_cable

ExecStart=/usr/sbin/route add -net 192.168.2.0 netmask 255.255.255.0 gw 10.0.0.2

ExecStop=/usr/bin/connmanctl disconnect vpn\_X\_klaus

​

\[Install\]

WantedBy=multi-user.target

![](data:image/svg+xml;base64,PHN2ZyBzdHlsZT0idmVydGljYWwtYWxpZ246IG1pZGRsZTsgd2lkdGg6IDE0cHg7IGhlaWdodDogMTRweDsiIGNsYXNzPSJyLWg3Z2RvYiIgZGF0YS1ybndpLWhhbmRsZT0ibmVhcmVzdCIgcHJlc2VydmVhc3BlY3RyYXRpbz0ieE1pZFlNaWQgbWVldCIgZmlsbD0ibm9uZSIgdmlld2JveD0iMCAwIDE2IDE2Ij48cGF0aCBzdHlsZT0i4oCTZGFya3JlYWRlci1pbmxpbmUtZmlsbDpjdXJyZW50Q29sb3I7IiBkYXRhLWRhcmtyZWFkZXItaW5saW5lLWZpbGwgZmlsbD0iY3VycmVudENvbG9yIiBkPSJNMCAuNUEuNS41IDAgMDEuNSAwaDEwYS41LjUgMCAwMS41LjVWNGgtMVYxSDF2OWgzdjFILjVhLjUuNSAwIDAxLS41LS41Vi41eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PHBhdGggc3R5bGU9IuKAk2RhcmtyZWFkZXItaW5saW5lLWZpbGw6Y3VycmVudENvbG9yOyIgZGF0YS1kYXJrcmVhZGVyLWlubGluZS1maWxsIGZpbGw9ImN1cnJlbnRDb2xvciIgZD0iTTUgNS41YS41LjUgMCAwMS41LS41aDEwYS41LjUgMCAwMS41LjV2MTBhLjUuNSAwIDAxLS41LjVoLTEwYS41LjUgMCAwMS0uNS0uNXYtMTB6TTYgNnY5aDlWNkg2eiIgY2xpcC1ydWxlPSJldmVub2RkIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiIC8+PC9zdmc+)

The following forum thread has tips and examples: [https://forum.libreelec.tv/thread/21906-wireguard-changes-the-default-route-although-not-configured/](https://forum.libreelec.tv/thread/21906-wireguard-changes-the-default-route-although-not-configured/)

## 

Thanks