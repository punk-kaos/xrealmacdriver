# Custom user-space driver for the Xreal Air, Xreal Air 2, Xreal Air 2 Pro and Xreal Air 2 Ultra to use it on Mac

## Information before use

The code is provided as is and it's free to use. However the contributors can neither guarantee that 
it will work or that it won't damage your device since all of it is based on reverse-engineering 
instead of public documentation. The contributors are not responsible for proper or even official 
support. So use it at your own risk!

## Inspiration and motivation

This code is mostly original to Tobias Frisch's original code and the credit largely goes to him. 
I just fixed a minor Endian library difference that was making the code not compile on MacOS. 

Has been tested personally with Xreal Air 2 Pro's and outputs sensical data that I've been able to push to Opentrack and get proper head tracking!

Original GIT repo is here: https://gitlab.com/TheJackiMonster/nrealAirLinuxDriver


## Features

The driver will read, parse and interpret sensor data from two HID interfaces to feed custom event 
callbacks with data which can be used in user-space applications (for example whether buttons have 
been pressed, the current brightness level and the orientation quaternion/matrix/euler angles).

It's still a work-in-progress project since the goal would be to wire such events up into a 
compositor to render whole screens virtually depending on your 6-DoF orientation (without position).

Also keep in mind that this software will only run on Linux including devices like the Steam Deck, 
Pinephone or other mobile Linux devices.

## Dependencies

You can build the binary using `cmake` and there are only three dependencies for now:
 - [hidapi](https://github.com/libusb/hidapi)
 - [json-c](https://github.com/json-c/json-c/)
 - [Fusion](https://github.com/xioTechnologies/Fusion)

Fusion is a sensor fusion library which is integrated as git submodule. So when you checkout the 
repository, just update the submodules to get it. The libraries `hidapi` and `json-c` should be 
pretty common in most Linux distributions repositories.

## Build

The build process should be straight forward:

```
mkdir build
cd build
cmake ..
make
```

## Run

It's easiest to run the software with root privileges.

```
sudo xrealAirLinuxDriver
```

Alternatively, you can copy the xreal_air.rules to /etc/udev/rules.d:

```
sudo cp udev/xreal_air.rules /etc/udev/rules.d/xreal_air.rules
```
