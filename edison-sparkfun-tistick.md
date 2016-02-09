
# Set up Edison + TI Stick
There are plenty of other setups to consider, so you should check them out [here](https://github.com/oskarpearson/mmeowlink/wiki) and [here](https://github.com/openaps/docs).

##1. Set up your Edison
  * Activate your power button on your board with ```sudo apt-get install -y acpid```. This will allow you to restart the board safely when asked during the flashing of the Edison process
  * [Prepare the Edison for OpenAPS] (https://github.com/oskarpearson/mmeowlink/wiki/Prepare-the-Edison-for-OpenAPS)
  * Set up your wifi for [smart switching to home network] (https://github.com/TC2013/edison_wifi)
  * [Install OpenAPS] (https://github.com/openaps/docs) by starting at Section 1, Point 4. 
  

##2. Write the firmware to the TI-stick using cc-tool on Linux
  * Download CC-Tool ```wget http://downloads.sourceforge.net/project/cctool/cc-tool-0.26-src.tgz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fcctool%2F&ts=1454912359&use_mirror=tcpdiag -O cc-tool-0.26-src.tgz```, then unzip it ```tar xvfz cc-tool-0.26-src.tgz```
  * Edit ```vi cc-tool/programmer/cc_programmer.cpp``` and change the line ```USB_SET_CHIP_INFO, 1, 1, &command[0], command.size());``` to ```USB_SET_CHIP_INFO, 1, 0, &command[0], command.size());``` then save the file.
  * Install it with ```cd cc-tool``` then ```./configure``` then  ```make```
  * Install a few other needed items with ```sudo apt-get install libusb-1.0-0-dev libboost-all-dev sdcc```. 
  * Grab the [current hex file](https://github.com/ps2/subg_rfspy/releases) which you plan to flash onto the TI stick. If you are in the US and for our TI stick here it'd be usb_ep0_TI_DONGLE_US_STDLOC.hex.
  * Plug your CC-Debugger that you purchased or borrowed into your your machine running CC-Tool or TI Flash Programmer Tool.
  * Plug your TI stick's USB into power.
  * Plug the other end onto your TI stick labeled DEBUG with the right stripe inwards towards the USB end of the board.
  * Press the reset button on your CC-Debugger. Make sure it is a green light before moving on.
  * Flash it with ```sudo cc-tool --log install.log -ew FILE-YOU-JUST-GRABBED.hex```

##3. [Install MMeowlink] (https://github.com/oskarpearson/mmeowlink/wiki/Installing-MMeowlink) onto your Edison.
##4. [Install mmtune] (https://github.com/oskarpearson/mmeowlink/wiki/Tuning-your-connection-with-mmtune)
