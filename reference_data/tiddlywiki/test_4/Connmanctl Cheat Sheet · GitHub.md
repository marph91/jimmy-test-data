https://gist.github.com/kylemanna/6930087

# Connmanctl Cheat Sheet

-   Documentation @ [http://git.kernel.org/cgit/network/connman/connman.git/tree/doc](http://git.kernel.org/cgit/network/connman/connman.git/tree/doc)

## [![](data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgaGVpZ2h0PSIxNiIgd2lkdGg9IjE2IiB2ZXJzaW9uPSIxLjEiIHZpZXdib3g9IjAgMCAxNiAxNiIgY2xhc3M9Im9jdGljb24gb2N0aWNvbi1saW5rIj48cGF0aCBkPSJNNy43NzUgMy4yNzVhLjc1Ljc1IDAgMDAxLjA2IDEuMDZsMS4yNS0xLjI1YTIgMiAwIDExMi44MyAyLjgzbC0yLjUgMi41YTIgMiAwIDAxLTIuODMgMCAuNzUuNzUgMCAwMC0xLjA2IDEuMDYgMy41IDMuNSAwIDAwNC45NSAwbDIuNS0yLjVhMy41IDMuNSAwIDAwLTQuOTUtNC45NWwtMS4yNSAxLjI1em0tNC42OSA5LjY0YTIgMiAwIDAxMC0yLjgzbDIuNS0yLjVhMiAyIDAgMDEyLjgzIDAgLjc1Ljc1IDAgMDAxLjA2LTEuMDYgMy41IDMuNSAwIDAwLTQuOTUgMGwtMi41IDIuNWEzLjUgMy41IDAgMDA0Ljk1IDQuOTVsMS4yNS0xLjI1YS43NS43NSAwIDAwLTEuMDYtMS4wNmwtMS4yNSAxLjI1YTIgMiAwIDAxLTIuODMgMHoiIGZpbGwtcnVsZT0iZXZlbm9kZCIgLz48L3N2Zz4=)](https://gist.github.com/kylemanna/6930087#configure-wifi)Configure WiFi

-   Scan for access points (run multiple times for more complete scan):

          # connmanctl scan wifi
          Scan completed for wifi

-   Display access points discovered:

          # connmanctl services
          *AO Wired                ethernet_9059af5f4217_cable
              HOME-0842            wifi_009e959b585c_484f4d452d30383432_managed_psk
              ATT440               wifi_009e959b585c_415454343430_managed_psk
              andent               wifi_009e959b585c_616e64656e74_managed_psk
                                   wifi_009e959b585c_hidden_managed_psk
              ATT512               wifi_009e959b585c_415454353132_managed_psk
              GoldenBearTriangle   wifi_009e959b585c_476f6c64656e42656172547269616e676c65_managed_psk
              Mr. Pamuk            wifi_009e959b585c_4d722e2050616d756b_managed_psk
              thegirls             wifi_009e959b585c_7468656769726c73_managed_psk
              HappyDays            wifi_009e959b585c_486170707944617973_managed_psk
              tipsycoopaloop       wifi_009e959b585c_7469707379636f6f70616c6f6f70_managed_psk
              2BlueWiFi            wifi_009e959b585c_32426c756557694669_managed_psk

-   Displays details on the AP of interest:

          # connmanctl services wifi_009e959b585c_32426c756557694669_managed_psk
          /net/connman/service/wifi_009e959b585c_32426c756557694669_managed_psk
            Type = wifi
            Security = [ psk ]
            State = idle
            Strength = 63
            Favorite = False
            Immutable = False
            AutoConnect = False
            Name = 2BlueWiFi
            Ethernet = [ Method=auto, Interface=wlan0, Address=00:9E:95:9B:58:5C, MTU=1500 ]
            IPv4 = [  ]
            IPv4.Configuration = [ Method=dhcp ]
            IPv6 = [  ]
            IPv6.Configuration = [ Method=auto, Privacy=disabled ]
            Nameservers = [  ]
            Nameservers.Configuration = [  ]
            Timeservers = [  ]
            Timeservers.Configuration = [  ]
            Domains = [  ]
            Domains.Configuration = [  ]
            Proxy = [  ]
            Proxy.Configuration = [  ]
            Provider = [  ]

-   Write config file for connecting to secure AP:

          # cat << EOF > /var/lib/connman/-psk.config
          [service_wifi__managed_psk]
          Type = wifi
          Name = 
          Passphrase = 
          EOF

    -   Should be automatically re-read without needing to restart connman.
    -   Verify this worked correctly by re-running **connmanctl services** and observe **Immutable**, **AutoConnect** and **Favorite** are set to true.

-   Connect to the new secure AP:

          # connmanctl connect wifi_009e959b585c_32426c756557694669_managed_psk

    -   Verify correct operation by running **connmanctl services** and observe the local interface address as well as DNS. Also can check **ip addr ls** and **cat /etc/resolv.conf**

## [![](data:image/svg+xml;base64,PHN2ZyBhcmlhLWhpZGRlbj0idHJ1ZSIgaGVpZ2h0PSIxNiIgd2lkdGg9IjE2IiB2ZXJzaW9uPSIxLjEiIHZpZXdib3g9IjAgMCAxNiAxNiIgY2xhc3M9Im9jdGljb24gb2N0aWNvbi1saW5rIj48cGF0aCBkPSJNNy43NzUgMy4yNzVhLjc1Ljc1IDAgMDAxLjA2IDEuMDZsMS4yNS0xLjI1YTIgMiAwIDExMi44MyAyLjgzbC0yLjUgMi41YTIgMiAwIDAxLTIuODMgMCAuNzUuNzUgMCAwMC0xLjA2IDEuMDYgMy41IDMuNSAwIDAwNC45NSAwbDIuNS0yLjVhMy41IDMuNSAwIDAwLTQuOTUtNC45NWwtMS4yNSAxLjI1em0tNC42OSA5LjY0YTIgMiAwIDAxMC0yLjgzbDIuNS0yLjVhMiAyIDAgMDEyLjgzIDAgLjc1Ljc1IDAgMDAxLjA2LTEuMDYgMy41IDMuNSAwIDAwLTQuOTUgMGwtMi41IDIuNWEzLjUgMy41IDAgMDA0Ljk1IDQuOTVsMS4yNS0xLjI1YS43NS43NSAwIDAwLTEuMDYtMS4wNmwtMS4yNSAxLjI1YTIgMiAwIDAxLTIuODMgMHoiIGZpbGwtcnVsZT0iZXZlbm9kZCIgLz48L3N2Zz4=)](https://gist.github.com/kylemanna/6930087#comments–issues)Comments / Issues

-   WiFi driver + connman-1.17 + beaglebone appears to be buggy with connmanctl disable/enable
-   Connmanctl **connect** seems buggy, potential it calls enable?