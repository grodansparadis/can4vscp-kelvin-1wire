# Configure the module

You configure a VSCP module by writing content into the modules registers. You can do this manually or with the wizard available in VSCP works. Using the wizard is absolutely the easiest way to accomplish different things.

## Sensor calibration

DS1820, [DS18S20](https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/DS18S20.html) and [DS18B20](https://www.maximintegrated.com/en/products/analog/sensors-and-sensor-interface/DS18B20.html) does not need any calibration and they measures temperatures from -55°C to +125°C (-67°F to +257°F) with a ±0.5°C accuracy from -10°C to +85°C

The resolution for the DS1820 is 0.5°C and 0.0625°C for the DS18S20 and the DS18B20 ([read more about this here](https://www.maximintegrated.com/en/app-notes/index.mvp/id/4377)).

If you feel a sensor is off you can calibrate it with the [Sensor calibration registers](registers.md?id=sensor-calibration-registers). The calibration registers hold a twos complement times hundred calibration value that is added to the temperature read from the sensor before it is used or reported.

![](media/calibration.jpg ':size=700')

## Zones and sub zones

Zones and sub zones are used to group things together. Normally you don't address events to a certain receiver in VSCP ([CLASS1.PROTOCOL](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.protocol) being the exception that prove this rule). Instead you report/send things to a group of modules defined by a zone and a sub zone. The sender have no knowledge of how many units this zone/sub zone consist of. Well it does not even care.

Zone and sub zone for the module can be set in register [module zone registers](registers.md?id=module-zone-registers). But more useful than the module zone sub zone is the zone information for each individual sensor that is available in the [sensor zone registers](registers.md?id=sensor-zone-registers). Here you can specify the zone/sub zone units you think is interested in this event. You can also set them both (or one of them) to 0xff meaning all zones or all sub zones.

Think of a zone as a house, floor plan or similar and sub-zone as a room or a location. Note again that this is not an address. It's just a way to group functionality together. Or let the MSB bits of the zone be the floor plan, the LSB bits of the zone be the room on that floor plan and the sub zone be a group of functionality for that room.

It is good to think this through before you start to configure a system with VSCP modules.

## Sensor Control Registers

In the [Sensor Control Registers](registers.md?id=sensor-control-registers) you can configure how sensor data is reported and acted up on. You can set the unit you want temperatures to be reported in. You can enable alarms. You can define that TurnOn/TurnOff events should be sent when levels have been reached or data has been found to be below a certain level. And other things.

## Temperature measurements

If you have gone through the steps above you can now read temperature data in the [temperature registers](registers.md?id=temperature-registers). The temperature is shown in the selected unit as an integer which is temperature * 1000. The value is presented as a 24-bit floating point value. In the abstraction view of VSCP works you can get decimal values.

However usually this is not the way to get temperature readings. Instead you set a report interval for a sensor expressed in seconds in [report interval registers](registers.md?id=report-interval-registers) (or set to zero to turn of reporting) and get temperature readings automatically delivered/reported over the bus.

After entering a value here [temperature events](events.md?id=temperature-event-integer) will be sent with the configured interval. The receiver of this information can be another module, a routine that writes them to a database or a websocket widget that diagram them live on a screen or on a web page.

## Alarms

In the [low Alarm](registers.md?id=low-alarm-registers) and in the [high Alarm](registers.md?id=high-alarm-registers) registers you can set the level at which [alarm events](events.md?id=alarm-event) are sent.

An activated low alarm event (activated by setting bit 3 in the [sensor control registers](registers.md?id=sensor-control-registers))) is sent when the temperature is going below the low alarm value. When this happens the low alarm bit in the [standard alarm register](alarms.md) is set. This bit will only be rested by reading the alarm register. The alarm is considered active as long as the temperature is below the low alarm set point + the hysteresis value set in [sensor hysteresis registers](registers.md?id=sensor-hysteresis-registers). So if temperature moves above this point a new alarm event will be sent again when temperature again is moving below the set point.

An activated high alarm event (activated by setting bit 4 in the [sensor control registers](registers.md?id=sensor-control-registers)) is sent when the temperature is going above the high alarm value. When this happens the high alarm bit in the [standard alarm register](alarms.md) is set. This bit will only be rested by reading the alarm register. The alarm is considered active as long as the temperature is above the low alarm set point - the hysteresis value set in [sensor hysteresis registers](registers.md?id=sensor-hysteresis-registers). So if temperature moves below this point a new alarm event will be sent again when temperature again is moving above the set point.

It is possible to have continuous alarms events sent by setting bit 7 in the [sensor control registers](registers.md?id=sensor-control-registers)). An alarm event will be sent every second while the alarm condition persist.

## Controlling things

Instead of alarms [CLASS1.CONTROL, Type=5, TurnOn events](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_5_0x05_turnon) and [CLASS1.CONTROL, Type=6, TurnOn](http://www.vscp.org/docs/vscpspec/doku.php?id=class1.control#type_6_0x06_turnoff) events can be sent.  This functionality is activated by setting **bit 5** in the [control register](http://www.grodansparadis.com/kelvinntc10k/manual/doku.php?id=registers#description_of_control_register_bits).

Another bit, bit 6, in the control register decides when the TurnOff/TurnOn events are sent. If set to zero TurnOff is sent when the high point is reached and TurnOn when the low point is reached. Suitable for control of a heating system for example. If the bit is set the TurnOn event is sent at the high set point and the TurnOff is sent on the low set point. Suitable for a cooling system.

![](media/limits.png ':size=400')

The picture shows a real world example where a Kelvin NTC10K module measures temperature in a fridge which have its compressor controlled by a [Paris relay module](http://www.grodansparadis.com/paris/paris.html). The Paris [decision matrix](http://www.vscp.org/docs/vscpspec/doku.php?id=decision_matrix) is programmed to turn on the compressor when TurnOn events is received from the the zone/subzone programmed into the Kelvin NTC10K module sensor that measure the fridge temperature.

So here TurnOff events are sent by the Kelvin 1-wire module when the temperature go below -22 degrees Celsius. This event is received by the Paris module and it turn of the relay that controls the fridge compressor. Continuous mode is activated so the TurnOff events are sent until the temperature reach -20 degrees Celsius. A function to protect against events not being delivered.

When the temperature goes up above -20 degrees Celsius no events will be sent until the temperature go above -17 degrees Celsius. At this point TurnOn events will be sent which are received by the Paris module which turn on the relay that control the Fridge compressor. TurnOn events are sent continuously until the temperature go down to -19 degrees Celsius and again there will be a dead zone until the temperature falls to -22 degrees Celsius.

<br>

---

![](media/grodan_logo.png ':size=100')
<br>

<center>

**Paradise of the Frog AB** Brattbergavägen 17 820 50 LOS SWEDEN<br>
**email:** [info@grodansparadis.com](mailto:info@grodansparadis.com) **phone:** +46 (0)8 40011835 <br>
**web:**[http://www.grodansparadis.com](http://www.grodansparadis.com) <br>

</center>
