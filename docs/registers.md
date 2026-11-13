# Registers

All VSCP modules have a set of 8-bit registers defined to export it's functionality in a common way. Some of them (register 128-255) are predefined and the information in them are the same for all VSCP modules. See the [VSCP specification](http://www.vscp.org/docs/vscpspec/doku.php?id=register_abstraction_model) for a description of their content.

The lower 128 register space is used for module specific registers. It is also here you find registers with which you configure your module. Also registers where you typically can read status information such as measurement data from the module is here.

The lower register space is further expanded in register pages.

Below is a description of the registers of the Kelvin NTC10KA module.

## Module zone registers

| Register | Page | Description |
| --- | --- | --- |
| 0 | 0 | The zone this module belongs to. |
| 1 | 0 | The sub zone this module belongs to. |

## Sensor zone registers

| Register | Page | Description |
| --- | --- | --- |
| 2 | 0 | The zone for temperature sensor 0. |
| 3 | 0 | The sub zone for temperature sensor 0. |
| 4 | 0 | The zone for temperature sensor 1. |
| 5 | 0 | The sub zone for temperature sensor 1. |
| 6 | 0 | The zone for temperature sensor 2. |
| 7 | 0 | The sub zone for temperature sensor 2. |
| 8 | 0 | The zone for temperature sensor 3. |
| 9 | 0 | The sub zone for temperature sensor 3. |
| 10 | 0 | The zone for temperature sensor 4. |
| 11 | 0 | The sub zone for temperature sensor 4. |
| 12 | 0 | The zone for temperature sensor 5. |
| 13 | 0 | The sub zone for temperature sensor 5. |
| 14 | 0 | The zone for temperature sensor 6. |
| 15 | 0 | The sub zone for temperature sensor 6. |
| 16 | 0 | The zone for temperature sensor 7. |
| 17 | 0 | The sub zone for temperature sensor 7. |

## Sensor Control Registers

Configure which data is reported here and how it is reported and the overall functionality for each sensor.

| Register | Page | Description |
| --- | --- | --- |
| 18 | 0 | Control byte **low** for sensor 0. |
| 19 | 0 | Control byte **high** for sensor 0. |
| 20 | 0 | Control byte **low** for sensor 1. |
| 21 | 0 | Control byte **high** for sensor 1. |
| 22 | 0 | Control byte **low** for sensor 2. |
| 23 | 0 | Control byte **high** for sensor 2. |
| 24 | 0 | Control byte **low** for sensor 3. |
| 25 | 0 | Control byte **high** for sensor 3. |
| 26 | 0 | Control byte **low** for sensor 4. |
| 27 | 0 | Control byte **high** for sensor 4. |
| 28 | 0 | Control byte **low** for sensor 5. |
| 29 | 0 | Control byte **high** for sensor 5. |
| 30 | 0 | Control byte **low** for sensor 6. |
| 31 | 0 | Control byte **high** for sensor 6. |
| 32 | 0 | Control byte **low** for sensor 7. |
| 33 | 0 | Control byte **high** for sensor 7. |

### Description of low control register bits

| Bit | Description |
| --- | --- |
| 0,1 | **Temperature report unit** <br><br>**00** - Kelvin. <br>**01** - Celsius (default). <br> **10** - Fahrenheit. <br>**11** - Reserved. |
| 2 | Reserved. |
| 3 | Enable low alarm if set to one. |
| 4 | Enable high alarm if set to one. |
| 5 | Send **TurnOn/TurnOff** events instead of Alarm if set to one. |
| 6 | Controls when **TurnOn/TurnOff** events will be sent if activated. <br><br>0 - **TurnOn** event is sent when low temperature is reached as set in low temperature alarm register (see [sub:Low-alarm-registers]). **TurnOff** event is sent when high temperature is reached as set in high temperature alarm register (see [sub:High-alarm-registers]).<br><br>1 - **TurnOff** event is sent when low temperature is reached as set in low temperature alarm register (see [sub:Low-alarm-registers]). **TurnOn** event is sent when high temperature is reached as set in high temperature alarm register (see [sub:High-alarm-registers]). <br><br>The hysteresis value (see [sub:Sensor-hysteresis-registers]) will effect **TurnOn/TurnOff** events The temperature must go above or below the hysteresis value before a new event will be sent out. |
| 7 | If this bit is set sn Alarm events will be sent continuous with a one second interval until the alarm register is read or the temperature goes to a non alarm state (with hysteresis taken into account see [sub:Low-temperature-alarm](sub/low-temperature-alarm.md)). **TurnOn/TurnOff** events will not be affected by a cleared alarm register and will be sent until this bit is cleared or the temperature goes to a non alarm state (with hysteresis taken into account. |

### Description of high control register bits

| Bit | Description |
| --- | --- |
| 0,1 | **Report format** <br><br>**00** - CLASS=10, Report as int. <br>**01** - CLASS=10, Report as float (default). <br> **10** - CLASS=10, Report as string. <br>**11** - Reserved. |
| 2-7 | Reserved |

## Report interval registers

| Register | Page | Description |
| --- | --- | --- |
| 34 | 0 | Report interval for sensor 0 in seconds (Set to zero for no report). |
| 35 | 0 | Report interval for sensor 1 in seconds (Set to zero for no report). |
| 36 | 0 | Report interval for sensor 2 in seconds (Set to zero for no report). |
| 37 | 0 | Report interval for sensor 3 in seconds (Set to zero for no report). |
| 38 | 0 | Report interval for sensor 4 in seconds (Set to zero for no report). |
| 39 | 0 | Report interval for sensor 5 in seconds (Set to zero for no report). |
| 40 | 0 | Report interval for sensor 6 in seconds (Set to zero for no report). |
| 41 | 0 | Report interval for sensor 7 in seconds (Set to zero for no report). |

## B constant for on-board sensor

| Register | Page | Description |
| --- | --- | --- |
| 42 | 0 | This register holds the most significant byte of the NTC B constant for sensor 9 the on-board sensor. |
| 43 | 0 | This register holds the least significant byte of the NTC B constant for sensor 9 the on-board sensor. |

# Page 1

## Temperature registers

Temperatures is stored as 32-bit floating point numbers in big-endian format (MSB first).

| Register | Page | Description |
| --- | --- | --- |
| 0 | 0 | Temperature sensor 0 MSB. |
| 1 | 0 | Temperature sensor 0. |
| 2 | 0 | Temperature sensor 0. |
| 3 | 0 | Temperature sensor 0 LSB. |
| 4 | 0 | Temperature sensor 1 MSB. |
| 5 | 0 | Temperature sensor 1. |
| 6 | 0 | Temperature sensor 1. |
| 7 | 0 | Temperature sensor 1 LSB. |
| 8 | 0 | Temperature sensor 2 MSB. |
| 9 | 0 | Temperature sensor 2. |
| 10 | 0 | Temperature sensor 2. |
| 11 | 0 | Temperature sensor 2 LSB. |
| 12 | 0 | Temperature sensor 3 MSB. |
| 13 | 0 | Temperature sensor 3. |
| 14 | 0 | Temperature sensor 3. |
| 15 | 0 | Temperature sensor 3 LSB. |
| 16 | 0 | Temperature sensor 4 MSB. |
| 17 | 0 | Temperature sensor 4. |
| 18 | 0 | Temperature sensor 4. |
| 19 | 0 | Temperature sensor 4 LSB. |
| 20 | 0 | Temperature sensor 5 MSB. |
| 21 | 0 | Temperature sensor 5. |
| 22 | 0 | Temperature sensor 5. |
| 23 | 0 | Temperature sensor 5 LSB. |
| 24 | 0 | Temperature sensor 6 MSB. |
| 25 | 0 | Temperature sensor 6. |
| 26 | 0 | Temperature sensor 6. |
| 27 | 0 | Temperature sensor 6 LSB. |
| 28 | 0 | Temperature sensor 7 MSB. |
| 29 | 0 | Temperature sensor 7. |
| 30 | 0 | Temperature sensor 7. |
| 31 | 0 | Temperature sensor 7 LSB. |
| 32 | 0 | Temperature sensor 8 MSB (on board sensor). |
| 33 | 0 | Temperature sensor 8. (on board sensor). |
| 34 | 0 | Temperature sensor 8. (on board sensor). |
| 35 | 0 | Temperature sensor 8 LSB (on board sensor). |

- Sensor 0 and sensor 1 is on channel 0.
- Sensor 2 and sensor 3 is on channel 1.
- Sensor 4 and sensor 5 is on channel 2.
- Sensor 6 and sensor 7 is on channel 3.
- Sensor 9 is the on-board NTC sensor.

# Page 2

## Low alarm registers

| Register | Page | Description |
| --- | --- | --- |
| 0 | 2 | Low alarm set point for sensor 0 MSB. |
| 1 | 2 | Low alarm set point for sensor 0 LSB. |
| 2 | 2 | Low alarm set point for sensor 1 MSB. |
| 3 | 2 | Low alarm set point for sensor 1 LSB. |
| 4 | 2 | Low alarm set point for sensor 2 MSB. |
| 5 | 2 | Low alarm set point for sensor 2 LSB. |
| 6 | 2 | Low alarm set point for sensor 3 MSB. |
| 7 | 2 | Low alarm set point for sensor 3 LSB. |
| 8 | 2 | Low alarm set point for sensor 4 MSB. |
| 9 | 2 | Low alarm set point for sensor 4 LSB. |
| 10 | 2 | Low alarm set point for sensor 5 MSB. |
| 11 | 2 | Low alarm set point for sensor 5 LSB. |
| 12 | 2 | Low alarm set point for sensor 6 MSB. |
| 13 | 2 | Low alarm set point for sensor 6 LSB. |
| 14 | 2 | Low alarm set point for sensor 7 MSB. |
| 15 | 2 | Low alarm set point for sensor 7 LSB. |

Writing any of these registers will reset high/low alarm conditions for that sensor.

The value is stored as a twos complement number as temperature * 100.

## High alarm registers

| Register | Page | Description |
| --- | --- | --- |
| 16 | 2 | High alarm set point for sensor 0 MSB. |
| 17 | 2 | High alarm set point for sensor 0 LSB. |
| 18 | 2 | High alarm set point for sensor 1 MSB. |
| 19 | 2 | High alarm set point for sensor 1 LSB. |
| 20 | 2 | High alarm set point for sensor 2 MSB. |
| 21 | 2 | High alarm set point for sensor 2 LSB. |
| 22 | 2 | High alarm set point for sensor 3 MSB. |
| 23 | 2 | High alarm set point for sensor 3 LSB. |
| 24 | 2 | High alarm set point for sensor 4 MSB. |
| 25 | 2 | High alarm set point for sensor 4 LSB. |
| 26 | 2 | High alarm set point for sensor 5 MSB. |
| 27 | 2 | High alarm set point for sensor 5 LSB. |
| 28 | 2 | High alarm set point for sensor 6 MSB. |
| 29 | 2 | High alarm set point for sensor 6 LSB. |
| 30 | 2 | High alarm set point for sensor 7 MSB. |
| 31 | 2 | High alarm set point for sensor 7 LSB. |

Writing any of these registers will reset high/low alarm conditions for that sensor.

The value is stored as a twos complement number as temperature * 100.

## Sensor absolute low temperature registers

| Register | Page | Description |
| --- | --- | --- |
| 32 | 2 | Absolute low for sensor 0 MSB (Write to reset). |
| 33 | 2 | Absolute low for sensor 0 LSB (Write to reset). |
| 34 | 2 | Absolute low for sensor 1 MSB (Write to reset). |
| 35 | 2 | Absolute low for sensor 1 LSB (Write to reset). |
| 36 | 2 | Absolute low for sensor 2 MSB (Write to reset). |
| 37 | 2 | Absolute low for sensor 2 LSB (Write to reset). |
| 38 | 2 | Absolute low for sensor 3 MSB (Write to reset). |
| 39 | 2 | Absolute low for sensor 3 LSB (Write to reset). |
| 40 | 2 | Absolute low for sensor 4 MSB (Write to reset). |
| 41 | 2 | Absolute low for sensor 4 LSB (Write to reset). |
| 42 | 2 | Absolute low for sensor 5 MSB (Write to reset). |
| 43 | 2 | Absolute low for sensor 5 LSB (Write to reset). |
| 44 | 2 | Absolute low for sensor 6 MSB (Write to reset). |
| 45 | 2 | Absolute low for sensor 6 LSB (Write to reset). |
| 46 | 2 | Absolute low for sensor 7 MSB (Write to reset). |
| 47 | 2 | Absolute low for sensor 7 LSB (Write to reset). |

The value is stored as a twos complement number as temperature * 100.  Writing any of the registers will rest the value.

## Sensor absolute high temperature registers

| Register | Page | Description |
| --- | --- | --- |
| 48 | 2 | Absolute high for sensor 0 MSB (Write to reset). |
| 49 | 2 | Absolute high for sensor 0 LSB (Write to reset). |
| 50 | 2 | Absolute high for sensor 1 MSB (Write to reset). |
| 51 | 2 | Absolute high for sensor 1 LSB (Write to reset). |
| 52 | 2 | Absolute high for sensor 2 MSB (Write to reset). |
| 53 | 2 | Absolute high for sensor 2 LSB (Write to reset). |
| 54 | 2 | Absolute high for sensor 3 MSB (Write to reset). |
| 55 | 2 | Absolute high for sensor 3 LSB (Write to reset). |
| 56 | 2 | Absolute high for sensor 4 MSB (Write to reset). |
| 57 | 2 | Absolute high for sensor 4 LSB (Write to reset). |
| 58 | 2 | Absolute high for sensor 5 MSB (Write to reset). |
| 59 | 2 | Absolute high for sensor 5 LSB (Write to reset). |
| 60 | 2 | Absolute high for sensor 6 MSB (Write to reset). |
| 61 | 2 | Absolute high for sensor 6 LSB (Write to reset). |
| 62 | 2 | Absolute high for sensor 7 MSB (Write to reset). |
| 63 | 2 | Absolute high for sensor 7 LSB (Write to reset). |

The value is stored as a twos complement number as temperature * 100.  Writing any of the registers will rest the value.

## Sensor hysteresis registers

| Register | Page | Description |
| --- | --- | --- |
| 64 | 2 | Hysteresis in degrees Celsius for sensor 0 (default is 5 degrees). |
| 65 | 2 | Hysteresis in degrees Celsius for sensor 1 (default is 5 degrees). |
| 66 | 2 | Hysteresis in degrees Celsius for sensor 2 (default is 5 degrees). |
| 67 | 2 | Hysteresis in degrees Celsius for sensor 3 (default is 5 degrees). |
| 68 | 2 | Hysteresis in degrees Celsius for sensor 4 (default is 5 degrees). |
| 69 | 2 | Hysteresis in degrees Celsius for sensor 5 (default is 5 degrees). |
| 70 | 2 | Hysteresis in degrees Celsius for sensor 6 (default is 5 degrees). |
| 71 | 2 | Hysteresis in degrees Celsius for sensor 7 (default is 5 degrees). |

## Sensor calibration registers

The value in the calibration register is added to the measured sensor value before it's reported. The calibration value is stored as a two's complement temperature * 100 to allow for both positive and negative numbers. So 24.23 degrees is stored as 2423 and so on. This means that 100 will add one degree to the measured value while 65436 (0xFF9c) is -100 and will subtract one degree form the measured value. If you are unsecure on how two complement umbers work there is an introduction here https://www.cs.cornell.edu/~tomf/notes/cps104/twoscomp.html

| Register | Page | Description |
| --- | --- | --- |
| 72 | 2 | MSB of calibration value for sensor 0. |
| 73 | 2 | LSB of calibration value for sensor 0. |
| 74 | 2 | MSB of calibration value for sensor 1. |
| 75 | 2 | LSB of calibration value for sensor 1. |
| 76 | 2 | MSB of calibration value for sensor 2. |
| 77 | 2 | LSB of calibration value for sensor 2. |
| 78 | 2 | MSB of calibration value for sensor 3. |
| 79 | 2 | LSB of calibration value for sensor 3. |
| 80 | 2 | MSB of calibration value for sensor 4. |
| 81 | 2 | LSB of calibration value for sensor 4. |
| 82 | 2 | MSB of calibration value for sensor 5. |
| 83 | 2 | LSB of calibration value for sensor 5. |
| 84 | 2 | MSB of calibration value for sensor 6. |
| 85 | 2 | LSB of calibration value for sensor 6. |
| 86 | 2 | MSB of calibration value for sensor 7. |
| 87 | 2 | LSB of calibration value for sensor 7. |
| 88 | 2 | MSB of calibration value for on board temperature sensor. |
| 89 | 2 | LSB of calibration value for on board temperature sensor. |

# Page 3

### Channel control register

- Writing a one to bit 0 will search for the first two temperature sensors that an be found on channel 1 and save there address information in the address array.
- Writing a one to bit 1 will search for the first two temperature sensors that an be found on channel 2 and save there address information in the address array.
- Writing a one to bit 2 will search for the first two temperature sensors that an be found on channel 3 and save there address information in the address array.
- Writing a one to bit 3 will search for the first two temperature sensors that an be found on channel 4 and save there address information in the address array.

The array is filled with the first found sensor in index position zero and the next found sensor in the index position one. This mean that if there are more sensors in attached thy will not be visible to the module but the functionality will be the same. Only DS1820, DS18S20 and DS18B20 is recognized.

It is also possible to enter the ROM codes manually.

The sensor search is the the most sensitive operation of the 1-wire protocol. If you have long cable lengths ( >5 meters) and/or bad cables and/or are in a bad environment. you may need to do the search several times to find the sensors on a channel. One way around this is to get the sensors ROM code and set it manually (search it with the sensor at a closer distance) and after that mount it on the long cable. [There is a paper here](https://www.maximintegrated.com/en/app-notes/index.mvp/id/148) discussing how to use long cable runs on 1-wire networks.

A [CLASS1.INFORMATION, Type=37, Token activity event](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_37_0x25_token_activity) is sent for each found device on the one wire bus is the corresponding bit in the upper half nibble is set.

Will always read as zero.

| Register | Page | Description |
| --- | --- | --- |
| 0 | 3 | Channel control register |

| Bit | Description |
| --- | --- |
| 0 | Channel 0 ROM code find is performed if the channel control register is written with this bit set. |
| 1 | Channel 1 ROM code find is performed if the channel control register is written with this bit set. |
| 2 | Channel 2 ROM code find is performed if the channel control register is written with this bit set. |
| 3 | Channel 3 ROM code find is performed if the channel control register is written with this bit set. |
| 4 | [CLASS1.INFORMATION, Type=37, Token activity](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_37_0x25_token_activity) events are sent for all found devices on channel 0. Note that the event is sent for all found not only the two temperature sensors that when found are placed in the ROM code array if the corresponding low nibble bit also is set. |
| 5 | [CLASS1.INFORMATION, Type=37, Token activity](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_37_0x25_token_activity) events are sent for all found devices on channel 1. Note that the event is sent for all found not only the two temperature sensors that when found are placed in the ROM code array if the corresponding low nibble bit also is set. |
| 6 | [CLASS1.INFORMATION, Type=37, Token activity](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_37_0x25_token_activity) events are sent for all found devices on channel 2. Note that the event is sent for all found not only the two temperature sensors that when found are placed in the ROM code array if the corresponding low nibble bit also is set. |
| 7 | [CLASS1.INFORMATION, Type=37, Token activity](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.information#type_37_0x25_token_activity) events are sent for all found devices on channel 3. Note that the event is sent for all found not only the two temperature sensors that when found are placed in the ROM code array if the corresponding low nibble bit also is set. |

### ROM code registers

64-Bit Lasered ROM Code for sensors connected to **channel 0**. Initialized to zero.

| Register | Page | Description |
| --- | --- | --- |
| 1 | 3 | CRC of ROM Code for sensor 0 MSB |
| 2 | 3 | 48 bit serial of ROM Code for sensor 0 (Stored big endian) |
| 3 | 3 | 48 bit serial of ROM Code for sensor 0 (Stored big endian) |
| 4 | 3 | 48 bit serial of ROM Code for sensor 0 (Stored big endian) |
| 5 | 3 | 48 bit serial of ROM Code for sensor 0 (Stored big endian) |
| 6 | 3 | 48 bit serial of ROM Code for sensor 0 (Stored big endian) |
| 7 | 3 | 48 bit serial of ROM Code for sensor 0 (Stored big endian) |
| 8 | 3 | 8 bit family code of ROM Code for sensor 0 |
| 9 | 3 | CRC of ROM Code for sensor 1 MSB |
| 10 | 3 | 48 bit serial of ROM Code for sensor 1 (Stored big endian) |
| 11 | 3 | 48 bit serial of ROM Code for sensor 1 (Stored big endian) |
| 12 | 3 | 48 bit serial of ROM Code for sensor 1 (Stored big endian) |
| 13 | 3 | 48 bit serial of ROM Code for sensor 1 (Stored big endian) |
| 14 | 3 | 48 bit serial of ROM Code for sensor 1 (Stored big endian) |
| 15 | 3 | 48 bit serial of ROM Code for sensor 1 (Stored big endian) |
| 16 | 3 | 8 bit family code of ROM Code for sensor 1 |

64-Bit Lasered ROM Code for sensors connected to **channel 1**. Initialized to zero.

| Register | Page | Description |
| --- | --- | --- |
| 17 | 3 | CRC of ROM Code for sensor 2 MSB |
| 18 | 3 | 48 bit serial of ROM Code for sensor 2 (Stored big endian) |
| 19 | 3 | 48 bit serial of ROM Code for sensor 2 (Stored big endian) |
| 20 | 3 | 48 bit serial of ROM Code for sensor 2 (Stored big endian) |
| 21 | 3 | 48 bit serial of ROM Code for sensor 2 (Stored big endian) |
| 22 | 3 | 48 bit serial of ROM Code for sensor 2 (Stored big endian) |
| 23 | 3 | 48 bit serial of ROM Code for sensor 2 (Stored big endian) |
| 24 | 3 | 8 bit family code of ROM Code for sensor 2 |
| 25 | 3 | CRC of ROM Code for sensor 3 MSB |
| 26 | 3 | 48 bit serial of ROM Code for sensor 3 (Stored big endian) |
| 27 | 3 | 48 bit serial of ROM Code for sensor 3 (Stored big endian) |
| 28 | 3 | 48 bit serial of ROM Code for sensor 3 (Stored big endian) |
| 29 | 3 | 48 bit serial of ROM Code for sensor 3 (Stored big endian) |
| 30 | 3 | 48 bit serial of ROM Code for sensor 3 (Stored big endian) |
| 31 | 3 | 48 bit serial of ROM Code for sensor 3 (Stored big endian) |
| 32 | 3 | 8 bit family code of ROM Code for sensor 3 |

64-Bit Lasered ROM Code for sensors connected to **channel 2**. Initialized to zero.

| Register | Page | Description |
| --- | --- | --- |
| 33 | 3 | CRC of ROM Code for sensor 4 MSB |
| 34 | 3 | 48 bit serial of ROM Code for sensor 4 (Stored big endian) |
| 35 | 3 | 48 bit serial of ROM Code for sensor 4 (Stored big endian) |
| 36 | 3 | 48 bit serial of ROM Code for sensor 4 (Stored big endian) |
| 37 | 3 | 48 bit serial of ROM Code for sensor 4 (Stored big endian) |
| 38 | 3 | 48 bit serial of ROM Code for sensor 4 (Stored big endian) |
| 39 | 3 | 48 bit serial of ROM Code for sensor 4 (Stored big endian) |
| 40 | 3 | 8 bit family code of ROM Code for sensor 4 |
| 41 | 3 | CRC of ROM Code for sensor 5 MSB |
| 42 | 3 | 48 bit serial of ROM Code for sensor 5 (Stored big endian) |
| 43 | 3 | 48 bit serial of ROM Code for sensor 5 (Stored big endian) |
| 44 | 3 | 48 bit serial of ROM Code for sensor 5 (Stored big endian) |
| 45 | 3 | 48 bit serial of ROM Code for sensor 5 (Stored big endian) |
| 46 | 3 | 48 bit serial of ROM Code for sensor 5 (Stored big endian) |
| 47 | 3 | 48 bit serial of ROM Code for sensor 5 (Stored big endian) |
| 48 | 3 | 8 bit family code of ROM Code for sensor 5 |

64-Bit Lasered ROM Code for sensors connected to **channel 3**. Initialized to zero.

| Register | Page | Description |
| --- | --- | --- |
| 49 | 3 | CRC of ROM Code for sensor 6 MSB |
| 50 | 3 | 48 bit serial of ROM Code for sensor 6 (Stored big endian) |
| 51 | 3 | 48 bit serial of ROM Code for sensor 6 (Stored big endian) |
| 52 | 3 | 48 bit serial of ROM Code for sensor 6 (Stored big endian) |
| 53 | 3 | 48 bit serial of ROM Code for sensor 6 (Stored big endian) |
| 54 | 3 | 48 bit serial of ROM Code for sensor 6 (Stored big endian) |
| 55 | 3 | 48 bit serial of ROM Code for sensor 6 (Stored big endian) |
| 56 | 3 | 8 bit family code of ROM Code for sensor 6 |
| 57 | 3 | CRC of ROM Code for sensor 7 MSB |
| 58 | 3 | 48 bit serial of ROM Code for sensor 7 (Stored big endian) |
| 59 | 3 | 48 bit serial of ROM Code for sensor 7 (Stored big endian) |
| 60 | 3 | 48 bit serial of ROM Code for sensor 7 (Stored big endian) |
| 61 | 3 | 48 bit serial of ROM Code for sensor 7 (Stored big endian) |
| 62 | 3 | 48 bit serial of ROM Code for sensor 7 (Stored big endian) |
| 63 | 3 | 48 bit serial of ROM Code for sensor 7 (Stored big endian) |
| 64 | 3 | 8 bit family code of ROM Code for sensor 7 |

<br>

---

![](media/grodan_logo.png ':size=100')

<center>
<b>Paradise of the Frog AB</b> Brattbergavägen 17, 820 50 LOS, SWEDEN<br />
<b>email:</b> <a href="info@grodansparadis.com">info@paradiseofthefrog.com</a> <b>phone:</b> +46 (0)8 40011835<br />
<b>web:</b> <a href="http://www.grodansparadis.com">http://www.paradiseofthefrog.com</a><br>
</center>
