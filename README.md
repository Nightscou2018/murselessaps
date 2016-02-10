### murselessaps - an openaps implemenation that's small enough for murse avoidance

![murse photo](http://ecx.images-amazon.com/images/I/41V0l2-6V8L.jpg)

##Version #1
#Goals
  1. Form factors as small as possible, while
  2. Not having to use a soldering iron
  3. Have  a full day (8-10 hours) of battery life (ok, I wanted longer but that's what I got)

#Setup
I used a combination of the TI stick, Intel Edison and Sparkfun base board, a battery that has pass-through charging (so you can charger it will keeping your Edison up and running), along with a few other tools and connectors. I was able to order everything from Amazon using Same Day delivery options except the TI Stick and CC Debugger which I got from ti.com. They have default shipping of 2 day air for $7.

#Results
[Photos and details from v1](https://github.com/jmatheson/murselessaps/blob/master/v1.md)

##Version #2
Version 1 seemed to have a crappy (2-3 hour) battery life. So for v2, I tried reduce consumption by moving from 2 USB connections (battery and TI stick) down to 1. I did this by switching to this [2000mAu LiPo battery](http://www.amazon.com/gp/product/B00D73WJCY). The result was a smaller form factor [seen here](), but battery life did not improve at all. The next try was to move my loop time from once a minute to once every five. Still, the battery life was only 2-3 hours. So, I have decided to move on to v3.
