https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/

WireGuard is a general-purpose VPN (Virtual Private Network) that utilizes state-of-the-art cryptography. Compared to other popular VPN solutions, such as IPsec and [OpenVPN](https://linuxize.com/post/how-to-set-up-an-openvpn-server-on-debian-9/) , [WireGuard](https://www.wireguard.com/) is generally faster, easier to configure, and has a smaller footprint. It is cross-platform and can run almost anywhere, including Linux, Windows, Android, and macOS.

Wireguard is a peer-to-peer VPN; it does not use the client-server model. Depending on the configuration, a peer can act as a traditional server or client. It works by creating a network interface on each peer device that acts as a tunnel. Peers authenticate each other by exchanging and validating public keys, mimicking the SSH model. Public keys are mapped with a list of IP addresses that are allowed in the tunnel. The VPN traffic is encapsulated in UDP.

This article explains how to install and configure WireGuard on Debian 10 that will act as a VPN server. We’ll also show you how to configure WireGuard as a client on Linux, Windows, and macOS. The client’s traffic will be routed through the Debian 10 server.

This setup can be used as a protection against Man in the Middle attacks, surfing the web anonymously, bypassing Geo-restricted content, or allowing your colleagues who work from home to connect to the company network securely.

## Prerequisites [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#prerequisites)

To follow this guide, you’ll need a machine with Debian 10 installed. You also need root or \[sudo access\](https://linuxize.com/post/how-to-create-a-sudo-user-on-debian/ to install packages and make changes to the system.

## Setting Up the WireGuard Server [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#setting-up-the-wireguard-server)

We’ll start by installing the WireGuard package on the Debian machine and set it up to act as a server. We’ll also configure the system to route the clients’ traffic through it.

### Install WireGuard on Debian 10 [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#install-wireguard-on-debian-10)

WireGuard is available from the Debian backports repositories. To add the repository to your system, run:

``` terminal
echo 'deb http://ftp.debian.org/debian buster-backports main' | sudo tee /etc/apt/sources.list.d/buster-backports.listCopy
```

Once the repository is enabled, update the apt cache and install the WireGuard module and tools:

``` terminal
sudo apt updatesudo apt install wireguardCopyCopy
```

WireGuard runs as a kernel module.

### Configuring WireGuard [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#configuring-wireguard)

You can configure and manage the WireGuard interfaces with the `wg` and `wg-quick` command-line tools.

Each device in the WireGuard VPN network needs to have a private and public key. Run the following command to generate the key pair:

``` terminal
wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickeyCopy
```

The files are generated in the `/etc/wireguard` directory. Use the [`cat`](https://linuxize.com/post/linux-cat-command/) or [`less`](https://linuxize.com/post/linux-cat-command/) commands to view the contents of the files. The private key should never be shared with anyone and should always be kept secure.

Wireguard also supports a pre-shared key, which adds an additional layer of symmetric-key cryptography. This key is optional and must be unique for each peer pair.

The next step is to configure the tunnel device that will route the VPN traffic.

The device can be set up either from the command line using the [`ip`](https://linuxize.com/post/linux-ip-command/) and `wg` commands, or by manually creating the configuration file. We’ll create the configuration with a text editor.

Open your editor and create a new file named `wg0.conf` with the following contents:

``` terminal
sudo nano /etc/wireguard/wg0.confCopy
```

/etc/wireguard/wg0.conf

``` chroma
[Interface]
Address = 10.0.0.1/24
SaveConfig = true
ListenPort = 51820
PrivateKey = SERVER_PRIVATE_KEY
PostUp = iptables -A FORWARD -i %i -j ACCEPT; iptables -t nat -A POSTROUTING -o ens3 -j MASQUERADE
PostDown = iptables -D FORWARD -i %i -j ACCEPT; iptables -t nat -D POSTROUTING -o ens3 -j MASQUERADE
```

Copy

You can name the interface anything you want to. However it is recommended to use something like `wg0` or `wgvpn0`.

The settings in the interface section have the following meaning:

-   Address - A comma-separated list of v4 or v6 IP addresses for the `wg0` interface. You can you an IP address from a range that is reserved for the private networks (10.0.0.0/8, 172.16.0.0/12 or 192.168.0.0/16).

-   ListenPort - The listening port.

-   PrivateKey - A private key generated by the `wg genkey` command. (To see the contents of the file type: `sudo cat /etc/wireguard/privatekey`)

-   SaveConfig - When set to true, the current state of the interface is saved to the configuration file when shutdown.

-   PostUp - Command or script that is executed before bringing the interface up. In this example, we’re using iptables to enable masquerading. This allows traffic to leave the server, giving the VPN clients access to the Internet.

    Make sure to replace `ens3` after `-A POSTROUTING` to match the name of your public network interface. You can easily find the interface with:

    ``` terminal
    ip -o -4 route show to default | awk '{print $5}'Copy
    ```

-   PostDown - A command or script which is executed before bringing the interface down. The iptables rules will be removed once the interface is down.

The `wg0.conf` and `privatekey` files should not be readable to normal users. Use [`chmod`](https://linuxize.com/post/chmod-command-in-linux/) to set the files permissions to `600`:

``` terminal
sudo chmod 600 /etc/wireguard/{privatekey,wg0.conf}Copy
```

Once done, bring the `wg0` interface up using the attributes specified in the configuration file:

``` terminal
sudo wg-quick up wg0Copy
```

The output will look something like this:

```
[#] ip link add wg0 type wireguard
[#] wg setconf wg0 /dev/fd/63
[#] ip -4 address add 10.0.0.1/24 dev wg0
[#] ip link set mtu 1420 up dev wg0
[#] iptables -A FORWARD -i wg0 -j ACCEPT; iptables -t nat -A POSTROUTING -o ens3 -j MASQUERADE
Copy
```

To check the interface state and configuration, run:

``` terminal
sudo wg show wg0Copy
```

```
interface: wg0
  public key: +Vpyku+gjVJuXGR/OXXt6cmBKPdc06Qnm3hpRhMBtxs=
  private key: (hidden)
  listening port: 51820
Copy
```

You can also verify the interface state with `ip a show wg0`:

``` terminal
ip a show wg0Copy
```

```
4: wg0:  mtu 1420 qdisc noqueue state UNKNOWN group default qlen 1000
    link/none 
    inet 10.0.0.1/24 scope global wg0
       valid_lft forever preferred_lft forever
Copy
```

WireGuard can be managed with Systemd. To bring the WireGuard interface at boot time, run the following command:

``` terminal
sudo systemctl enable wg-quick@wg0Copy
```

### Server Networking and Firewall Configuration [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#server-networking-and-firewall-configuration)

IP forwarding must be enabled for NAT to work. Open the `/etc/sysctl.conf` file and add or uncomment the following line:

``` terminal
sudo nano /etc/sysctl.confCopy
```

/etc/sysctl.conf

``` chroma
net.ipv4.ip_forward=1
```

Copy

Save the file and apply the change:

``` terminal
sudo sysctl -pCopy
```

```
net.ipv4.ip_forward = 1
Copy
```

If you are using UFW to manage your [firewall](https://linuxize.com/post/how-to-setup-a-firewall-with-ufw-on-debian-10/) you need to open UDP traffic on port `51820`:

``` terminal
sudo ufw allow 51820/udpCopy
```

That’s it. The Debian peer that will act as a server has been set up.

## Linux and macOS Clients Setup [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#linux-and-macos-clients-setup)

The installation instructions for all supported platforms are available at [https://wireguard.com/install/](https://wireguard.com/install/) . On Linux systems, you can install the package using the distribution package manager and on macOS with `brew`.

Once installed, follow the steps below to configure the client device.

The process for setting up a Linux and macOS client is pretty much the same as you did for the server. First, generate the public and private keys:

``` terminal
wg genkey | sudo tee /etc/wireguard/privatekey | wg pubkey | sudo tee /etc/wireguard/publickeyCopy
```

Create the file `wg0.conf` and add the following contents:

``` terminal
sudo nano /etc/wireguard/wg0.confCopy
```

/etc/wireguard/wg0.conf

``` chroma
[Interface]
PrivateKey = CLIENT_PRIVATE_KEY
Address = 10.0.0.2/24


[Peer]
PublicKey = SERVER_PUBLIC_KEY
Endpoint = SERVER_IP_ADDRESS:51820
AllowedIPs = 0.0.0.0/0
```

Copy

The settings in the interface section have the same meaning as when setting up the server:

-   Address - A comma-separated list of v4 or v6 IP addresses for the `wg0` interface.
-   PrivateKey - To see the contents of the file on the client machine, run: `sudo cat /etc/wireguard/privatekey`

The peer section contains the following fields:

-   PublicKey - A public key of the peer you want to connect to. (The contents of the server’s `/etc/wireguard/publickey` file).
-   Endpoint - An IP or hostname of the peer you want to connect to, followed by a colon and then a port number on which the remote peer listens to.
-   AllowedIPs - A comma-separated list of v4 or v6 IP addresses from which incoming traffic for the peer is allowed and to which outgoing traffic for this peer is directed. We’re using 0.0.0.0/0 because we are routing the traffic and want the server peer to send packets with any source IP.

If you need to configure additional clients, just repeat the same steps using a different private IP address.

## Windows Clients Setup [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#windows-clients-setup)

Download and install the Windows msi package from the [WireGuard website](https://wireguard.com/install/) .

Once installed, open the WireGuard application and click on “Add Tunnel” -&gt; “Add empty tunnel…” as shown on the image below:

![WireGuard Windows add Tunnel](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/windows-add-tunnel_hu56a3787b65506e3031c39b5f2d23f7ff_36326_768x0_resize_q75_lanczos.jpg)

A publickey pair is automatically created and displayed on the screen.

![WireGuard Windows Tunnel](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/windows-tunnel_huec2f8613c4e0f62234ee1d2c887150b3_60380_768x0_resize_q75_lanczos.jpg)

Enter a name for the tunnel and edit the configuration as follows:

``` chroma
[Interface]
PrivateKey = CLIENT_PRIVATE_KEY
Address = 10.0.0.2/24


[Peer]
PublicKey = SERVER_PUBLIC_KEY
Endpoint = SERVER_IP_ADDRESS:51820
AllowedIPs = 0.0.0.0/0
```

Copy

In the interface section, add a new line to define the client tunnel Address.

In the peer section, add the following fields:

-   PublicKey - The public key of the Debian server (`/etc/wireguard/publickey` file).
-   Endpoint - The IP address of the Debian server followed by a colon and WireGuard port (51820).
-   AllowedIPs - 0.0.0.0/0

Once done, click on the “Save” button.

## Add the Client Peer to the Server [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#add-the-client-peer-to-the-server)

The last step is to add the client’s public key and IP address to the server. To do that, run the following command on the Debian server:

``` terminal
sudo wg set wg0 peer CLIENT_PUBLIC_KEY allowed-ips 10.0.0.2Copy
```

Make sure to change the `CLIENT_PUBLIC_KEY` with the public key you generated on the client machine (`sudo cat /etc/wireguard/publickey`) and adjust the client IP address if it is different. Windows users can copy the public key from the WireGuard application.

Once done, go back to the client machine and bring up the tunneling interface.

### Linux and macOS Clients [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#linux-and-macos-clients)

Run the following command the bring up the interface:

``` terminal
sudo wg-quick up wg0Copy
```

Now you should be connected to the Debian server, and the traffic from your client machine should be routed through it. You can check the connection with:

``` terminal
sudo wgCopy
```

```
interface: wg0
  public key: gFeK6A16ncnT1FG6fJhOCMPMeY4hZa97cZCNWis7cSo=
  private key: (hidden)
  listening port: 53527
  fwmark: 0xca6c

peer: r3imyh3MCYggaZACmkx+CxlD6uAmICI8pe/PGq8+qCg=
  endpoint: XXX.XXX.XXX.XXX:51820
  allowed ips: 0.0.0.0/0
  latest handshake: 53 seconds ago
  transfer: 3.23 KiB received, 3.50 KiB sent
Copy
```

You can also open your browser, type “what is my ip”, and you should see your Debian server IP address.

To stop the tunneling, bring down the `wg0` interface:

``` terminal
sudo wg-quick down wg0Copy
```

### Windows Clients [\#](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/#windows-clients)

If you installed WireGuard on Windows, click on the “Activate” button. Once the peers are connected, the tunnel status will change to Active:

![WireGuard Windows connect Tunnel](https://linuxize.com/post/how-to-set-up-wireguard-vpn-on-debian-10/windows-connect-tunnel_hud873eb0fda625aa40c16e0159ae1b4f2_73122_768x0_resize_q75_lanczos.jpg)

## Conclusion