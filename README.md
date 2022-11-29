# Raspberry-Pi-Custom-Linux-Distro

The project deals with creating a minimal image for Raspberry Pi 3 that supports programming languages such as C/C++ and Python for Development and supports internet using Ethernet or Wifi. 

The custom embedded Linux is made using the Yocto project. Detailed documentation can be found here. 

Pre-requisites for Ubuntu (Also works for Linux-Mint) - 
```
sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev zstd liblz4-tool
```

Pre-requisites for other linux distribution can be found here. 

After installing the pre-requisites, clone poky, which is a reference distribution provided by the Yocto Project 

```
mkdir raspberry_image
cd raspberry_image
git clone -b dunfell git://git.yoctoproject.org/poky
```
We use the dunfell branch in this project. 

Poky along isn't enough to make an image for Raspberry Pi. You need to add other layers that support Raspberry Pi Image creation. For more information about layers, refer to the documentation. 

The following meta-layers are necessary for development of Raspberry Pi Linux Distribution -
```
git clone -b dunfell git://git.yoctoproject.org/meta-raspberrypi
git clone -b dunfell git://git.yoctoproject.org/meta-openembedded
```
