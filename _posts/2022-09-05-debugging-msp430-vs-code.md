---
layout: post
title:  "Debugging MSP430 in VS Code"
---

My experience with embedded systems is rather small and related to pet projects only. 


So far I've been tinkering with 8-bit [AVR's](https://en.wikipedia.org/wiki/AVR_microcontrollers), 16- and 32-bit [chips by Texas Instruments](https://en.wikipedia.org/wiki/TI_MSP430) and [ESP8266](https://en.wikipedia.org/wiki/ESP8266) SoCs. I would not count Raspberry Pi in this list (there's even one  Pi Zero working at my home). 


And there's an absolute leader in my personal list: Texas Instruments. Reasons: great documentation, great selection of launchpads and also community. These guys are also crazy about low-power consumption.
There are also tradeoffs as always. In my opinion, their standard IDe [Code Composer Studio™](https://www.ti.com/tool/CCSTUDIO) is too heavy and not working that great under Linux. 

One obvious way to tackle the problem is to use a GCC compiler in combination with VS Code. While playing around with this setup, I found out for myself how gdb works and how lightweight the embedded-development setup might be.

To be continued...