![](images/csgb-cover-crop2b1.jpg)

# Overview

CS Gain Block (CSGB) is a very economical [HMC313](https://www.analog.com/en/products/hmc313.html) based RF amplifier module with on board power regulation and a nice "cutting edge RF black magic" aesthetic thanks to the inverted soldermask. 

It has about 10 dB of gain, and is good from near DC to just a bit over 6 GHz. (These are figures from characterization with VNA, see more details below.) 

We developed this as part of our exploration into radar imaging, [Project Mashiro](https://github.com/criterionsignalworks/mashiro) - I (supposedly) broke an LNA evaluation board lent to us by Tektronix, which is why I'm making sure to include some protection circuitry. 

![](images/csgb-side-postmod2-crop2b1.jpg)

# Realization 

The circuit board is designed using Altium. As I'm too lazy to find a clever way to get this inverted soldermask effect, so I used manually placed polygons and regions. Tedious, yes, but it seems to work. 

For the on board voltage regulation circutiry, we reused the LDO design with ferrite bead and reverse blocking P channel MOSFET from our (WIP) development platform for STM8, [CS Coda](https://csw.cx/assets/projects/coda/coda-7-pre-asy-black.jpg). (Adapted to 5V, of course.) The supporting passives for the MMIC amplifier (just a bias tee) were derived from the [datasheet](https://www.analog.com/media/en/technical-documentation/data-sheets/hmc313.pdf). We chose 0402 components for the DC blocking capacitors and RF blocking inductors due to our assembly capabilities and performance. 

We did a little microstrip filter design with the bowtie capacitor to ground - it mainly just look pretty, it doesn't seem to contribute too much to the performance of the device. 

![](images/csgb-drawing-crop2b1.png)

# Errata

This is my first microstrip PCB design involving slightly more complex design considerations (though indeed it's pretty much just a simple breakout for HMC313)

I made a mistake with the placement of the bias tee - the RF blocking inductor should ideally be right on the transmission line. Instead, I cleverly placed a long track that acts as an open stub at the frequencies we're dealing with. This acted as a band reject filter, centering somewhere about 3 GHz. 

To fix this, a little bodge is required: cut the bias track close to the transmission line, put an inductor across there with an accompanying capacitor to ground. The exact values don't seem to matter too much, same 1 nH inductors and something like 1 nF should work. Keep the quality factor of the components in mind. 

This problem actually exists in the [official evaluation board](https://www.analog.com/en/design-center/evaluation-hardware-and-software/evaluation-boards-kits/eval-hmc313.html) designed by Hitite (now AD), which costs like $248.85 USD. The gain at near 6 GHz approaches -20 dB, rendering it entirely useless within the specified range!

We discovered this issue with help from Tektronix, who provided us access to a VNA from their mainstream lab (thanks!) 

![](images/csgb-dut-postmod-crop2b1.jpg)

# Performance 

Again thanks to kind folks at Tektronix, we were able characterize our design with the VNA. Our (revised) design performs better than the Hitite/AD reference board. 



## JLCPCB 

JLCPCB were able to help us fabricate these boards. We've worked with them for all of our projects so far and their flexibility and performance really helps realizing compact and high performing designs! 

We were able to get some close up images with a microscope, showing crisp soldermask and copper deposition:

![](images/csgb-ms-connector-crop2b1.jpg)
![](images/csgb-ms-microstrip-crop2b1.jpg)

## License
This work is licensed under a [Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International License][cc-by-nc-sa].

![](images/csgb-tekmod-reverse-crop2b1.jpg)

[cc-by-nc-sa]: http://creativecommons.org/licenses/by-nc-sa/4.0/
