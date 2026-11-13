# Getting started

You need

- RJ-45 patch cables or similar.
- A stable +9V - +28V DC power source.
- A host computer with a serial or USB interface.

The Kelvin 1-wire module is powered from the CAN4VSCP bus. [This article](http://www.grodansparadis.com/wiki/doku.php?id=connecting_can4vscp_devices_together) have information on how the bus is powered and set up. Follow it for a reliable setup. Don't forget the two 120 ohm terminators at each end of the bus. <u>They are important!</u>  You can also activate the on board terminator on the module if it is located at one end of your bus (see the [hardware section](hardware.md)).

When you power the module by inserting the RJ-45 cable the red LED on the board should light up to indicate it is powered. This is just a power indicator LED. When you power the board for the first time the green led starts to blink to indicate that the module search for a nickname. During normal operation this LED should light steady.

Remember that there need to be <u>at least two</u> CAN4VSCP (or other CAN device set to 125kbps) devices (one additional if you have the [Frankfurt RS-232](http://www.grodansparadis.com/frankfurt/rs232/frankfurt-rs232.html)) on the bus to be able to communicate. A single device can't talk by itself on a bus. It's an error.

![](media/odessa_inter_module_connector.png ':size=500')

As an alternative to power the Kelvin 1-wire module from the CAN4VSCP bus you can power it over the daisy chain connector. The [CAN4VSCP Power Injector](http://www.grodansparadis.com/powerinjector/can4vscp_big/powerinjector.html) is needed (or similar) for this.

## Installing the module

Connect the module to the CAN4VSCP bus. The red led led on the module should light up indicating that the device is powered. If this is the first time you start up the module the green lamp next to the initializing button will start to blink. This means that the module is trying to negotiate a nickname address with the rest of the modules on the bus. When it found a free nickname the green led will light steady. If the green led does not start to blink press the initialization button until it does. Now your module is ready to use.

If the green led never stops blinking you have a problem with your bus as the typically mean that the module dos not find any other module on the bus. Remember there must always be at least two active modules. Also check cables and that you have 120 ohm terminators installed on both ends of the bus.

When your module is installed it's time to configure it.

## Connecting temperature sensor(s)

![](media/18b20.jpg ':size=400')

To just test that communication works you don't need to install any external temperature sensors. You can work with the internal sensor even if it is very limited in functionality compared to the functionality that is available for external sensors. The on board sensor will not send out any data. But you can view it's temperature in the VSCP Works configuration view (Registers 24/25/26 on register page 1). It is presented as a 24-bit floating point value as all temperatures here so you may be better of if you switch to the abstraction view where the value is displayed in decimal.

You can view VSCP traffic on the CAN4VSCP bus with all CAN tools set to 125kbit/s but [VSCP Works](http://www.vscp.org/docs/vscpworks/doku.php?id=start) makes handling, configuring, diagnosing VSCP stuff a lot more easy. So this may be the time to get to know this piece of software which works on both Linux and Window.

The internal temperature sensor is heated by the processor and other things on the PCB so it will always give a bit of a high value. You can calibrate away this error if you want. See the [configuration section](http://www.grodansparadis.com/kelvin1w/manual/doku.php?id=configure).

![](media/pinout_small.jpg ':size=800')

To connect the external temperature sensors to the module you connect the sensors to the module as in this picture.

![](media/daisy_chaining.png ':size=800')

The picture shows two sensors but you can have as many 1-wire devices (well almost) as you like on a segment. However only two of them will be automatically handled by the module. You connect the daisy chain of sensors to one of the channel inputs. For cable length etc [read this](https://www.maximintegrated.com/en/app-notes/index.mvp/id/148).

The Kelvin 1-wire module have four measurement channels and you can connect two 1-wire temperature sensors to each of the channels. Types that currently is recognized by the firmware is DS1820 (the original), DS18S20 (not so old) and the latest version DS18B20 (recommended).

For a sensor to be recognized by the module you must enter it's ROM code in the correct position in the [ROM code register](registers.md?id=rom-code-registers) . Note that as all numbers on all VSCP system parts the ROM code should be entered MSB first (big endian).

Luckily there is a way to automatically find the ROM codes of the attached sensors. The code will also be written to the correct position in the ROM code registers. It is also possible to report the codes over the bus.

Do do this in the [Channel control register](registers.md?id=channel-control-register). For example writing **1** to this location will search 1-wire devices attached to channel 0 and fill in there ROM codes for that channel, writing **2** will do the same for channel 1 and so on. Well you can do both by writing **3** or all channels by writing **15**.

The upper nibble of the ROM code register have bits for searching and reporting findings on the bus. You can can do both at the same time or just one of them. The things you can possibly find on the bus is [listed here](http://owfs.sourceforge.net/family.html). The family code will identify each device.

The sensor search is the the most sensitive operation of the 1-wire protocol. If you have long cable lengths ( >5 meters) and/or bad cables and/or are in a bad environment. you may need to do the search several times to find the sensors on a channel. One way around this is to get the sensors ROM code and set it manually (search it with the sensor at a closer distance) and after that mount it on the long cable. [There is a paper here](https://www.maximintegrated.com/en/app-notes/index.mvp/id/148) discussing how to use long cable runs on 1-wire networks.

<br>

---

![](media/grodan_logo.png ':size=100')

<center>
<b>Paradise of the Frog AB</b> Brattbergavägen 17, 820 50 LOS, SWEDEN<br />
<b>email:</b> <a href="info@grodansparadis.com">info@paradiseofthefrog.com</a> <b>phone:</b> +46 (0)8 40011835<br />
<b>web:</b> <a href="http://www.grodansparadis.com">http://www.paradiseofthefrog.com</a><br>
</center>
