### murselessaps - an openaps implemenation that's small enough for murse avoidance

![murse photo](http://ecx.images-amazon.com/images/I/41V0l2-6V8L.jpg)

##Version #1

I used a combination of the TI stick, Intel Edison and Sparkfun base board, a battery that has pass-through charging (so you can charger it will keeping your Edison up and running), along with a few other tools and connectors. 
[See V1 Page for photos and details](https://github.com/jmatheson/murselessaps/blob/master/v1.md)

##Version #2
Version 1 seemed to have a crappy (2-3 hour) battery life. So for v2, I tried reduce consumption by moving from 2 USB connections (battery and TI stick) down to 1. I did this by switching to this [2000mAu LiPo battery](http://www.amazon.com/gp/product/B00D73WJCY). The result was a smaller form factor [photo coming soon](), but battery life did not improve at all. The next try was to move my loop time from once a minute to once every five. Still, the battery life was only 2-3 hours. So, I have decided to move on to v3.

##Version #3
I am going to try the [Edison board + ERF stick](https://github.com/oskarpearson/mmeowlink/wiki/Intel-Edison-with-ERF-stick) setup - stay tuned!
