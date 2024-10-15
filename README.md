###SETUP Armbian (debian12) Wifi Router

install 

```
apt update
apt install dnsmasq hostapd network-manager
systemctl disable dnsmasq
```

edit netplan

```
vim /etc/netplan/10-dhcp-all-interfaces.yaml
```

add config

```
network:
  version: 2
  renderer: NetworkManager
  ethernets:
    all-eth-interfaces:
      match:
        name: "e*"
      dhcp4: yes
  wifis:
    wlan0:
      dhcp4: no
      dhcp6: no
      addresses: [192.168.12.254/24]
      access-points:
        "orange":   #wifi name
          mode: ap
          password: "12345678" #wifi password
```

apply config

```
netplan --debug apply
```
