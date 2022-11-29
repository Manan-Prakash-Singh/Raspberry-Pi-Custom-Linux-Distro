# Raspberry-Pi-Custom-Linux-Distro

The project deals with creating a minimal image for Raspberry Pi 3 that supports programming languages such as C/C++ and Python for Development and supports internet using Ethernet or Wifi. 

The custom embedded Linux is made using the Yocto project. Detailed documentation can be found [here](https://docs.yoctoproject.org/index.html). 

Pre-requisites for Ubuntu (Also works for Linux-Mint) - 
```
sudo apt install gawk wget git diffstat unzip texinfo gcc build-essential chrpath socat cpio python3 python3-pip python3-pexpect xz-utils debianutils iputils-ping python3-git python3-jinja2 libegl1-mesa libsdl1.2-dev pylint3 xterm python3-subunit mesa-common-dev zstd liblz4-tool
```

Pre-requisites for other linux distribution can be found here. 

After installing the pre-requisites, clone poky, which is a reference distribution provided by the Yocto Project 

We use the dunfell branch in this project. 
Poky alone isn't enough to make an image for Raspberry Pi. You need to add other layers that support Raspberry Pi Image creation. For more information about layers, refer to the documentation. 

The following meta-layers are necessary for development of Raspberry Pi Linux Distribution -
```
mkdir raspberry_image
cd raspberry_image
git clone -b dunfell git://git.yoctoproject.org/poky
git clone -b dunfell git://git.yoctoproject.org/meta-raspberrypi
git clone -b dunfell git://git.yoctoproject.org/meta-openembedded
```

change into poky and source the oe-init-build-env
```
cd poky
source oe-init-build-env ../build
```

A build folder will be created in the raspberry_image document. Here is where the final image will be created. 

cd into conf directory and replace the sample local.conf file with the local.conf given in this repository 

Before you can begin making your image, you need to add your meta-layers into the bblayers.conf file. This can be easily done using bitbake. Use the following command to add layers to bblayers.conf
```
bitbake-layers add-layer /path/to/meta-layer (eg. /home/USER/raspberry_image/meta-raspberrypi/)
```

Use the above syntax to add the following layers - 
1) meta-raspberrypi
2) meta-oe (Found in meta-openembedded)
3) meta-python
4) meta-networking
5) meta-multimedia

Refer to the documentation to know more about how to add layers using bitbake. A sample bblayers.conf is attached for your reference.


Finally, use bitbake to bake your image. 
```
bitbake core-image-minimal
```

This process can take hours depending on your internet connection and host machine. When the process is done, the image can be find in build/tmp/deploy/image/raspberrypi3/

 
Find core-image-minimal-raspberrypi3.wic.gz or core-image-minimal-raspberrypi3.wic.xz and use Balena Etcher to flash these images to SD card. Viola! You are done with your custom linux distro for Raspberry Pi. You can customize it further by modifying your local.conf file to suit your needs. Run bitbake core-image-minimal again after modification (It takes considerably less time after the first time you run bitbake)


