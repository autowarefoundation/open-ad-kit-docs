# Installation

This page explains how to set up the development and runtime environment for the Open **AD Kit v3.0**

## Minimum requirements
- Arm64 based platfrom
  - minimum 40-core ARM Neoverse N1 equivalent
- NVIDIA GPU for GPU accelleration

- Tested Developer Platforms:
  - [AADP - AVA Developer Platform](https://www.ipi.wiki/pages/com-hpc-altra)
  - NVIDIA Orin with Jetpack 6 - **Tests are on going**

- Container Images:
  - https://github.com/autowarefoundation/autoware/pkgs/container/autoware-openadk


## 1. Set up the developer platform

The setup procedure depends on the developer platform. Currently only verified platform is the AADP

### AVA Platform

1. [Getting started with EWAOL](./getting-started.md)
1. [Boot EWAOL](./boot-ewaol.md)
1. [Extend rootfs partition](./extend-rootfs.md)

## 2. Pull Open AD Kit images on the developer platform

**TODO- Official images will be published  in Q1/2024**

```console
docker pull ghcr ghcr.io/autowarefoundation/openadk:..
docker pull ghcr ghcr.io/autowarefoundation/openadk:..
docker pull ghcr ghcr.io/autowarefoundation/openadk:..
docker pull ghcr ghcr.io/autowarefoundation/openadk:..
```

## 3. Run Autoware on the development platform
**TODO**

## 4. Advanced setup

The instructions how to install advanced software such as desktop environment and NVIDIA driver.

### AVA Platform

1. [Advanced setup for AVA Platform](./advanced-setup-setup-ava.md)
