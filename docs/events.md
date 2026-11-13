# Events

Here the events sent by the module is described.

## Temperature Event - Integer

If the two least significant [high control register](registers.md) bits is both set to zero for a sensor the temperature will be reported as a normalized integer.

| Event | Description |
| --- | --- |
| [CLASS1.MEASUREMENT (10) Type=6, Temperature](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.measurement#type_6_0x06_temperature) | If this event is enabled for a sensor it is sent periodically. The temperature is reported as a normalized integer value by this event. The event frequency is set in the [Report interval registers](registers.md) (default is off) and must be set to a non zero value for it to be sent.<br><br>Temperature can be reported in one of three units. Kelvin, Celsius (default) or Fahrenheit as set in the [low control register](registers.md). <br><br><u>**Data**</u><br>**Byte 0** - Data coding byte. See description below.<br>**Byte 1** - Always 131 (0x83). Decimal point should be shifted three steps to the left = divide by 1000.<br>**Byte 2** - MSB of normalized integer. Two complement number.<br>**Byte 3** - Normalized integer. Two complement number.<br>**Byte 4** - LSB of normalized integer. Two complement number.<br><br> |

The data coding byte is the measurement data coding format described in [the VSCP specification](http://www.vscp.org/docs/vscpspec/doku.php?id=data_coding).

The normalized integer is stored as a two complement 24-bit integer. To convert

1\. Calculate the 24-bit twos complement as MSB byte * 256 + LSB byte.

2\. If the most significant bit is not set this is a positive temperature. Divide by 1000 and you have the temperature.

3\. If the most significant bit is set this is a negative temperature. Now invert the result (the bits are inverted; 0 becomes 1, and 1 becomes 0) and add one to the result. Dive by 1000 and you have the negative temperature.

This means that +125 degrees Celsius is reported as 00E848 and -55 degrees Celsius is reported as FF2908.

### Data coding byte

| Bits | Description |
| --- | --- |
| 5,6,7 | Always set to 4 (0b100) - Normalized integer format. |
| 3,4 | <u>**Unit**:</u><br>**0 (0b00)** - Kelvin.<br> **1 (0b01)** – Celsius.<br> **2 (0b10)** – Fahrenheit. |
| 0,1,2 | <u>**Sensor Index**:</u><br>**0 (0b000)** - Sensor 0.<br>**1 (0b001)** - Sensor 1.<br>**2 (0b010)** - Sensor 2.<br>**3 (0b011)** - Sensor 3.<br>**4 (0b100)** - Sensor 4.<br>**5 (0b101)** - Sensor 5.<br>**6 (0b110)** - Sensor 6.<br>**7 (0b111)** - Sensor 7. |

## Temperature Event - Float

If the two least significant [high control register](registers.md) bits is set to **0b01** for a sensor the temperature will be reported as a floating point value. This is the default for the Kelvin 1-wire module.

| Event | Description |
| --- | --- |
| [CLASS1.MEASUREMENT (10) Type=6, Temperature](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.measurement#type_6_0x06_temperature) | If this event is enabled for a sensor it is sent periodically. The temperature is reported as a 32-bit floating point value by this event. The event frequency is set in the [Report interval registers](registers.md) (default is off) and must be set to a non zero value for it to be sent.<br><br>Temperature can be reported in one of three units. Kelvin, Celsius (default) or Fahrenheit as set in the [low control register](registers.md). <br><br><u>**Data**</u><br>**Byte 0** - Data coding byte. See description below.<br>**Byte 1** - MSB of 32-bit floating point value.<br>**Byte 2** - 32-bit floating point value.<br>**Byte 3** - 32-bit floating point value.<br>**Byte 4** - LSB of 32-bit floating point value.<br><br> |

The data coding byte is the measurement data coding format described in [the VSCP specification](http://www.vscp.org/docs/vscpspec/doku.php?id=data_coding).

### Data coding byte

| Bits | Description |
| --- | --- |
| 5,6,7 | Always set to 10 (0b101) - Floating point format. |
| 3,4 | <u>**Unit**:</u><br>**0 (0b00)** - Kelvin.<br> **1 (0b01)** – Celsius.<br> **2 (0b10)** – Fahrenheit. |
| 0,1,2 | <u>**Sensor Index**:</u><br>**0 (0b000)** - Sensor 0.<br>**1 (0b001)** - Sensor 1.<br>**2 (0b010)** - Sensor 2.<br>**3 (0b011)** - Sensor 3.<br>**4 (0b100)** - Sensor 4.<br>**5 (0b101)** - Sensor 5.<br>**6 (0b110)** - Sensor 6.<br>**7 (0b111)** - Sensor 7. |

## Temperature Event - String

If the two least significant [high control register](registers.md) bits is set to 2 (**0b10**) for a sensor the temperature will be reported as a string value.

| Event | Description |
| --- | --- |
| [CLASS1.MEASUREMENT (10) Type=6, Temperature](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.measurement#type_6_0x06_temperature) | If this event is enabled for a sensor it is sent periodically. The temperature is reported as a string value by this event. The event frequency is set in the [Report interval registers](registers.md) (default is off) and must be set to a non zero value for it to be sent.<br><br>Temperature can be reported in one of three units. Kelvin, Celsius (default) or Fahrenheit as set in the [low control register](registers.md). <br><br><u>**Data**</u><br>**Byte 0** - Data coding byte. See description below.<br>**Byte 1-7** - Value in string form. A period is always used as a decimal separator.<br><br> |

The data coding byte is the measurement data coding format described in [the VSCP specification](http://www.vscp.org/docs/vscpspec/doku.php?id=data_coding).

### Data coding byte

| Bits | Description |
| --- | --- |
| 5,6,7 | Always set to 4 (0b010) - String format. |
| 3,4 | <u>**Unit**:</u><br>**0 (0b00)** - Kelvin.<br> **1 (0b01)** – Celsius.<br> **2 (0b10)** – Fahrenheit. |
| 0,1,2 | <u>**Sensor Index**:</u><br>**0 (0b000)** - Sensor 0.<br>**1 (0b001)** - Sensor 1.<br>**2 (0b010)** - Sensor 2.<br>**3 (0b011)** - Sensor 3.<br>**4 (0b100)** - Sensor 4.<br>**5 (0b101)** - Sensor 5.<br>**6 (0b110)** - Sensor 6.<br>**7 (0b111)** - Sensor 7. |

## Alarm Event

If enabled the event is sent when a temperature sensor goes below a low alarm set point (see [Low-alarm-registers](http://www.grodansparadis.com/kelvinntc10k/manual/doku.php?id=registers)) or above a high alarm set point (see [High-alarm-registers](http://www.grodansparadis.com/kelvinntc10k/manual/doku.php?id=registers)). The hysteresis registers is used so that after an alarm event has been sent a new alarm event is not sent until the temperature goes below/above the value set in the set point plus(low)/minus(high) signed content of hysteresis register.

A read of the alarm register will reset the alarm status and alarm events will not be sent out again until the the temperature changed with the hysteresis amount.

| Event | Description |
| --- | --- |
| [CLASS1.ALARM, Type=2, Alarm occurred](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.alarm#type_2_0x02_alarm_occurred) | <u>**Data**</u><br>**Byte 0** - Index.<br> Index is <br>- **0** for Sensor 0. <br>- **1** for Sensor 1, <br>- **2** for Sensor 2. <br>- **3** for Sensor 3. <br>- **4** for Sensor 4. <br>- **5** for Sensor 5. <br>- **6** for Sensor 6. <br>- **7** for Sensor 7.<br><br>**Byte 1** - Zone.<br>**Byte 2** - Sub zone. |

Zone and sub-zone are the modules settings for the sensor generating the alarm. See [register 74-85](http://www.grodansparadis.com/kelvinntc10k/manual/doku.php?id=registers)

## TurnOn/TurnOff Event

If enabled, the event [CLASS1.CONTROL, Type=5, TurnOn](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_5_0x05_turnon) or [CLASS1.CONTROL, Type=6, TurnOff](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_6_0x06_turnoff) (Bit 5 in control register must be set (see [Control-registers](registers.md?id=sensor-control-registers)])) is sent when the temperature goes below or above the low(see [Low-alarm-registers](registers.md?id=low-alarm-registers)/high(see [High-alarm-registers](registers.md?id=high-alarm-registers) alarm set points. Settings in the control register bit 6 (see [sub:Control-registers]) decides which of the **TurnOn/TurnOff** event that is sent. The hysteresis setting (see [sub:Sensor-hysteresis-registers]) tells how much a temperature must raise or fall below the alarm set point before a new event will be sent.

| Event | Description |
| --- | --- |
| [CLASS1.CONTROL, Type=5, TurnOn](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_5_0x05_turnon) | <u>**Data**:</u><br>**Byte 0** - Index,<br>**Byte 1** - Zone.<br>**Byte 2** - Sub zone. |

| Event | Description |
| --- | --- |
| [CLASS1.CONTROL, Type=6, TurnOff](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_6_0x06_turnoff) | <u>**Data**:</u><br>**Byte 0** - Index,<br>**Byte 1** - Zone.<br>**Byte 2** - Sub zone. |

<u>**Index**</u> is **0** for Sensor 0, **1** for Sensor 1, **2** for Sensor 2 and so on.

<u>**Zone**</u> information is fetched from sensor zone register (see [sensor zone information registers](http://www.grodansparadis.com/kelvinntc10k/manual/doku.php?id=registers#sensor_zone_information_registers)).

<u>**Sub zone**</u> information is fetched from sensor sub-zone register (see [sensor zone information registers](http://www.grodansparadis.com/kelvinntc10k/manual/doku.php?id=registers#sensor_zone_information_registers)).

## Token Activity Event

| Event | Description |
| --- | --- |
| [CLASS1.INFORMATION, Type=37, Token Activity](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_37_0x25_token_activity) | One or more of this event is sent when a 1-wire bus is searched for ROM codes (see [channel_control_register](registers.md?id=channel-control-register)). Two frames are sent for each found device on a channel. <br><br>Note that all types of 1-wire devices attached to a channel is reported, not only temperature devices. <br><br><u>**Data for event 1 of 2**:</u><br>**Byte 0** - 0b00000101 (5),<br>**Byte 1** - Zone for module.<br>**Byte 2** - Sub zone for module.<br>**Byte 3** - 0 (first frame of two). <br>**Byte 4** - Byte 0 of ROM code. (MSB. CRC.) <br>**Byte 5** - Byte 1 of ROM code. (MSB of id) <br>**Byte 6** - Byte 2 of ROM code. <br>**Byte 7** - Byte 3 of ROM code. <br> <br><u>**Data for event 2 of 2**:</u><br>**Byte 0** - 0b00000101 (5),<br>**Byte 1** - Zone for module.<br>**Byte 2** - Sub zone for module.<br>**Byte 3** - 1 (second frame of two). <br>**Byte 4** - Byte 4 of ROM code. (MSB. CRC.) <br>**Byte 5** - Byte 5 of ROM code. <br>**Byte 6** - Byte 6 of ROM code (LSB of id). <br>**Byte 7** - Byte 7 of ROM code (family code). <br><br> |

## Sync. Event (incoming)

If a SYNC event is received by the module it will check the zone/subzone parameters of the event and send out [temperature measurement event(s)](http://www.grodansparadis.com/kelvin1w/manual/doku.php?id=events#temperature_event) for all sensors that match. This can be a handy feature to use of one want synchronized data from several sources.

| Event | Description |
| --- | --- |
| [CLASS1.CONTROL, Type=26, Sync](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_26_0x1a_sync) | <u>**Data**:</u><br>**Byte 0** - Index,<br>**Byte 1** - Zone.<br>**Byte 2** - Sub zone. |

<br>

---

![](media/grodan_logo.png ':size=100')

<center>
<b>Paradise of the Frog AB</b> Brattbergavägen 17, 820 50 LOS, SWEDEN<br />
<b>email:</b> <a href="info@grodansparadis.com">info@paradiseofthefrog.com</a> <b>phone:</b> +46 (0)8 40011835<br />
<b>web:</b> <a href="http://www.grodansparadis.com">http://www.paradiseofthefrog.com</a><br>
</center>
