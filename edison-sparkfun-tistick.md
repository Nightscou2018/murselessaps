
# Set up Edison + Sparkfun Base Board + TI Stick
There are plenty of other setups to consider, so you should check them out [here](https://github.com/oskarpearson/mmeowlink/wiki) and [here](https://github.com/openaps/docs).

###Getting the software set up
1. Set up your Edison
  * [Prepare the Edison for OpenAPS] (https://github.com/oskarpearson/mmeowlink/wiki/Prepare-the-Edison-for-OpenAPS)
  * [Install OpenAPS] (https://github.com/openaps/docs) by starting at Section 1, Point 4. 
  * Optional: Set up your wifi for [smart switching to home network] (https://github.com/TC2013/edison_wifi)
  * Activate your power button on the Sparkfun ```sudo apt-get install -y acpid```. This will allow you to shutdown the edison safely before battery swaps, etc.
  * Note, my setup using a Dexcom G5 which is connected to the G5 ios app via Ble, then to Nightscout via Share. My openaps implentation pulls BG values from NS. I do not have a Dexcom Receiver as part of the setup, nor can I do offline mode at this time. TODO: use Ble on the Edison to receive BG values from the Dexcom G5 transmitted directly.
2. Set up your TI Stick
  * Write the firmware to the TI-stick
    * Download CC-Tool ```wget http://downloads.sourceforge.net/project/cctool/cc-tool-0.26-src.tgz?r=http%3A%2F%2Fsourceforge.net%2Fprojects%2Fcctool%2F&ts=1454912359&use_mirror=tcpdiag -O cc-tool-0.26-src.tgz```, then unzip it ```tar xvfz cc-tool-0.26-src.tgz```
    * Edit ```vi cc-tool/programmer/cc_programmer.cpp``` and change the line ```USB_SET_CHIP_INFO, 1, 1, &command[0], command.size());``` to ```USB_SET_CHIP_INFO, 1, 0, &command[0], command.size());``` then save the file.
    * Install it with ```cd cc-tool``` then ```./configure``` then  ```make```
    * Install a few other needed items with ```sudo apt-get install libusb-1.0-0-dev libboost-all-dev sdcc```. PC/Mac are other options which can use the [TI Flash Programmer Tool instead] (http://www.ti.com/tool/flash-programmer).
    * Grab the [current hex file](https://github.com/ps2/subg_rfspy/releases) which you plan to flash onto the TI stick. If you are in the US and for our TI stick here it'd be usb_ep0_TI_DONGLE_US_STDLOC.hex.
    * Plug your CC-Debugger that you purchased or borrowed into your your machine running CC-Tool or TI Flash Programmer Tool.
    * Plug your TI stick's USB into power.
    * Plug the other end onto your TI stick labeled DEBUG with the right stripe inwards towards the USB end of the board.
    * Press the reset button on your CC-Debugger. Make sure it is a green light before moving on.
    * Flash it. If using Linux that'd be ```sudo cc-tool --log install.log -ew FILE-YOU-JUST-GRABBED.hex``` NOTE: If you get [this error](http://sourceforge.net/p/cctool/discussion/general/thread/8f70cec7/) then you can 
  * [Install MMeowlink] (https://github.com/oskarpearson/mmeowlink/wiki/Installing-MMeowlink) onto your Edison.
  * Install mmtune (which tunes the radio frequency on the stick to best match your pump). Replace XXXXXX with your pump id. If that port is incorrect for you, just `ls /dev/tty*`, then unplug the TI stick and run `ls /dev/tty*` again to see what the name of the port should be changed to.
```
git clone https://github.com/ps2/minimed_rf
cd minimed_rf
Sudo apt-get install ruby-full
sudo gem install bundler
bundle
ruby -I lib bin/mmtune /dev/ttyACM0 XXXXX

If not working, you may need:
Apt-get ruby-colorize
gem install serialport
```
  * Add mmtune to your aliases ```openaps alias add mmtune "! bash -c \"cd ~/src/minimed_rf/ && ruby -I lib bin/mmtune /dev/ttyACM0 XXXXXX | egrep -v 'rssi:|OK|Ver|Open'\""```
  * Run the tuner to make sure it works and to set up a frequency for the first time ```openaps mmtune```. It may show errors, but if it gives a frequency it's probably safe to ignore the errors.
  * Optional: Add the tuner as part of your preflight loop to get the best connection every time. ```openaps add preflight 'bash -c "rm -f monitor/clock.json && openaps mmtune && echo -n \"PREFLIGHT \" && openaps report invoke monitor/clock.json 2>/dev/null >/dev/null && grep -q T monitor/clock.json && echo OK || ( echo FAIL; openaps get-bg; sleep 120; exit 1 )"'```. Be sure to remove your old preflight if you have one first and then make sure it's added into whatever your cron sequence is.
