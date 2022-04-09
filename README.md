# libcamera-apps

This is a small suite of libcamera-based apps that aim to copy the functionality of the existing "raspicam" apps. 

Build
-----
For usage and build instructions, see the official Raspberry Pi documenation pages [here.](https://www.raspberrypi.com/documentation/accessories/camera.html#libcamera-and-libcamera-apps)

Cross Build RPI4
----------------
Example steps for cross compile libcamera-apps for raspberry pi 4
````
git submodule sync --init
mkdir build && cd build
cmake .. -DENABLE_DRM=0 -DENABLE_X11=0 -DENABLE_QT=0 -DENABLE_OPENCV=0 -DCMAKE_C_COMPILER=aarch64-rpi4-linux-gnu-gcc -DCMAKE_CXX_COMPILER=aarch64-rpi4-linux-gnu-g++ -DCMAKE_BUILD_TYPE=Debug -DCMAKE_INSTALL_PREFIX=/path/to/install
make && make install
````

License
-------

The source code is made available under the simplified [BSD 2-Clause license](https://spdx.org/licenses/BSD-2-Clause.html).

Status
------

[![ToT libcamera build/run test](https://github.com/raspberrypi/libcamera-apps/actions/workflows/libcamera-test.yml/badge.svg)](https://github.com/raspberrypi/libcamera-apps/actions/workflows/libcamera-test.yml)
