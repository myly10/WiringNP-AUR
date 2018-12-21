This repo provides the WiringNP package for ArchLinux.

This branch is hard coded for NanoPi-NEO2 with kernel 4.x, since current ArchLinux kernel doesn't have the necessary information in `/proc/cpuinfo` to automatically identify the board model.

This package installs WiringPi headers to `/usr/local/include/wiringPi`, so please use `#include <wiringPi/wiringPi.h>` for headers.
