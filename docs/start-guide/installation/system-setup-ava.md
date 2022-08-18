# System Setup on AVA platform

## Overview

This instruction explains how to perform system setup for test execution on AVA platform.

## Access to AVA platform via SSH

```console
ssh root@IP-ADDRESS
```

:speech_balloon: For example;

```console
ssh root@192.168.0.62
```

## Download kubernetes yaml files

Autoware.Universe runs as k3s clusters in Open AD Kit, so please download kubernetes yaml files to deploy Autoware to AVA platform.
  
1. Download.

   ```console
   wget https://raw.githubusercontent.com/autowarefoundation/open-ad-kit-docs/v2.0/docs/start-guide/installation/deployments/comhpc-deployments.zip
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
   root@ava:~# ls -la ~/map
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
   wget -P /etc/sysctl.d https://raw.githubusercontent.com/autowarefoundation/open-ad-kit-docs/v2.0/docs/start-guide/installation/sysctl.d/60_cyclonedds.conf
   ```

1. Update kernel parameters.

   ```console
   sysctl -p /etc/sysctl.d/60_cyclonedds.conf
   ```

## Download configuration file of Cyclone DDS

In this test, we are using Cyclone DDS, so you also need to download configuration file of Cyclone DDS.

1. Download `cyclonedds.xml`.

   ```console
   wget -P ~/cyclonedds https://raw.githubusercontent.com/autowarefoundation/open-ad-kit-docs/v2.0/docs/start-guide/installation/cyclonedds/cyclonedds.xml
   ```

## Modify `cyclonedds.xml`

You need to change the element `NetworkInterfaceAddress` to the network interface currently in use.

1. Find network interface.

   ```console
   root@comhpc:~# ip a 
   1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
      link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
      inet 127.0.0.1/8 scope host lo
         valid_lft forever preferred_lft forever
      inet6 ::1/128 scope host 
         valid_lft forever preferred_lft forever
   2: enP4p4s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP group default qlen 1000
      link/ether 00:30:64:1a:0a:65 brd ff:ff:ff:ff:ff:ff
      inet 192.168.0.62/24 brd 192.168.0.255 scope global dynamic enP4p4s0
         valid_lft 3383sec preferred_lft 2933sec
      inet6 fe80::1ab4:7a14:28e:4e61/64 scope link 
         valid_lft forever preferred_lft forever
      inet6 fe80::230:64ff:fe1a:a65/64 scope link 
         valid_lft forever preferred_lft forever
   3: sit0@NONE: <NOARP> mtu 1480 qdisc noop state DOWN group default qlen 1000
      link/sit 0.0.0.0 brd 0.0.0.0
   4: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
      link/ether 02:42:4b:b2:ee:68 brd ff:ff:ff:ff:ff:ff
      inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
         valid_lft forever preferred_lft forever
   ...

   :speech_balloon: You can find a network interface such as `enP4p4s0`.

1. Change the `NetworkInterfaceAddress`.

   ```console
   vi ~/cyclonedds/cyclonedds.xml
   ```

   For example; :page_facing_up: cyclonedds.xml

   ```diff
    <General>
   -  <NetworkInterfaceAddress>lo</NetworkInterfaceAddress>
   +  <NetworkInterfaceAddress>enP4p4s0</NetworkInterfaceAddress>
    </General>

   ```
