# pvbrowser on embedded device
This repo is forked from pvbrowser/pvb, and has been modified to run on embedded devices with QT5.5 environment.

## Prepare building environment
1. qmake  
Ensure that the qmake tool for arm device(`qt5.5.0-arm`) have been put into `/usr/local/`
    >NOTE: This program only supports QT5.5, other versions haven't been tested.  

2. cross compiler  
Install a cross compiler according to the architecture of your device.
    ``` bash
    # For gnueabihf:
    sudo apt-get install gcc-arm-linux-gnueabihf
    # For gnueabi:
    sudo apt-get install gcc-arm-linux-gnueabi
    ```
## Download the source code
clone this repo
``` bash
  git clone https://github.com/xujuntwt95329/pvb.git
```
## Build pvbrowser
This repo has been modified so you can build directly
``` bash
  cd /path/to/your/pvb
  ./build.sh
```
The building process takes a few minutes, then there will be an executable program in pvbrowser/pvbrowser, you can check it by type:
``` bash
  file pvbrowser/pvbrowser
```
and then you will see the information:
> pvbrowser/pvbrowser: ELF 32-bit LSB executable, ARM, EABI5 version 1 (GNU/Linux), dynamically linked, interpreter /lib/ld-linux-armhf.so.3, for GNU/Linux 3.2.0, BuildID[sha1]=f6de2421d8bdd5bbc4c71ba4d79838feb519e759, not stripped

If you want to use another compiler, a config file of qmake should be modified.  
Change the name of compiler in `/usr/local/qt5.5.0-arm/mkspecs/linux-arm-gnueabi-g++/qmake.conf`
``` bash
  # modifications to g++.conf
  QMAKE_CC                = arm-linux-gnueabihf-gcc
  QMAKE_CXX               = arm-linux-gnueabihf-g++
  QMAKE_LINK              = arm-linux-gnueabihf-g++
  QMAKE_LINK_SHLIB        = arm-linux-gnueabihf-g++

  # modifications to linux.conf
  QMAKE_AR                = arm-linux-gnueabihf-ar cqs
  QMAKE_OBJCOPY           = arm-linux-gnueabihf-objcopy
  QMAKE_NM                = arm-linux-gnueabihf-nm -P
  QMAKE_STRIP             = arm-linux-gnueabihf-strip
  load(qt_config)
```
If your compiler haven't been added into `$PATH`, then an absolute path is required.
