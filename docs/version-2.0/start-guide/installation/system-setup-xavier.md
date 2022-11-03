# System Setup on Xavier platform

## Overview

This instruction explains how to perform system setup for test execution on Xavier platform.

## Access to Xavier platform via SSH

```console
ssh root@IP-ADDRESS
```

:speech_balloon: For example;

```console
ssh nv@192.168.10.46
```

## Copy Autoware.Auto image to Xavier

**NOTE**: docker should be installed with post-installation steps. For instructions please refer to:

- [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu).
- [Post-installation steps for Linux](https://docs.docker.com/engine/install/linux-postinstall).

The docker image of Autoware.Auto is registered in [GitLab Container Registry](https://gitlab.com/autowarefoundation/autoware.auto/AutowareAuto/container_registry/2511358).

1. Copy docker image to Xavier.

   ```console
   docker pull registry.gitlab.com/autowarefoundation/autoware.auto/autowareauto/arm64/openadkit-foxy:latest
   ```

## K3s Installation

**NOTE**: K3s should be installed with following steps. For official instructions please refer to: [Install K3s on Ubuntu](https://docs.k3s.io/quick-start).

1. Install K3s.

   ```console
   curl -sfL https://get.k3s.io | sh -
   ```

1. Create directory.

   ```console
   mkdir ~/.kube/
   ```

1. Copy config file

   ```console
   sudo cp /etc/rancher/k3s/k3s.yaml ~/.kube/config
   ```

1. Setting environment

   ```console
   export KUBECONFIG=~/.kube/config
   ```

## Download kubernetes yaml files

Autoware.Universe runs as k3s clusters in Open AD Kit, so please download kubernetes yaml files to deploy Autoware to Xavier platform.

1. Download.

   ```console
   wget https://raw.githubusercontent.com/autowarefoundation/open-ad-kit-docs/main/docs/version-2.0/start-guide/installation/deployments/comhpc-deployments.zip
   ```

1. Unzip it.

   ```console
   unzip comhpc-deployments.zip -d comhpc-deployments
   ```

   :speech_balloon: You will see the following files are unzipped.

   ```console
   Archive:  comhpc-deployments.zip
     inflating: comhpc-api-deployment.yaml
     inflating: comhpc-control-deployment.yaml
     inflating: comhpc-map-deployment.yaml
     inflating: comhpc-persistent-volume.yaml
     inflating: comhpc-persistent-volume-claim.yaml
     inflating: comhpc-planning-deployment.yaml
     inflating: comhpc-simulator-deployment.yaml
     inflating: comhpc-system-deployment.yaml
     inflating: comhpc-vehicle-deployment.yaml
   ```

## Download map files

1. Download from Google Drive.

   ```console
   wget "https://drive.google.com/uc?export=download&id=1vWMLbmwJJE5tYO40ypCMxqtmgQPQxhiw&confirm=t&uuid=3d84d854-3dd2-4950-8cc8-248feeab547d" -O sample_data.zip
   ```

1. Unzip it.

   ```console
   unzip sample_data.zip
   ```

1. Move `map` directory from `sample_data`.

   ```console
   mv sample_data/map/ ~/
   ```

   :speech_balloon: You will see the following files are located.

   ```console
   ls -la ~/map
   total 61288
   drwxrwxr-x 2 root root     4096 Aug 18 06:23 .
   drwx------ 6 root root     4096 Aug 18 06:23 ..
   -rw-r--r-- 1 root root  1841436 Aug 18 06:23 lanelet2_map.osm
   -rw-r--r-- 1 root root 60904720 Aug 18 06:23 pointcloud_map.pcd
   ```

## Download **kernel configuration** file for tuning kernel parameters

We have to reconfigure kernel parameters by using `sysctl` for system stability.

1. Download.

   ```console
   wget -P /etc/sysctl.d https://raw.githubusercontent.com/autowarefoundation/open-ad-kit-docs/main/docs/version-2.0/start-guide/installation/sysctl.d/60_cyclonedds.conf
   ```

1. Update kernel parameters.

   ```console
   sysctl -p /etc/sysctl.d/60_cyclonedds.conf
   ```

## Download configuration file of Cyclone DDS

In this test, we are using Cyclone DDS, so you also need to download configuration file of Cyclone DDS.

1. Download `cyclonedds.xml`.

   ```console
   wget -P ~/cyclonedds https://raw.githubusercontent.com/autowarefoundation/open-ad-kit-docs/main/docs/version-2.0/start-guide/installation/cyclonedds/cyclonedds.xml
   ```

## Modify `cyclonedds.xml`

You need to change the element `NetworkInterfaceAddress` to the network interface currently in use.

1. Find network interface.

   ```console
   ip addr
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group    default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
   2: dummy0: <BROADCAST,NOARP> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 0e:fa:61:5e:35:cd brd ff:ff:ff:ff:ff:ff
   3: eth0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast state DOWN group default qlen 1000
    link/ether 48:b0:2d:2b:7a:a8 brd ff:ff:ff:ff:ff:ff
   4: l4tbr0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether 82:24:ce:68:6a:bd brd ff:ff:ff:ff:ff:ff
   5: rndis0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast master l4tbr0 state DOWN group default qlen 1000
    link/ether 82:24:ce:68:6a:bd brd ff:ff:ff:ff:ff:ff
   6: usb0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc pfifo_fast master l4tbr0 state DOWN group default qlen 1000
    link/ether 82:24:ce:68:6a:bf brd ff:ff:ff:ff:ff:ff
   7: eth1: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast state UP group default qlen 1000
    link/ether 2c:16:db:a3:03:10 brd ff:ff:ff:ff:ff:ff
    inet 192.168.10.46/22 brd 192.168.11.255 scope global dynamic noprefixroute eth1
       valid_lft 84077sec preferred_lft 84077sec
    inet6 fe80::9fcb:8fc6:a1a4:c6d2/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
   8: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default
    link/ether 02:42:0b:47:8f:45 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
   ```

   :speech_balloon: You can find a network interface such as `eth1`.

2. Change the `NetworkInterfaceAddress`.

   ```console
   vi ~/cyclonedds/cyclonedds.xml
   ```

   For example; :page_facing_up: cyclonedds.xml

   ```diff
    <General>
   -  <NetworkInterfaceAddress>lo</NetworkInterfaceAddress>
   +  <NetworkInterfaceAddress>eth1</NetworkInterfaceAddress>
    </General>

   ```
