# MMDVM firmware installation for Nucleo64 F446RE

If you are using Pi-Star, expand filesystem (if you haven't done before):

    sudo pistar-expand
    sudo reboot

Enable RW filesystem if you are using Pi-Star:

    rpi-rw

Update list of packages:

    sudo apt-get update

Install toolchain and necessary packages:

    sudo apt-get install git gcc-arm-none-eabi gdb-arm-none-eabi libstdc++-arm-none-eabi-newlib autoconf libtool pkg-config libusb-1.0-0 libusb-1.0-0-dev

Install OpenOCD:

    git clone https://github.com/ntfreak/openocd
    cd openocd
    ./bootstrap
    ./configure
    make
    sudo make install

Download the sources:

    git clone https://github.com/g4klx/MMDVM
    cd MMDVM
    git submodule init
    git submodule update

Edit Config.h:

    nano Config.h
    
Usually you could enable (for Morpho connector):

    #define MODE_PINS
    #define STM32F4_NUCLEO_MORPHO_HEADER
    #define SEND_RSSI_DATA
    #define SERIAL_REPEATER
    #define USE_DCBLOCKER
    #define USE_ALTERNATE_POCSAG_LEDS

Compile the code:

    make nucleo

If you are using Pi-Star, stop services:

    sudo pistar-watchdog.service stop
    sudo systemctl stop mmdvmhost.timer
    sudo systemctl stop mmdvmhost.service

Upload the firmware:

    sudo make deploy
