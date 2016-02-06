# murselessaps - OpenAPS small enough that you don't have to carry a Murse

![murse photo](http://ecx.images-amazon.com/images/I/41V0l2-6V8L.jpg)

### The goals I had were
1. Make it as small as possible while
2. Not having to use a soldering iron
3. Have at least a full day (16-18 hours) of battery life

I used a combination of the TI stick, Intel Edison and Sparkfun base board, along with a few other things. I was able to order everything from Amazon using Same Day delivery options except the TI Stick and CC Debugger which I got from ti.com. They have default shipping of 2 day air for $7.
* [Purchase List](http://amzn.com/w/10OD9UTHX6TTK)

###Setting up the software
1. Set up your Edison
..* [(https://github.com/oskarpearson/mmeowlink/wiki/Prepare-the-Edison-for-OpenAPS)
2. Set up your TI Stick
..* Grab the current hex file
..* Write the firmware to the stick using [CC-Tool] on Linux. You could also use the [TI Flash Programmer Tool](http://www.ti.com/tool/flash-programmer) on a PC (but I have not tested this).
..* [Install MMeowlink] (https://github.com/oskarpearson/mmeowlink/wiki/Installing-MMeowlink) onto your Edison

###Setting up the hardware

