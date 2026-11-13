# Hardware

## Most current information

You can find the most current information about the Beijing module at <br>[http://www.grodansparadis.com/beijing/beijing.html](http://www.grodansparadis.com/beijing/beijing.html). On the site you can also find links to the latest firmware, drivers and schematics etc for its use.

## The raw facts

| Parameter | Value |
| --- | --- |
| Current hardware reversion | B |
| Current firmware version | See [firmware release page](https://github.com/grodansparadis/can4vscp_kelvin_1wire/releases) |
| Supply voltage | +9-+28 VDC |
| PCB Size | 42mm x 72mm |
| Mounting options | DIN or wall |
| Power requirements | 0.1W |
| Communication: CAN4VSCP (CAN) | 125 kbps |
| Number of sensors supported | 6 |

## Schematics

![](media/kelvin_1wire_sch_rev_a.png ':size=700')

Schematics: Rev A (click picture to enlarge)

## Components

### Internal temperature sensor

The internal temperature sensor used on the Kelvin NTC10KA is the Murata [NCP21XV103J03RA](https://www.google.se/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&uact=8&ved=0ahUKEwiu-ujjlrnJAhWDjiwKHY9aCQQQFggiMAA&url=http%3A%2F%2Fwww.murata.com%2F~%2Fmedia%2Fwebrenewal%2Fsupport%2Flibrary%2Fcatalog%2Fproducts%2Fthermistor%2Fntc%2Fr44e.ashx&usg=AFQjCNE0U3R9tCH8Mm3JbRtiqhAN5yqOaQ&sig2=3Ga5yx9Fc6e15Gvr6YVbPg). Data for this sensor is as follows

| Description | Value |
| --- | --- |
| Time constant | 10 s |
| B[25/100]- value | 3944K |
| Temperature range | -40...+125ºC |
| Resistance tolerance | 5% |
| Resistance @ 25ºC | 10 Kohm |
| Max effect | 210 @ 25ºC mW |
| B[25/50]- value | 3900 |
| B[25/85]- value | 3934 |
| B[25/100]- value | 3944K 3% |
| Max error (B[25/100]) | 2.8 (%/C) |

![](media/kelvin_parts_a.png ':size=700')

![](media/kelvin_parts_b.png ':size=700')

## Connectors

![](media/kelvin_connectors.png ':size=700')

### Terminal block

![](media/pinout.png ':size=800')

| Pin | Description |
| --- | --- |
| 1 | Ground (GND) |
| 2 | +5V |
| 3 | Channel 3 |
| 4 | Ground (GND) |
| 5 | +5V |
| 6 | channel 2 |
| 7 | Ground (GND) |
| 8 | +5V |
| 9 | Channel 1 |
| 10 | Ground (GND) |
| 11 | +5V |
| 12 | Channel 0 |

### RJ-XX pin-out

The unit is powered over the CAN4VSCP bus. The CAN4VSCP normally uses CAT5 or better twisted pair cable. You can use other cables if you which. The important thing is that the CANH and CANL signals uses a twisted cable. For connectors you can use RJ10, RJ11, RJ12 or the most common RJ45 connectors.

Recommended connector is RJ-34/RJ-12 or RJ-11 with pin out as in this table.

| Pin | Use | RJ-11 | RJ-12 | RJ-45 | Patch Cable wire color T568B |
| --- | --- | --- | --- | --- | --- |
| 1 | +9-28V DC |  |  | RJ-45 | Orange/White |
| 2 1 | +9-28V DC |  | RJ-12 | RJ-45 | Orange |
| 3 2 1 | +9-28V DC | RJ-11 | RJ-12 | RJ-45 | Green/White |
| 4 3 2 | CANH | RJ-11 | RJ-12 | RJ-45 | Blue |
| 5 4 3 | CANL | RJ-11 | RJ-12 | RJ-45 | Blue/White |
| 6 5 4 | GND | RJ-11 | RJ-12 | RJ-45 | Green |
| 7 6 | GND |  | RJ-12 | RJ-45 | Brown/White |
| 8 | GND |  |  | RJ-45 | Brown |

![RJ-11/12/45 pin-out](media/rj45.jpg ':size=300')
**RJ-11/12/45 pin-out**

:!: Always use a pair of twisted wires for CANH/CANL for best noise immunity. If the EIA/TIA 56B standard is used this condition will be satisfied. This is good as most Ethernet networks already is wired this way.

### Inter module connector

The inter module connector can be used to connect modules that are physically close to each other together in an easy way. Remember that the minimum length of a connection cable is 30 cm.

| Pin | Description |
| --- | --- |
| 1 | Power from CAN4VSCP bus |
| 2 | CANH |
| 3 | CANL |
| 4 | GND |

<br>

![](media/odessa_inter_module_connector.png ':size=600')

### PIC programming Connector

| pin | Description |
| --- | --- |
| 1 | Reset |
| 2 | VCC |
| 3 | GND |
| 4 | PGD (RX of second serial port is here to) |
| 5 | PGC (TX of second serial port is here to) |
| 6 | LWPGM |

<br>

![](media/odessa_programming_connector.png ':size=700')

### Functionality of the status LED

The LED is used to indicate the status of the module. It will light steady when the firmware is running and will blink when the module is in the nickname discovery process.

| LED | Description |
| --- | --- |
| Steady | No error. Firmware running. |
| Blinking | Module is going through the [nickname discovery process](http://www.vscp.org/docs/vscpspec/doku.php?id=vscp_level_i_specifics#address_or_nickname_assignment_for_level_i_nodes). |

### CAN

CAN4VSCP is a CAN based bus running at 125 kbps with the addition of DC power. If you are interested in how CAN works you have a pretty good intro [here](http://www.eeherald.com/section/design-guide/esmod9.html).

CAN is known to be robust and is there for used in vehicles and in the industry.

<br>

---

![](media/grodan_logo.png ':size=100')

<center>
<b>Paradise of the Frog AB</b> Brattbergavägen 17, 820 50 LOS, SWEDEN<br />
<b>email:</b> <a href="info@grodansparadis.com">info@paradiseofthefrog.com</a> <b>phone:</b> +46 (0)8 40011835<br />
<b>web:</b> <a href="http://www.grodansparadis.com">http://www.paradiseofthefrog.com</a><br>
</center>
