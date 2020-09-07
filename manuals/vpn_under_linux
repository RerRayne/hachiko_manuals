# VPN for Linux
For using hachiko's from your comfortable bed one can use VPN.
Windows guys have to clap on CISCO icon while Linux-jedi just need to type "ucivpnup" in command line.

To achieve this following easy steps are needed:

1. Install open-connect

    ```bash
    sudo apt-get install openconnect lib32ncurses5 lib32tinfo5 lib32z1 libc6-i386 libpkcs11-helper1 openvpn vpnc-scripts net-tools
   ```
2. Download my [ucivpnup](misc/ucivpnup) and [ucivpndown](misc/ucivpndown) files.
3. Change "evgenii.ponomarev" to your account name
4. Copy to /usr/bin:

    ```bash
    cp ucivpn* /usr/bin/
    chmod +x /usr/bin/ucivpn*
   ```

## Up VPN
Just type:

```bash
ucivpnup
```

answer yes and type your password

## Down VPN:

```bash
ucivpndown
```

## Additional manuals
* [Installing and Using the Linux OpenConnect client with UCI's VPN](http://www.socsci.uci.edu/~jstern/uci_vpn_ubuntu/ubuntu-openconnect-uci-instructions.html)
* manjaro vpnc-script:

    ```bash
    wget http://git.infradead.org/users/dwmw2/vpnc-scripts.git/blob_plain/HEAD:/vpnc-script
    ```