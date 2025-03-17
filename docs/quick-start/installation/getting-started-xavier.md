# Getting started with Xavier

## Overview

_Reference: [Jetson AGX Xavier Developer Kit User Guide](https://developer.download.nvidia.com/assets/embedded/secure/jetson/xavier/docs/nv_jetson_agx_xavier_developer_kit_user_guide.pdf?mtIAvQlN-sZrtjEHIsVUWXewh_QY7Ja7cvAs2Tu7Vf5c42lLOmzwl_d97CBty4YcTr-_AoacSUDe66p0ISXJtEs7WzaRY0RWa47toceqOkEx0wvhby85pdW0R12u5DAW6EouyvgunVtBFjDLDU_AosRtubkJLuw6yS3jPd_uDDBUV50jZ652kgflfV-p26N4tLQoZ_itE_RRkw&t=eyJscyI6ImdzZW8iLCJsc2QiOiJodHRwczpcL1wvd3d3Lmdvb2dsZS5jb21cLyJ9)_

This instruction explains how to boot up Ubuntu on Xavier and access it from host PC.

## Connect To Xavier via SSH

Connect Xavier to internet, this network port is configured to obtain IP address automatically from DHCP by default.

You can look for IP address of the public ethernet and connect to Xavier via SSH.

```console
ifconfig
docker0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        inet 172.17.0.1  netmask 255.255.0.0  broadcast 172.17.255.255
        ether 02:42:1c:6c:b1:ec  txqueuelen 0  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 48:b0:2d:2b:7a:a8  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

eth1: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
        inet 192.168.10.46  netmask 255.255.252.0  broadcast 192.168.11.255
        inet6 fe80::9fcb:8fc6:a1a4:c6d2  prefixlen 64  scopeid 0x20<link>
        ether 2c:16:db:a3:03:10  txqueuelen 1000  (Ethernet)
        RX packets 4946  bytes 6212659 (6.2 MB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 723  bytes 72036 (72.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

lo: flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
        inet 127.0.0.1  netmask 255.0.0.0
        inet6 ::1  prefixlen 128  scopeid 0x10<host>
        loop  txqueuelen 1000  (Local Loopback)
        RX packets 218  bytes 20064 (20.0 KB)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 218  bytes 20064 (20.0 KB)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

rndis0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 82:24:ce:68:6a:bd  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0

usb0: flags=4099<UP,BROADCAST,MULTICAST>  mtu 1500
        ether 82:24:ce:68:6a:bf  txqueuelen 1000  (Ethernet)
        RX packets 0  bytes 0 (0.0 B)
        RX errors 0  dropped 0  overruns 0  frame 0
        TX packets 0  bytes 0 (0.0 B)
        TX errors 0  dropped 0 overruns 0  carrier 0  collisions 0
```

:speech_balloon: You can find IP address of Xavier such as `192.168.10.46`.
