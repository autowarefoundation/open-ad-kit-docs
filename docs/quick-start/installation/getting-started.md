# Getting started with EWAOL

## Overview

_Reference: [Project Quickstart — EWAOL documentation](https://ewaol.sites.arm.com/meta-ewaol/quickstart.html)_

This instruction explains how to build yocto image with EWAOL on your host machine.

## Build Host Setup

1. Install required packages for the build host by following [The Yocto Project ® 3.3.1 documentation](https://docs.yoctoproject.org/3.3.1/singleindex.html#required-packages-for-the-build-host).

   ```console
   sudo apt-get install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev
   ```

1. Install the kas setup tool.

   ```console
   sudo -H pip3 install kas
   ```

## Checkout the repository for AVA platform

1. [ADLINK / meta-adlink-ampere](https://github.com/ADLINK/meta-adlink-ampere)

   ```console
   git clone https://github.com/ADLINK/meta-adlink-ampere.git -b kirkstone
   ```

1. [EWAOL / meta-ewaol](https://git.gitlab.arm.com/ewaol/meta-ewaol)

   ```console
   cd meta-adlink-ampere
   git clone https://git.gitlab.arm.com/ewaol/meta-ewaol.git -b v1.0
   ```

1. Replace `virtualization` with `baremetal` in `ava.yml`.

   ```diff
    header:
    version: 1
    includes:
       - repo: meta-ewaol
   -     file: meta-ewaol-config/kas/virtualization.yml
   +     file: meta-ewaol-config/kas/baremetal.yml

    repos:
    meta-ewaol:
       path: meta-ewaol

    meta-adlink-ampere:



    machine: ava

    bblayers_conf_header:
    base: |
       POKY_BBLAYERS_CONF_VERSION = "2"
       BBPATH = "${TOPDIR}"
       BBFILES ?= ""

    target:
   -  - ewaol-virtualization-image
   +  - ewaol-baremetal-image
   ```

1. Build via kas

   ```console
   kas build ava.yml
   ```

:warning: You should be careful of utilizing full CPU power during build.
![Build](images/getting-started/build.png)
