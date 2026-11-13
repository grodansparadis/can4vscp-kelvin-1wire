# Decision Matrix

# Decision Matrix

The full functionality of the decision matrix is explained [in the specification](http://www.vscp.org/docs/vscpspec/doku.php?id=decision_matrix).

The module have a decision matrix consisting of eight entries. This matrix can be used to control the scanning of channels. Possible actions are listed in the table below.

| Action | Action code | Parameter | Description |
| --- | --- | --- | --- |
| **NOOP** | 0 | Not used | No operation. Will do absolutely nothing. |
| **Scan** | 1 | Bit-array for channels. | Scan for ROM codes for channel which have bit set. Bit 1 is channel 0m bit 2 is channel 1 ans so on. |
| **Scan and Store** | 2 | Bit-array for channels | Scan for ROM codes for channel which have bit set and store result.  Bit 1 is channel 0, bit 2 is channel 1 and so on. |
| **Report** | 3 | Bit-array for sensors | Report temperature for sensors that have bit in array set. Bit0 = Sensor 0, Bit1 = Sensor 2 and so on. |
| **Clear alarm** | 4 | Not used | Clear alarm flags. |
| **Clear high** | 5 | Bit array for sensors. | Clear absolute high value for sensor(s) identified by bit-array. Bit0 = Sensor 0, Bit1 = Sensor 2 and so on. |
| **Clear low** | 6 | Bit array for sensors. | Clear absolute low value for sensor(s) identified by bit-array. Bit0 = Sensor 0, Bit1 = Sensor 2 and so on. |

The bit arrays have a bit for each channel. So 1 (0x0001) is channel 0 and 2 (0b0010) is channel 1, and 4 (0x0100) is channel 2 and 8(0x1000) is channel 3. It is also possible to assign several channels  so that 15 (0x1111) is all channels and 3 (0x0011) is channel 0 + 1.

<br>

---

![](media/grodan_logo.png ':size=100')

<center>
<b>Paradise of the Frog AB</b> Brattbergavägen 17, 820 50 LOS, SWEDEN<br />
<b>email:</b> <a href="info@grodansparadis.com">info@paradiseofthefrog.com</a> <b>phone:</b> +46 (0)8 40011835<br />
<b>web:</b> <a href="http://www.grodansparadis.com">http://www.paradiseofthefrog.com</a><br>
</center>
