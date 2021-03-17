![](images/csgb-cover-crop2b1.jpg)

# Overview

CS Gain Block (CSGB) is a very economical HMC313 based RF amplifier module with on board power regulation and a nice "cutting edge RF black magic" aesthetic thanks to the inverted soldermask. 

It has about 10 dB of gain, and is good from near DC to 6 or 7 GHz. (These are figures from characterization with VNA, see more details below.) 

We developed this as part of our exploration into radar imaging, [Project Mashiro](https://github.com/criterionsignalworks/mashiro).

![](images/csgb-side-postmod2-crop2b1.jpg)
# Realization 

The circuit board is designed using Altium. As I'm too lazy to find a clever way to get this inverted soldermask effect, so I used manually placed polygons and regions. Tedious, yes, but it seems to work. 

For the on board voltage regulation circutiry, we reused the LDO design with ferrite bead and reverse blocking P channel MOSFET from our (WIP) development platform for STM8, CS Coda. The supporting passives (just a bias tee) for the MMIC amplifier were derived from the datasheet. We chose 0402 components for the DC blocking capacitors and RF blocking inductors due to our assembly capabilities and performance. 

We did a little microstrip filter design with the bowtie capacitor to ground - it mainly just look pretty, it doesn't seem to contribute too much to the performance of the device. 

![](images/csgb-drawing-crop2b1.png)
# Errata



![](images/csgb-tekmod-reverse-crop2b1.jpg)
## License
This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
