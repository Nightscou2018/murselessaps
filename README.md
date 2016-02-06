# murselessaps - OpenAPS small enough that you don't have to carry a Murse

![murse photo](http://ecx.images-amazon.com/images/I/41V0l2-6V8L.jpg)

### The goals I had were
1. Make it as small as possible while
2. Not having to use a soldering iron
3. Have at least a full day (16-18 hours) of battery life

I used a combination of the TI stick, Intel Edison and Sparkfun base board, a battery that has pass-through charging (so you can charger it will keeping your Edison up and running), along with a few other tools and connectors. I was able to order everything from Amazon using Same Day delivery options except the TI Stick and CC Debugger which I got from ti.com. They have default shipping of 2 day air for $7.
* [Purchase List](http://amzn.com/w/10OD9UTHX6TTK)

There are plenty of other setups to consider, so you should check them out [here](https://github.com/oskarpearson/mmeowlink/wiki) and [here](https://github.com/openaps/docs).

###Setting up the software
1. Set up your Edison
  * [Prepare the Edison for OpenAPS] (https://github.com/oskarpearson/mmeowlink/wiki/Prepare-the-Edison-for-OpenAPS)
  * [Install OpenAPS] (https://github.com/openaps/docs) by starting at Section 1, Point 4. 
2. Set up your TI Stick
  * Write the firmware to the TI-stick
    * Install CC-Tool and a few other needed items with ```sudo apt-get install libusb-1.0-0-dev libboost-all-dev sdcc```. PC/Mac are other options which can use the [TI Flash Programmer Tool instead] (http://www.ti.com/tool/flash-programmer).
    * Grab the [current hex file]() which you plan to flash onto the TI stick
    * Plug your CC-Debugger that you purchased or borrowed into your your machine running Linux with a USB cable that carries data.
    * Plug your TI stick's USB into power.
    * Plug the other end onto your TI stick labeled DEBUG with the right stripe inwards towards the USB end of the board.
    * Press the reset button on your CC-Debugger. Make sure it is a green light before moving on.
    * Flash it ```cc-tool --log install.log -ew FILE-YOU-JUST-GRABBED.hex``` If you get [this error](http://sourceforge.net/p/cctool/discussion/general/thread/8f70cec7/) then you can edit cc-tool/programmer/cc_programmer.cpp and change the line ```USB_SET_CHIP_INFO, 1, 1, &command[0], command.size());``` to ```USB_SET_CHIP_INFO, 1, 0, &command[0], command.size());``` then save the file and recompile the tool by running ```make``` in the cc-tool directory
  * [Install MMeowlink] (https://github.com/oskarpearson/mmeowlink/wiki/Installing-MMeowlink) onto your Edison.
  * Install the tuner which tunes the radio frequency to best match your pump
  * Run the tuner to make sure it works
  * Add the tuner as part of your preflight loop

###Setting up the hardware to fit in your pocket
* Watch this short video

