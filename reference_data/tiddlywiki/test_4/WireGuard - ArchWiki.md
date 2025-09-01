https://wiki.archlinux.org/title/WireGuard


							

				From ArchWiki

Related articles

-   [Linux Containers/Using VPNs](https://wiki.archlinux.org/title/WireGuard/title/Linux_Containers/Using_VPNs "Linux Containers/Using VPNs")

From the [WireGuard](https://www.wireguard.com/) project homepage:

WireGuard is an extremely simple yet fast and modern VPN that utilizes state-of-the-art cryptography. It aims to be faster, simpler, leaner, and more useful than IPsec, while avoiding the massive headache. It intends to be considerably more performant than OpenVPN. WireGuard is designed as a general purpose VPN for running on embedded interfaces and super computers alike, fit for many different circumstances. Initially released for the Linux kernel, it is now cross-platform (Windows, macOS, BSD, iOS, Android) and widely deployable.

A rough introduction to the main concepts used in this article can be found on [WireGuard's](https://www.wireguard.com/) project homepage. WireGuard has been included in the [Linux kernel](https://git.kernel.org/pub/scm/linux/kernel/git/torvalds/linux.git/commit/?id=e7096c131e5161fa3b8e52a650d7719d2857adfd) since late 2019.

## Installation

[Install](https://wiki.archlinux.org/title/WireGuard/title/Install "Install") the [wireguard-tools](https://archlinux.org/packages/?name=wireguard-tools) package for userspace utilities.

Alternatively, various network managers provide support for WireGuard, provided that peer keys are available. See [#Persistent configuration](https://wiki.archlinux.org/title/WireGuard#Persistent_configuration) for details.

### Graphical clients

-   **Qomui** — OpenVPN GUI with advanced features and support for multiple providers.

[https://github.com/corrad1nho/qomui](https://github.com/corrad1nho/qomui) \|\| [qomui](https://aur.archlinux.org/packages/qomui/)^AUR^

### Command-line tools

-   **wg\_tool** — Tool to manage wireguard configs for server and users.

[https://github.com/gene-git/wg\_tool](https://github.com/gene-git/wg_tool) \|\| [wg\_tool](https://aur.archlinux.org/packages/wg_tool/)^AUR^

## Usage

[![Tango-edit-clear.png](https://wiki.archlinux.org/images/8/87/Tango-edit-clear.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-edit-clear.png)**This article or section needs language, wiki syntax or style improvements. See [Help:Style](https://wiki.archlinux.org/title/WireGuard/title/Help:Style "Help:Style") for reference.**[![Tango-edit-clear.png](https://wiki.archlinux.org/images/8/87/Tango-edit-clear.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-edit-clear.png)

**Reason:** Useless section name – everything on this page is about WireGuard usage. Moving the 4 subsections to the top level would make sense. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

The commands below demonstrate how to set up a basic tunnel between two or more peers with the following settings:

|  | External (public) addresses |  |  | Internal IP addresses |  | Port |
|----|----|----|----|----|----|----|
| Domain name | IPv4 address | IPv6 address | IPv4 address | IPv6 address |  |  |
| Peer A |  | 198.51.100.101 | 2001:db8:a85b:70a:ffd4:ec1b:4650:a001 | 10.0.0.1/24 | fdc9:281f:04d7:9ee9::1/64 | UDP/51871 |
| Peer B | peer-b.example | 203.0.113.102 | 2001:db8:40f0:147a:80ad:3e88:f8e9:b002 | 10.0.0.2/24 | fdc9:281f:04d7:9ee9::2/64 | UDP/51902 |
| Peer C |  | *dynamic* | *dynamic* | 10.0.0.3/24 | fdc9:281f:04d7:9ee9::3/64 | UDP/51993 |

**Tip:** The same UDP port can be used for all peers.

The external addresses should already exist. For example, if ICMP echo requests are not blocked, peer A should be able to [ping](https://wiki.archlinux.org/title/WireGuard/title/Ping "Ping") peer B via its public IP address(es) and vice versa.

The internal addresses will be new addresses, created either manually using the [ip(8)](https://man.archlinux.org/man/ip.8) utility or by network management software, which will be used internally within the new WireGuard network. The following examples will use 10.0.0.0/24 and fdc9:281f:04d7:9ee9::/64 as the internal network. The `/24` and `/64` in the IP addresses is the [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation "wikipedia:Classless Inter-Domain Routing").

### Key generation

Create a private and public key for each peer. If connecting dozens of peers optionally consider a vanity keypair to personalize the Base64 encoded public key string. See [#Vanity keys](https://wiki.archlinux.org/title/WireGuard#Vanity_keys).

To create a private key run:

    $ (umask 0077; wg genkey > peer_A.key)

**Note:** It is recommended to only allow reading and writing access for the owner. The above alters the [umask](https://wiki.archlinux.org/title/WireGuard/title/Umask "Umask") temporarily within a sub-shell to ensure that access (read/write permissions) is restricted to the owner.

To create a public key:

    $ wg pubkey < peer_A.key > peer_A.pub

Alternatively, do this all at once:

    $ wg genkey | (umask 0077 && tee peer_A.key) | wg pubkey > peer_A.pub

One can also generate a pre-shared key to add an additional layer of symmetric-key cryptography to be mixed into the already existing public-key cryptography, for post-quantum resistance. A pre-shared key should be generated for each peer pair and should not be reused. For example, three interconnected peers, A, B, and, C will need three separate pre-shared keys, one for each peer pair.

Generate a pre-shared key for each peer pair using the following command (make sure to use `umask 0077` for this as well):

    $ wg genpsk > peer_A-peer_B.psk
    $ wg genpsk > peer_A-peer_C.psk
    $ wg genpsk > peer_B-peer_C.psk

#### Vanity keys

Currently, WireGuard does not support comments or attaching human-memorable names to keys. This makes identifying the key's owner difficult particularly when multiple keys are in use. One solution is to generate a public key that contains some familiar characters (perhaps the first few letters of the owner's name or of the hostname etc.), [wireguard-vanity-address](https://aur.archlinux.org/packages/wireguard-vanity-address/)^AUR^ does this.

For example:

```
$ wireguard-vanity-address –in 8 leslie
```

```
searching for 'leslie' in pubkey[0..10], one of every 214748364 keys should match
one core runs at 2.69e6 keys/s, CPU cores available: 16
est yield: 5.0 seconds per key, 200.10e-3 keys/s
hit Ctrl-C to stop
private wEoVMj92P+E3fQXVf9IixWJqpCqcnP/4OfvrB1g3zmY=  public LEsliEny+aMcWcRbh8Qf414XsQHSBOAFk3TaEk/aSD0=
private EAOwlGGqpHVbZ9ehaCspdBJt+lkMcCfkwiA5T5a4JFs=  public VlesLiEB5BFd//OD2ILKXviolfz+hodG6uZ+XjoalC8=
private UDWG4VWI+RzAGzNSnlC+0X4d3nk9goWPs/NRC5tX524=  public 9lESlieIFOlJFV6dG7Omao2WS+amWgshDdBYn8ahRjo=
```

### Manual configuration

#### Peer setup

Manual setup is accomplished by using [ip(8)](https://man.archlinux.org/man/ip.8) and [wg(8)](https://man.archlinux.org/man/wg.8).

[![Tango-edit-clear.png](https://wiki.archlinux.org/images/8/87/Tango-edit-clear.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-edit-clear.png)**This article or section needs language, wiki syntax or style improvements. See [Help:Style](https://wiki.archlinux.org/title/WireGuard/title/Help:Style "Help:Style") for reference.**[![Tango-edit-clear.png](https://wiki.archlinux.org/images/8/87/Tango-edit-clear.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-edit-clear.png)

**Reason:** These examples use the pre-shared keys which were introduced as *optional* in [#Key generation](https://wiki.archlinux.org/title/WireGuard#Key_generation). (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

**Peer A setup:**

In this example peer A will listen on UDP port 51871 and will accept connection from peer B and C.

    # ip link add dev wg0 type wireguard
    1. ip addr add 10.0.0.1/24 dev wg0
    1. ip addr add fdc9:281f:04d7:9ee9::1/64 dev wg0
    1. wg set wg0 listen-port 51871 private-key /path/to/peer_A.key
    1. wg set wg0 peer PEER_B_PUBLIC_KEY preshared-key /path/to/peer_A-peer_B.psk endpoint peer-b.example:51902 allowed-ips 10.0.0.2/32,fdc9:281f:04d7:9ee9::2/128
    1. wg set wg0 peer PEER_C_PUBLIC_KEY preshared-key /path/to/peer_A-peer_C.psk allowed-ips 10.0.0.3/32,fdc9:281f:04d7:9ee9::3/128
    1. ip link set wg0 up

*`PEER_X_PUBLIC_KEY`* should be the contents of *`peer_X`*`.pub`.

The keyword `allowed-ips` is a list of addresses that will get routed to the peer. Make sure to specify at least one address range that contains the WireGuard connection's internal IP address(es).

**Peer B setup:**

    # ip link add dev wg0 type wireguard
    1. ip addr add 10.0.0.2/24 dev wg0
    1. ip addr add fdc9:281f:04d7:9ee9::2/64 dev wg0
    1. wg set wg0 listen-port 51902 private-key /path/to/peer_B.key
    1. wg set wg0 peer PEER_A_PUBLIC_KEY preshared-key /path/to/peer_A-peer_B.psk endpoint 198.51.100.101:51871 allowed-ips 10.0.0.1/32,fdc9:281f:04d7:9ee9::1/128
    1. wg set wg0 peer PEER_C_PUBLIC_KEY preshared-key /path/to/peer_B-peer_C.psk allowed-ips 10.0.0.3/32,fdc9:281f:04d7:9ee9::3/128
    1. ip link set wg0 up

**Peer C setup:**

    # ip link add dev wg0 type wireguard
    1. ip addr add 10.0.0.3/24 dev wg0
    1. ip addr add fdc9:281f:04d7:9ee9::3/64 dev wg0
    1. wg set wg0 listen-port 51993 private-key /path/to/peer_C.key
    1. wg set wg0 peer PEER_A_PUBLIC_KEY preshared-key /path/to/peer_A-peer_C.psk endpoint 198.51.100.101:51871 allowed-ips 10.0.0.1/32,fdc9:281f:04d7:9ee9::1/128
    1. wg set wg0 peer PEER_B_PUBLIC_KEY preshared-key /path/to/peer_B-peer_C.psk endpoint peer-b.example:51902 allowed-ips 10.0.0.2/32,fdc9:281f:04d7:9ee9::2/128
    1. ip link set wg0 up

#### Additional routes

To establish connections more complicated than point-to-point, additional setup is necessary.

[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)**This article or section needs expansion.**[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)

**Reason:** Add a scenario: only peer A has a public IP address (i.e. *endpoint*), peers B and C (which are generally behind a NAT) connect to peer A with `PersistentKeepalive`, connections from peer B to peer C and vice versa are routed via peer A. Configuration: peers B and C have `10.0.0.0/24` in `AllowedIPs` for peer A, peer A must enable packet forwarding and masquerading via firewall rules, e.g. `iptables -A FORWARD -i wg+ -j ACCEPT` and `iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o wg0 -j MASQUERADE`. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

##### Point-to-site

To access the network of a peer, specify the network subnet(s) in `allowed-ips` in the configuration of the peers who should be able to connect to it. E.g. `allowed-ips 10.0.0.2/32,fdc9:281f:04d7:9ee9::2/128,`**`192.168.35.0/24,fd7b:d0bd:7a6e::/64`**.

Make sure to also set up the [routing table](https://wiki.archlinux.org/title/WireGuard/title/Network_configuration#Routing_table "Network configuration") with [ip-route(8)](https://man.archlinux.org/man/ip-route.8). E.g.:

    # ip route add 192.168.35.0/24 dev wg0
    1. ip route add fd7b:d0bd:7a6e::/64 dev wg0

##### Site-to-point

[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)**This article or section needs expansion.**[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)

**Reason:** Add `ip route` examples; add alternative using NAT; mention the situation when the *site*-peer is the network's gateway. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

If the intent is to connect a device to a network with WireGuard peer(s), set up routes on each device so they know that the peer(s) are reachable via the device.

**Tip:** Deploy routes network-wide by configuring them in the router.

Enable IP forwarding on the peer through which other devices on the network will connect to WireGuard peer(s):

    # sysctl -w net.ipv4.ip_forward=1
    1. sysctl -w net.ipv6.conf.all.forwarding=1

**Warning:** Enabling IP forwarding without a properly configured [firewall](https://wiki.archlinux.org/title/WireGuard/title/Firewall "Firewall") is a security risk.

See [sysctl#Configuration](https://wiki.archlinux.org/title/WireGuard/title/Sysctl#Configuration "Sysctl") for instructions on how to set the *sysctl* parameters on boot.

##### Site-to-site

To connect two (or more) networks, apply both [#Point-to-site](https://wiki.archlinux.org/title/WireGuard#Point-to-site) and [#Site-to-point](https://wiki.archlinux.org/title/WireGuard#Site-to-point) on all *sites*.

##### Routing all traffic over WireGuard

[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)**This article or section needs expansion.**[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)

**Reason:** Add instructions on how to *route everything over VPN*.[\[1\]](https://www.wireguard.com/netns/) There is [#systemd-networkd: routing all traffic over WireGuard](https://wiki.archlinux.org/title/WireGuard#systemd-networkd:_routing_all_traffic_over_WireGuard) already. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

#### DNS

To use a peer as a DNS server, add its WireGuard tunnel IP address(es) to [/etc/resolv.conf](https://wiki.archlinux.org/title/WireGuard/title//etc/resolv.conf "/etc/resolv.conf"). For example, to use peer B as the DNS server:

```
/etc/resolv.conf
```

```
nameserver fdc9:281f:04d7:9ee9::2
nameserver 10.0.0.2
```

**Note:** If a peer will act as a DNS server, make sure to use its WireGuard tunnel address(es) as the DNS server address(es) instead of another of its addresses from allowed IPs. Otherwise DNS lookups may fail.

### Basic checkups

Invoking the [wg(8)](https://man.archlinux.org/man/wg.8) command without parameters will give a quick overview of the current configuration.

As an example, when peer A has been configured we are able to see its identity and its associated peers:

```
# wg
```

```
interface: wg0
  public key: UguPyBThx/+xMXeTbRYkKlP0Wh/QZT3vTLPOVaaXTD8=
  private key: (hidden)
  listening port: 51871

peer: 9jalV3EEBnVXahro0pRMQ+cHlmjE33Slo9tddzCVtCw=
  endpoint: 203.0.113.102:51902
  allowed ips: 10.0.0.2/32, fdc9:281f:04d7:9ee9::2

peer: 2RzKFbGMx5g7fG0BrWCI7JIpGvcwGkqUaCoENYueJw4=
  endpoint: 192.0.2.103:51993
  allowed ips: 10.0.0.3/32, fdc9:281f:04d7:9ee9::3
```

At this point one could reach the end of the tunnel. If the peers do not block ICMP echo requests, try [pinging](https://wiki.archlinux.org/title/WireGuard/title/Ping "Ping") a peer to test the connection between them.

Using ICMPv4:

    $ ping 10.0.0.2

Using ICMPv6:

    $ ping fdc9:281f:04d7:9ee9::2

After transferring some data between peers, the `wg` utility will show additional information:

```
# wg
```

```
interface: wg0
  public key: UguPyBThx/+xMXeTbRYkKlP0Wh/QZT3vTLPOVaaXTD8=
  private key: (hidden)
  listening port: 51871

peer: 9jalV3EEBnVXahro0pRMQ+cHlmjE33Slo9tddzCVtCw=
  endpoint: 203.0.113.102:51902
  allowed ips: 10.0.0.2/32, fdc9:281f:04d7:9ee9::2
  latest handshake: 5 seconds ago
  transfer: 1.24 KiB received, 1.38 KiB sent

peer: 2RzKFbGMx5g7fG0BrWCI7JIpGvcwGkqUaCoENYueJw4=
  allowed ips: 10.0.0.3/32, fdc9:281f:04d7:9ee9::3
```

### Persistent configuration

Persistent configuration can be achieved using `wg-quick@.service`, which is shipped with [wireguard-tools](https://archlinux.org/packages/?name=wireguard-tools), or using a network manager. Network managers that support WireGuard are [systemd-networkd](https://wiki.archlinux.org/title/WireGuard/title/Systemd-networkd "Systemd-networkd"), [netctl](https://wiki.archlinux.org/title/WireGuard/title/Netctl "Netctl")[\[2\]](https://gitlab.archlinux.org/archlinux/netctl/blob/master/docs/examples/wireguard), [NetworkManager](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager "NetworkManager") and [ConnMan](https://wiki.archlinux.org/title/WireGuard/title/ConnMan "ConnMan")[\[3\]](https://git.kernel.org/pub/scm/network/connman/connman.git/tree/doc/vpn-config-format.txt).

**Note:**

-   [netctl](https://wiki.archlinux.org/title/WireGuard/title/Netctl "Netctl") relies on [wg(8)](https://man.archlinux.org/man/wg.8) from [wireguard-tools](https://archlinux.org/packages/?name=wireguard-tools) and `/etc/wireguard/`*`interfacename`*`.conf` configuration files for establishing WireGuard connections.
-   [ConnMan](https://wiki.archlinux.org/title/WireGuard/title/ConnMan "ConnMan") has a very limited support for WireGuard. It can connect to only one peer.[\[4\]](https://git.kernel.org/pub/scm/network/connman/connman.git/commit/?id=95b25140bec7c4d9b6ae4e479dc1b94b7d409b39)

#### wg-quick

[wg-quick(8)](https://man.archlinux.org/man/wg-quick.8) configures WireGuard tunnels using configuration files from `/etc/wireguard/`*`interfacename`*`.conf`.

The current WireGuard configuration can be saved by utilizing the [wg(8)](https://man.archlinux.org/man/wg.8) utility's `showconf` command. For example:

    # wg showconf wg0 > /etc/wireguard/wg0.conf

To start a tunnel with a configuration file, use

    # wg-quick up interfacename

or use the systemd service—`wg-quick@`*`interfacename`*`.service`. To start the tunnel at boot, [enable](https://wiki.archlinux.org/title/WireGuard/title/Enable "Enable") the unit.

**Note:**

-   Users configuring the WireGuard interface using *wg-quick*, should make sure that no other [network management](https://wiki.archlinux.org/title/WireGuard/title/Network_management "Network management") software tries to manage it. To use [NetworkManager](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager "NetworkManager") and to not configure WireGuard interfaces with it, see [#Routes are periodically reset](https://wiki.archlinux.org/title/WireGuard#Routes_are_periodically_reset).
-   *wg-quick* adds additional configuration options to the configuration file format thus making it incompatible with [wg(8) § CONFIGURATION FILE FORMAT](https://man.archlinux.org/man/wg.8#CONFIGURATION_FILE_FORMAT). See the [wg-quick(8) § CONFIGURATION](https://man.archlinux.org/man/wg-quick.8#CONFIGURATION) man page for the configuration values in question. A *wg*-compatible configuration file can be produced by using `wg-quick strip`.
-   *wg-quick* does not provide a way to instruct [resolvconf](https://wiki.archlinux.org/title/WireGuard/title/Resolvconf "Resolvconf") to set the WireGuard interface as *private*. Even if there are search domains specified, all DNS queries from the system, not just those that match the search domains, will be sent to the DNS servers which are set in the WireGuard configuration.

**Peer A setup:**

```
/etc/wireguard/wg0.conf
```

```
[Interface]
Address = 10.0.0.1/24, fdc9:281f:04d7:9ee9::1/64
ListenPort = 51871
PrivateKey = PEER_A_PRIVATE_KEY

[Peer]
PublicKey = PEER_B_PUBLIC_KEY
PresharedKey = PEER_A-PEER_B-PRESHARED_KEY
AllowedIPs = 10.0.0.2/32, fdc9:281f:04d7:9ee9::2/128
Endpoint = peer-b.example:51902

[Peer]
PublicKey = PEER_C_PUBLIC_KEY
PresharedKey = PEER_A-PEER_C-PRESHARED_KEY
AllowedIPs = 10.0.0.3/32, fdc9:281f:04d7:9ee9::3/128
```

-   To *route all traffic* through the tunnel to a specific peer, add the [default route](https://en.wikipedia.org/wiki/Default_route "wikipedia:Default route") (`0.0.0.0/0` for IPv4 and `::/0` for IPv6) to `AllowedIPs`. E.g. `AllowedIPs = 0.0.0.0/0, ::/0`. wg-quick will automatically take care of setting up correct routing and fwmark[\[5\]](https://www.wireguard.com/netns/#routing-all-your-traffic) so that networking still functions.
-   To use a peer as a DNS server, set `DNS = `*`wireguard_internal_ip_address_of_peer`* in the `[Interface]` section. [Search domains](https://en.wikipedia.org/wiki/Search_domain "wikipedia:Search domain") are also set with the `DNS =` option. Separate all values in the list with commas.

**Peer B setup:**

```
/etc/wireguard/wg0.conf
```

```
[Interface]
Address = 10.0.0.2/24, fdc9:281f:04d7:9ee9::2/64
ListenPort = 51902
PrivateKey = PEER_B_PRIVATE_KEY

[Peer]
PublicKey = PEER_A_PUBLIC_KEY
PresharedKey = PEER_A-PEER_B-PRESHARED_KEY
AllowedIPs = 10.0.0.1/32, fdc9:281f:04d7:9ee9::1/128
Endpoint = 198.51.100.101:51871

[Peer]
PublicKey = PEER_C_PUBLIC_KEY
PresharedKey = PEER_B-PEER_C-PRESHARED_KEY
AllowedIPs = 10.0.0.3/32, fdc9:281f:04d7:9ee9::3/128
```

**Peer C setup:**

```
/etc/wireguard/wg0.conf
```

```
[Interface]
Address = 10.0.0.3/24, fdc9:281f:04d7:9ee9::3/64
ListenPort = 51993
PrivateKey = PEER_C_PRIVATE_KEY

[Peer]
PublicKey = PEER_A_PUBLIC_KEY
PresharedKey = PEER_A-PEER_C-PRESHARED_KEY
AllowedIPs = 10.0.0.1/32, fdc9:281f:04d7:9ee9::1/128
Endpoint = 198.51.100.101:51871

[Peer]
PublicKey = PEER_B_PUBLIC_KEY
PresharedKey = PEER_B-PEER_C-PRESHARED_KEY
AllowedIPs = 10.0.0.2/32, fdc9:281f:04d7:9ee9::2/128
Endpoint = peer-b.example:51902
```

#### systemd-networkd

[systemd-networkd](https://wiki.archlinux.org/title/WireGuard/title/Systemd-networkd "Systemd-networkd") has native support for setting up WireGuard interfaces. An example is provided in the [systemd.netdev(5) § EXAMPLES](https://man.archlinux.org/man/systemd.netdev.5#EXAMPLES) man page.

**Note:** Routing all DNS over WireGuard (i.e. `Domains=~.`) will prevent the DNS resolution of endpoints.

**Peer A setup:**

```
/etc/systemd/network/99-wg0.netdev
```

```
[NetDev]
Name=wg0
Kind=wireguard
Description=WireGuard tunnel wg0

[WireGuard]
ListenPort=51871
PrivateKey=PEER_A_PRIVATE_KEY

[WireGuardPeer]
PublicKey=PEER_B_PUBLIC_KEY
PresharedKey=PEER_A-PEER_B-PRESHARED_KEY
AllowedIPs=10.0.0.2/32
AllowedIPs=fdc9:281f:04d7:9ee9::2/128
Endpoint=peer-b.example:51902

[WireGuardPeer]
PublicKey=PEER_C_PUBLIC_KEY
PresharedKey=PEER_A-PEER_C-PRESHARED_KEY
AllowedIPs=10.0.0.3/32
AllowedIPs=fdc9:281f:04d7:9ee9::3/128
```

```
/etc/systemd/network/99-wg0.network
```

```
[Match]
Name=wg0

[Network]
Address=10.0.0.1/24
Address=fdc9:281f:04d7:9ee9::1/64
```

-   To use a peer as a DNS server, specify its WireGuard tunnel's IP address(es) in the *.network* file using the `DNS=` option. For [search domains](https://en.wikipedia.org/wiki/Search_domain "wikipedia:Search domain") use the `Domains=` option. See [systemd.network(5) § \[NETWORK\] SECTION OPTIONS](https://man.archlinux.org/man/systemd.network.5#%5BNETWORK%5D_SECTION_OPTIONS) for details.
-   To use a peer as the **only** DNS server, then in the *.network* file's `[Network]` section set `DNSDefaultRoute=true` and add `~.` to `Domains=` option.
-   To route additional subnets add them as `[Route]` sections in the *.network* file. For example:

```
/etc/systemd/network/99-wg0.network
```

```
...
[Route]
Destination=192.168.35.0/24
Scope=link

[Route]
Destination=fd7b:d0bd:7a6e::/64
Scope=link
```

**Warning:** In order to prevent the leaking of private keys, it is recommended to set the permissions of the *.netdev* file:

    # chown root:systemd-network /etc/systemd/network/99-*.netdev
    1. chmod 0640 /etc/systemd/network/99-*.netdev

**Peer B setup:**

```
/etc/systemd/network/99-wg0.netdev
```

```
[NetDev]
Name=wg0
Kind=wireguard
Description=WireGuard tunnel wg0

[WireGuard]
ListenPort=51902
PrivateKey=PEER_B_PRIVATE_KEY

[WireGuardPeer]
PublicKey=PEER_A_PUBLIC_KEY
PresharedKey=PEER_A-PEER_B-PRESHARED_KEY
AllowedIPs=10.0.0.1/32
AllowedIPs=fdc9:281f:04d7:9ee9::1/128
Endpoint=198.51.100.101:51871

[WireGuardPeer]
PublicKey=PEER_C_PUBLIC_KEY
PresharedKey=PEER_B-PEER_C-PRESHARED_KEY
AllowedIPs=10.0.0.3/32
AllowedIPs=fdc9:281f:04d7:9ee9::3/128
```

```
/etc/systemd/network/99-wg0.network
```

```
[Match]
Name=wg0

[Network]
Address=10.0.0.2/24
Address=fdc9:281f:04d7:9ee9::2/64
```

**Peer C setup:**

```
/etc/systemd/network/99-wg0.netdev
```

```
[NetDev]
Name=wg0
Kind=wireguard
Description=WireGuard tunnel wg0

[WireGuard]
ListenPort=51993
PrivateKey=PEER_C_PRIVATE_KEY

[WireGuardPeer]
PublicKey=PEER_A_PUBLIC_KEY
PresharedKey=PEER_A-PEER_C-PRESHARED_KEY
AllowedIPs=10.0.0.1/32
AllowedIPs=fdc9:281f:04d7:9ee9::1/128
Endpoint=198.51.100.101:51871

[WireGuardPeer]
PublicKey=PEER_B_PUBLIC_KEY
PresharedKey=PEER_B-PEER_C-PRESHARED_KEY
AllowedIPs=10.0.0.2/32
AllowedIPs=fdc9:281f:04d7:9ee9::2/128
Endpoint=peer-b.example:51902
```

```
/etc/systemd/network/99-wg0.network
```

```
[Match]
Name=wg0

[Network]
Address=10.0.0.3/24
Address=fdc9:281f:04d7:9ee9::3/64
```

#### systemd-networkd: routing all traffic over WireGuard

In this example Peer B connects to peer A with public IP address. Peer B routes all its traffic over WireGuard tunnel and uses Peer A for handling DNS requests.

**Peer A setup**

```
/etc/systemd/network/99-wg0.netdev
```

```
[NetDev]
Name=wg0
Kind=wireguard
Description=WireGuard tunnel wg0

[WireGuard]
ListenPort=51871
PrivateKey=PEER_A_PRIVATE_KEY

[WireGuardPeer]
PublicKey=PEER_B_PUBLIC_KEY
PresharedKey=PEER_A-PEER_B-PRESHARED_KEY
AllowedIPs=10.0.0.2/32
```

```
/etc/systemd/network/99-wg0.network
```

```
[Match]
Name=wg0

[Network]
Address=10.0.0.1/24
```

**Note:** You must still enable [IP Forwarding](https://wiki.archlinux.org/title/WireGuard/title/Internet_sharing#Enable_packet_forwarding "Internet sharing") and IP masquerading rules on Peer A in order to provide working internet to Peer B.

Assumes [ufw](https://wiki.archlinux.org/title/WireGuard/title/Ufw "Ufw"), but you could do the same with [iptables](https://wiki.archlinux.org/title/WireGuard/title/Iptables "Iptables") by using the rules outlined in the [Server configuration](https://wiki.archlinux.org/title/WireGuard#Server_configuration) section:

    $ ufw route allow in on wg0 out on enp5s0

```
/etc/ufw/before.rules
```

```
*nat
:POSTROUTING ACCEPT [0:0]
-A POSTROUTING -s 10.0.0.0/24 -o enp5s0 -j MASQUERADE
COMMIT
```

**Peer B setup:**

```
/etc/systemd/network/99-wg0.netdev
```

```
[NetDev]
Name=wg0
Kind=wireguard
Description=WireGuard tunnel wg0

[WireGuard]
ListenPort=51902
PrivateKey=PEER_B_PRIVATE_KEY
FirewallMark=0x8888

[WireGuardPeer]
PublicKey=PEER_A_PUBLIC_KEY
PresharedKey=PEER_A-PEER_B-PRESHARED_KEY
AllowedIPs=0.0.0.0/0
Endpoint=198.51.100.101:51871
```

```
/etc/systemd/network/50-wg0.network
```

```
[Match]
Name=wg0

[Network]
Address=10.0.0.2/24
DNS=10.0.0.1
DNSDefaultRoute=true
Domains=~.

[RoutingPolicyRule]
FirewallMark=0x8888
InvertRule=true
Table=1000
Priority=10

[Route]
Gateway=10.0.0.1
GatewayOnLink=true
Table=1000
```

**Exempting specific addresses**

In order to exempt specific addresses (such as private LAN addresses) from routing over the WireGuard tunnel, add them to a higher-priority RoutingPolicyRule than the one that was just created. This will configure them to use the default routing table, and prevent them from using the WireGuard table.

```
/etc/systemd/network/50-wg0.network
```

```
...

[RoutingPolicyRule]
To=192.168.0.0/24
Priority=9

...
```

#### Netctl

[Netctl](https://wiki.archlinux.org/title/WireGuard/title/Netctl "Netctl") has native support for setting up WireGuard interfaces. A typical set of WireGuard netctl profile configuration files would look like this:

**Peer A setup:**

```
/etc/netctl/wg0
```

```
Description="WireGuard tunnel on peer A"
Interface=wg0
Connection=wireguard
WGConfigFile=/etc/wireguard/wg0.conf

IP=static
Address=('10.0.0.1/24')
```

```
/etc/wireguard/wg0.conf
```

```
[Interface]
ListenPort = 51871
PrivateKey = PEER_A_PRIVATE_KEY

[Peer]
PublicKey = PEER_B_PUBLIC_KEY
AllowedIPs = 10.0.0.2/32
Endpoint = peer-b.example:51902

[Peer]
PublicKey = PEER_C_PUBLIC_KEY
AllowedIPs = 10.0.0.3/32
```

**Peer B setup:**

```
/etc/netctl/wg0
```

```
Description="WireGuard tunnel on peer B"
Interface=wg0
Connection=wireguard
WGConfigFile=/etc/wireguard/wg0.conf

IP=static
Address=('10.0.0.2/24')
```

```
/etc/wireguard/wg0.conf
```

```
[Interface]
ListenPort = 51902
PrivateKey = PEER_B_PRIVATE_KEY

[Peer]
PublicKey = PEER_A_PUBLIC_KEY
AllowedIPs = 10.0.0.1/32
Endpoint = peer-a.example:51871

[Peer]
PublicKey = PEER_C_PUBLIC_KEY
AllowedIPs = 10.0.0.3/32
```

**Peer C setup:**

```
/etc/netctl/wg0
```

```
Description="WireGuard tunnel on peer C"
Interface=wg0
Connection=wireguard
WGConfigFile=/etc/wireguard/wg0.conf

IP=static
Address=('10.0.0.3/24')
```

```
/etc/wireguard/wg0.conf
```

```
[Interface]
ListenPort = 51993
PrivateKey = PEER_C_PRIVATE_KEY

[Peer]
PublicKey = PEER_A_PUBLIC_KEY
AllowedIPs = 10.0.0.1/32
Endpoint = peer-a.example:51871

[Peer]
PublicKey = PEER_B_PUBLIC_KEY
AllowedIPs = 10.0.0.2/32
Endpoint = peer-b.example:51902
```

Then start and/or enable wg0 interface on every participating peer as needed, i.e.

    # netctl start wg0

To implement persistent site-to-peer, peer-to-site or site-to-site type of connection with WireGuard and Netctl, just add appropriate `Routes=` line into the netctl profile configuration file and add this network to `AllowedIPs` in the WireGuard profile, e.g. `Routes=('192.168.10.0/24 dev wg0')` in the `/etc/netctl/wg0` and `AllowedIPs=10.0.0.1/32, 192.168.10.0/24` in `/etc/wireguard/wg0.conf` and then do not forget to enable [IP forwarding](https://wiki.archlinux.org/title/WireGuard/title/Internet_sharing#Enable_packet_forwarding "Internet sharing").

#### NetworkManager

[NetworkManager](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager "NetworkManager") has native support for setting up WireGuard interfaces. For all details about WireGuard usage in NetworkManager, read Thomas Haller's blog post—[WireGuard in NetworkManager](https://blogs.gnome.org/thaller/2019/03/15/wireguard-in-networkmanager/).

**Tip:** NetworkManager can import a wg-quick configuration file. E.g.:

    # nmcli connection import type wireguard file /etc/wireguard/wg0.conf

**Note:** nmcli can create a WireGuard connection profile, but it does not support configuring peers. See [NetworkManager issue 358](https://gitlab.freedesktop.org/NetworkManager/NetworkManager/issues/358).

The following examples configure WireGuard via the keyfile format *.nmconnection* files. See [nm-settings-keyfile(5)](https://man.archlinux.org/man/nm-settings-keyfile.5) and [nm-settings(5)](https://man.archlinux.org/man/nm-settings.5) for an explanation on the syntax and available options.

**Peer A setup:**

```
/etc/NetworkManager/system-connections/wg0.nmconnection
```

```
[connection]
id=wg0
type=wireguard
interface-name=wg0

[wireguard]
listen-port=51871
private-key=PEER_A_PRIVATE_KEY
private-key-flags=0

[wireguard-peer.PEER_B_PUBLIC_KEY]
endpoint=peer-b.example:51902
preshared-key=PEER_A-PEER_B-PRESHARED_KEY
preshared-key-flags=0
allowed-ips=10.0.0.2/32;fdc9:281f:04d7:9ee9::2/128;

[wireguard-peer.PEER_C_PUBLIC_KEY]
preshared-key=PEER_A-PEER_C-PRESHARED_KEY
preshared-key-flags=0
allowed-ips=10.0.0.3/32;fdc9:281f:04d7:9ee9::3/128;

[ipv4]
address1=10.0.0.1/24
method=manual

[ipv6]
address1=fdc9:281f:04d7:9ee9::1/64
method=manual
```

-   To *route all traffic* through the tunnel to a specific peer, add the [default route](https://en.wikipedia.org/wiki/Default_route "wikipedia:Default route") (`0.0.0.0/0` for IPv4 and `::/0` for IPv6) to `wireguard-peer.`*`PEER_X_PUBLIC_KEY`*`.allowed-ips`. E.g. `wireguard-peer.`*`PEER_B_PUBLIC_KEY`*`.allowed-ips=0.0.0.0/0;::/0;`. Special handling of the default route in WireGuard connections is supported since NetworkManager 1.20.0.
-   To use a peer as a DNS server, specify its WireGuard tunnel's IP address(es) with the `ipv4.dns` and `ipv6.dns` settings. [Search domains](https://en.wikipedia.org/wiki/Search_domain "wikipedia:Search domain") can be specified with the `ipv4.dns-search=` and `ipv6.dns-search=` options. See [nm-settings(5)](https://man.archlinux.org/man/nm-settings.5) for more details. For example, using the keyfile format:

&nbsp;

    ...
    [ipv4]
    ...
    dns=10.0.0.2;
    dns-search=corp;
    ...
    [ipv6]
    ...
    dns=fdc9:281f:04d7:9ee9::2;
    dns-search=corp;
    ...

To use a peer as the **only** DNS server, set a negative DNS priority (e.g. `dns-priority=-1`) and add `~.` to the `dns-search=` settings.

**Peer B setup:**

```
/etc/NetworkManager/system-connections/wg0.nmconnection
```

```
[connection]
id=wg0
type=wireguard
interface-name=wg0

[wireguard]
listen-port=51902
private-key=PEER_B_PRIVATE_KEY
private-key-flags=0

[wireguard-peer.PEER_A_PUBLIC_KEY]
endpoint=198.51.100.101:51871
preshared-key=PEER_A-PEER_B-PRESHARED_KEY
preshared-key-flags=0
allowed-ips=10.0.0.1/32;fdc9:281f:04d7:9ee9::1/128;

[wireguard-peer.PEER_C_PUBLIC_KEY]
preshared-key=PEER_B-PEER_C-PRESHARED_KEY
preshared-key-flags=0
allowed-ips=10.0.0.3/32;fdc9:281f:04d7:9ee9::3/128;

[ipv4]
address1=10.0.0.2/24
method=manual

[ipv6]
address1=fdc9:281f:04d7:9ee9::2/64
method=manual
```

**Peer C setup:**

```
/etc/NetworkManager/system-connections/wg0.nmconnection
```

```
[connection]
id=wg0
type=wireguard
interface-name=wg0

[wireguard]
listen-port=51993
private-key=PEER_C_PRIVATE_KEY
private-key-flags=0

[wireguard-peer.PEER_A_PUBLIC_KEY]
endpoint=198.51.100.101:51871
preshared-key=PEER_A-PEER_C-PRESHARED_KEY
preshared-key-flags=0
allowed-ips=10.0.0.1/32;fdc9:281f:04d7:9ee9::1/128;

[wireguard-peer.PEER_B_PUBLIC_KEY]
endpoint=peer-b.example:51902
preshared-key=PEER_B-PEER_C-PRESHARED_KEY
preshared-key-flags=0
allowed-ips=10.0.0.2/32;fdc9:281f:04d7:9ee9::2/128;

[ipv4]
address1=10.0.0.3/24
method=manual

[ipv6]
address1=fdc9:281f:04d7:9ee9::3/64
method=manual
```

## Specific use-case: VPN server

[![Merge-arrows-2.png](https://wiki.archlinux.org/images/c/c9/Merge-arrows-2.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Merge-arrows-2.png)**This article or section is a candidate for merging with [#Routing all traffic over WireGuard](https://wiki.archlinux.org/title/WireGuard#Routing_all_traffic_over_WireGuard).**[![Merge-arrows-2.png](https://wiki.archlinux.org/images/c/c9/Merge-arrows-2.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Merge-arrows-2.png)

**Notes:** Same use case. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

**Note:** Usage of the terms "server" and "client" were purposefully chosen in this section specifically to help new users/existing OpenVPN users become familiar with the construction of WireGuard's configuration files. WireGuard documentation simply refers to both of these concepts as "peers."

The purpose of this section is to set up a WireGuard "server" and generic "clients" to enable access to the server/network resources through an encrypted and secured tunnel like [OpenVPN](https://wiki.archlinux.org/title/WireGuard/title/OpenVPN "OpenVPN") and others. The "server" runs on Linux and the "clients" can run on any number of platforms (the WireGuard Project offers apps on both iOS and Android platforms in addition to Linux, Windows and MacOS). See the official project [install link](https://www.wireguard.com/install/) for more.

**Tip:** Instead of using [wireguard-tools](https://archlinux.org/packages/?name=wireguard-tools) for server/client configuration, one may also use [systemd-networkd](https://wiki.archlinux.org/title/WireGuard#systemd-networkd) native WireGuard support.

### Server

[![Merge-arrows-2.png](https://wiki.archlinux.org/images/c/c9/Merge-arrows-2.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Merge-arrows-2.png)**This article or section is a candidate for merging with [#Site-to-point](https://wiki.archlinux.org/title/WireGuard#Site-to-point).**[![Merge-arrows-2.png](https://wiki.archlinux.org/images/c/c9/Merge-arrows-2.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Merge-arrows-2.png)

**Notes:** Same use case. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

On the peer that will act as the "server", first enable IPv4 forwarding using [sysctl](https://wiki.archlinux.org/title/WireGuard/title/Sysctl "Sysctl"):

    # sysctl -w net.ipv4.ip_forward=1

To make the change permanent, add `net.ipv4.ip_forward = 1` to `/etc/sysctl.d/99-sysctl.conf`.

A properly configured [firewall](https://wiki.archlinux.org/title/WireGuard/title/Firewall "Firewall") is *HIGHLY recommended* for any Internet-facing device.

If the server has a public IP configured, be sure to:

-   Allow UDP traffic on the specified port(s) on which WireGuard will be running (for example allowing traffic on `51820/UDP`).
-   Setup the forwarding policy for the firewall if it is not included in the WireGuard configuration for the interface itself `/etc/wireguard/wg0.conf`. The example below should have the iptables rules and work as-is.

If the server is behind NAT, be sure to forward the specified port(s) on which WireGuard will be running (for example, `51820/UDP`) from the router to the WireGuard server.

### Key generation

Generate key pairs for the server and for each client as explained in [#Key generation](https://wiki.archlinux.org/title/WireGuard#Key_generation).

### Server configuration

Create the "server" configuration file:

```
/etc/wireguard/wg0.conf
```

```
[Interface]
Address = 10.200.200.1/24
ListenPort = 51820
PrivateKey = SERVER_PRIVATE_KEY

1. substitute eth0 in the following lines to match the Internet-facing interface
1. if the server is behind a router and receives traffic via NAT, these iptables rules are not needed
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -A FORWARD -o %i -j ACCEPT; iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -D FORWARD -o %i -j ACCEPT; iptables -t nat -D POSTROUTING -o eth0 -j MASQUERADE

[Peer]
1. foo
PublicKey = PEER_FOO_PUBLIC_KEY
PresharedKey = PRE-SHARED_KEY
AllowedIPs = 10.200.200.2/32

[Peer]
1. bar
PublicKey = PEER_BAR_PUBLIC_KEY
PresharedKey = PRE-SHARED_KEY
AllowedIPs = 10.200.200.3/32
```

Additional peers ("clients") can be listed in the same format as needed. Each peer requires the `PublicKey` to be set. However, specifying `PresharedKey` is optional.

Notice that the `Address` has a netmask of `/24` and the clients on `AllowedIPs` `/32`. The clients only use their IP and the server only sends back their respective address.

The interface can be managed manually using [wg-quick(8)](https://man.archlinux.org/man/wg-quick.8) or using a [systemd](https://wiki.archlinux.org/title/WireGuard/title/Systemd "Systemd") service managed via [systemctl(1)](https://man.archlinux.org/man/systemctl.1).

The interface may be brought up using `wg-quick up wg0` respectively by [starting](https://wiki.archlinux.org/title/WireGuard/title/Start "Start") and potentially [enabling](https://wiki.archlinux.org/title/WireGuard/title/Enable "Enable") the interface via `wg-quick@`*`interface`*`.service`, e.g. `wg-quick@wg0.service`. To close the interface use `wg-quick down wg0` respectively [stop](https://wiki.archlinux.org/title/WireGuard/title/Stop "Stop") `wg-quick@`*`interface`*`.service`.

### Client configuration

Create the corresponding "client" configuration file(s):

```
foo.conf
```

```
[Interface]
Address = 10.200.200.2/32
PrivateKey = PEER_FOO_PRIVATE_KEY
DNS = 10.200.200.1

[Peer]
PublicKey = SERVER_PUBLICKEY
PresharedKey = PRE-SHARED_KEY
Endpoint = my.ddns.example.com:51820
AllowedIPs = 0.0.0.0/0, ::/0
```

```
bar.conf
```

```
[Interface]
Address = 10.200.200.3/32
PrivateKey = PEER_BAR_PRIVATE_KEY
DNS = 10.200.200.1

[Peer]
PublicKey = SERVER_PUBLICKEY
PresharedKey = PRE-SHARED KEY
Endpoint = my.ddns.example.com:51820
AllowedIPs = 0.0.0.0/0, ::/0
```

Using the catch-all `AllowedIPs = 0.0.0.0/0, ::/0` will forward all IPv4 (`0.0.0.0/0`) and IPv6 (`::/0`) traffic over the VPN.

**Note:** Users of [NetworkManager](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager "NetworkManager"), may need to [enable](https://wiki.archlinux.org/title/WireGuard/title/Enable "Enable") the `NetworkManager-wait-online.service` and users of [systemd-networkd](https://wiki.archlinux.org/title/WireGuard/title/Systemd-networkd "Systemd-networkd") may need to [enable](https://wiki.archlinux.org/title/WireGuard/title/Enable "Enable") the `systemd-networkd-wait-online.service` to wait until devices are network-ready before attempting a WireGuard connection.

## Testing the tunnel

[![Merge-arrows-2.png](https://wiki.archlinux.org/images/c/c9/Merge-arrows-2.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Merge-arrows-2.png)**This article or section is a candidate for merging with [#Basic checkups](https://wiki.archlinux.org/title/WireGuard#Basic_checkups).**[![Merge-arrows-2.png](https://wiki.archlinux.org/images/c/c9/Merge-arrows-2.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Merge-arrows-2.png)

**Notes:** Same topic. (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

Once a tunnel has been established, one can use [netcat](https://wiki.archlinux.org/title/WireGuard/title/Netcat "Netcat") to send traffic through it to test out throughput, CPU usage, etc.
On one side of the tunnel, run `nc` in listen mode and on the other side, pipe some data from `/dev/zero` into `nc` in sending mode.

In the example below, port 2222 is used for the traffic (be sure to allow traffic on port 2222 if using a firewall).

On one side of the tunnel listen for traffic:

    $ nc -vvlnp 2222

On the other side of the tunnel, send some traffic:

    $ dd if=/dev/zero bs=1024K count=1024 | nc -v 10.0.0.203 2222

Status can be monitored using `wg` directly.

```
# wg
```

```
interface: wg0
  public key: UguPyBThx/+xMXeTbRYkKlP0Wh/QZT3vTLPOVaaXTD8=
  private key: (hidden)
  listening port: 51820

peer: 9jalV3EEBnVXahro0pRMQ+cHlmjE33Slo9tddzCVtCw=
  preshared key: (hidden)
  endpoint: 192.168.1.216:53207
  allowed ips: 10.0.0.0/0
  latest handshake: 1 minutes, 17 seconds ago
  transfer: 56.43 GiB received, 1.06 TiB sent
```

## Tips and tricks

### Store private keys in encrypted form

It may be desirable to store private keys in encrypted form, such as through use of [pass](https://archlinux.org/packages/?name=pass). Just replace the PrivateKey line under \[Interface\] in the configuration file with:

    PostUp = wg set %i private-key <(su user -c "export PASSWORD_STORE_DIR=/path/to/your/store/; pass WireGuard/private-keys/%i")

where *user* is the Linux username of interest. See the [wg-quick(8)](https://man.archlinux.org/man/wg-quick.8) man page for more details.

### Endpoint with changing IP

After resolving a server's domain, WireGuard [will not check for changes in DNS again](https://lists.zx2c4.com/pipermail/wireguard/2017-November/002028.html).

If the WireGuard server is frequently changing its IP-address due DHCP, Dyndns, IPv6, etc., any WireGuard client is going to lose its connection, until its endpoint is updated via something like `wg set "$INTERFACE" peer "$PUBLIC_KEY" endpoint "$ENDPOINT"`.

Also be aware, if the endpoint is ever going to change its address (for example when moving to a new provider/datacenter), just updating DNS will not be enough, so periodically running reresolve-dns might make sense on any DNS-based setup.

Luckily, [wireguard-tools](https://archlinux.org/packages/?name=wireguard-tools) provides an example script `/usr/share/wireguard-tools/examples/reresolve-dns/reresolve-dns.sh`, that parses WG configuration files and automatically resets the endpoint address.

One needs to run the `/usr/share/wireguard-tools/examples/reresolve-dns/reresolve-dns.sh /etc/wireguard/wg.conf` periodically to recover from an endpoint that has changed its IP.

One way of doing so is by updating all WireGuard endpoints once every thirty seconds[\[6\]](https://git.zx2c4.com/WireGuard/tree/contrib/examples/reresolve-dns/README) via a systemd timer:

```
/etc/systemd/system/wireguard_reresolve-dns.timer
```

```
[Unit]
Description=Periodically reresolve DNS of all WireGuard endpoints

[Timer]
OnCalendar=*:*:0/30

[Install]
WantedBy=timers.target
```

```
/etc/systemd/system/wireguard_reresolve-dns.service
```

```
[Unit]
Description=Reresolve DNS of all WireGuard endpoints
Wants=network-online.target
After=network-online.target

[Service]
Type=oneshot
ExecStart=/bin/sh -c 'for i in /etc/wireguard/*.conf; do /usr/share/wireguard-tools/examples/reresolve-dns/reresolve-dns.sh "$i"; done'
```

Afterwards [enable](https://wiki.archlinux.org/title/WireGuard/title/Enable "Enable") and [start](https://wiki.archlinux.org/title/WireGuard/title/Start "Start") `wireguard_reresolve-dns.timer`

### Generate QR code

If the client is a mobile device such as a phone, [qrencode](https://archlinux.org/packages/?name=qrencode) can be used to generate client's configuration QR code and display it in terminal:

    $ qrencode -t ansiutf8 -r client.conf

### Enable debug logs

When using the Linux kernel module on a kernel that supports dynamic debugging, debugging information can be written into the kernel ring buffer (viewable with [dmesg](https://wiki.archlinux.org/title/WireGuard/title/Dmesg "Dmesg") and [journalctl](https://wiki.archlinux.org/title/WireGuard/title/Journalctl "Journalctl")) by running:

    # modprobe wireguard
    1. echo module wireguard +p > /sys/kernel/debug/dynamic_debug/control

### Reload peer (server) configuration

In case the WireGuard peer (mostly server) adding or removing another peers from its configuration and wants to reload it without stopping any active sessions, one can execute the following command to do it:

    # wg syncconf ${WGNET} <(wg-quick strip ${WGNET})

Where `$WGNET` is WireGuard interface name or configuration base name, for example `wg0` (for server) or `client` (without the *.conf* extension, for client).

[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)**This article or section needs expansion.**[![Tango-view-fullscreen.png](https://wiki.archlinux.org/images/3/38/Tango-view-fullscreen.png)](https://wiki.archlinux.org/title/WireGuard/title/File:Tango-view-fullscreen.png)

**Reason:** Show how to do this with other network managers from [#Persistent configuration](https://wiki.archlinux.org/title/WireGuard#Persistent_configuration). (Discuss in [Talk:WireGuard](https://wiki.archlinux.org/title/Talk:WireGuard))

## Troubleshooting

### Routes are periodically reset

Users of [NetworkManager](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager "NetworkManager") should make sure that it [is not managing](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager#Ignore_specific_devices "NetworkManager") the WireGuard interface(s). For example, create the following configuration file:

```
/etc/NetworkManager/conf.d/unmanaged.conf
```

```
[keyfile]
unmanaged-devices=type:wireguard
```

### Broken DNS resolution

When tunneling all traffic through a WireGuard interface, the connection can become seemingly lost after a while or upon new connection. This could be caused by a [network manager](https://wiki.archlinux.org/title/WireGuard/title/Network_manager "Network manager") or [DHCP](https://wiki.archlinux.org/title/WireGuard/title/DHCP "DHCP") client overwriting `/etc/resolv.conf`.

By default *wg-quick* uses *resolvconf* to register new [DNS](https://wiki.archlinux.org/title/WireGuard/title/DNS "DNS") entries (from the `DNS` keyword in the configuration file). This will cause issues with [network managers](https://wiki.archlinux.org/title/WireGuard/title/Network_manager "Network manager") and [DHCP](https://wiki.archlinux.org/title/WireGuard/title/DHCP "DHCP") clients that do not use *resolvconf*, as they will overwrite `/etc/resolv.conf` thus removing the DNS servers added by wg-quick.

The solution is to use networking software that supports [resolvconf](https://wiki.archlinux.org/title/WireGuard/title/Resolvconf "Resolvconf").

**Note:** Users of [systemd-resolved](https://wiki.archlinux.org/title/WireGuard/title/Systemd-resolved "Systemd-resolved") should make sure that [systemd-resolvconf](https://archlinux.org/packages/?name=systemd-resolvconf) is [installed](https://wiki.archlinux.org/title/WireGuard/title/Install "Install").

Users of [NetworkManager](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager "NetworkManager") should know that it does not use resolvconf by default. It is recommended to use [systemd-resolved](https://wiki.archlinux.org/title/WireGuard/title/Systemd-resolved "Systemd-resolved"). If this is undesirable, [install](https://wiki.archlinux.org/title/WireGuard/title/Install "Install") [openresolv](https://archlinux.org/packages/?name=openresolv) and configure NetworkManager to use it: [NetworkManager#Use openresolv](https://wiki.archlinux.org/title/WireGuard/title/NetworkManager#Use_openresolv "NetworkManager").

### Low MTU

Due to too low MTU (lower than 1280), wg-quick may have failed to create the WireGuard interface. This can be solved by setting the MTU value in WireGuard configuration in Interface section on client.

```
foo.config
```

```
[Interface]
Address = 10.200.200.2/24
MTU = 1420
PrivateKey = PEER_FOO_PRIVATE_KEY
DNS = 10.200.200.1
```

### Key is not the correct length or format

To avoid the following error, put the key value in the configuration file and not the path to the key file.

```
# wg-quick up wg0
```

```
[#] ip link add wg0 type wireguard
[#] wg setconf wg0 /dev/fd/63
Key is not the correct length or format: `/path/example.key'
Configuration parsing error
[#] ip link delete dev wg0
```

### Unable to establish a persistent connection behind NAT / firewall

By default, WireGuard peers remain silent while they do not need to communicate, so peers located behind a NAT and/or [firewall](https://wiki.archlinux.org/title/WireGuard/title/Firewall "Firewall") may be unreachable from other peers until they reach out to other peers themselves (or the connection may time out). Adding `PersistentKeepalive = 25` to the `[Peer]` settings of a peer located behind a NAT and/or firewall can ensure that the connection remains open.

```
# Set the persistent-keepalive via command line (temporarily)
```

```
[#] wg set wg0 peer $PUBKEY persistent-keepalive 25
```

### Loop routing

Adding the endpoint IP to the allowed IPs list, the kernel will attempt to send handshakes to said device binding, rather than using the original route. This results in failed handshake attempts.

As a workaround, the correct route to the endpoint needs to be manually added using

    ip route add  via  dev 

e.g. for peer B from above in a standard LAN setup:

    ip route add 203.0.113.102 via 192.168.0.1 dev eth0

To make this route persistent, the command can be added as `PostUp = ip route ...` to the `[Interface]` section of `wg0.conf`. However, on certain setups (e.g. using `wg-quick@.service` in combination with NetworkManager) this might fail on resume. Furthermore, this only works for a static network setup and fails if gateways or devices change (e.g. using ethernet or wifi on a laptop).

Using NetworkManager, a more flexible solution is to start WireGuard using a dispatcher script. As root, create

```
/etc/NetworkManager/dispatcher.d/50-wg0.sh
```

```
#!/bin/sh
case $2 in
  up)
    wg-quick up wg0
    ip route add  via $IP4_GATEWAY dev $DEVICE_IP_IFACE
    ;;
  pre-down)
    wg-quick down wg0
    ;;
esac
```

If not already running, start and enable `NetworkManager-dispatcher.service`.
Also, make sure that NetworkManager is not managing routes for `wg0` ([see above](https://wiki.archlinux.org/title/WireGuard#Routes_are_periodically_reset)).