JVC Remote
==========

### Pinout ###

[26pin_studio_10pin_remote_6pin_tally.xls](cable_doku/26pin_studio_10pin_remote_6pin_tally.xls)

Es wird nur der Remote Anschluß benötigt.<br />
Der Stecker ist ein gewönlicher 6pin Mini-Din (der PS/2 Stecker) Anschluß.<br />
Zum Beispiel: <http://www.reichelt.de/SE-DIO-M06/3/index.html?&ACTION=3&LA=446&ARTICLE=17457&artnr=SE-DIO+M06>

Protokoll
---------

Signallevel: 3.3V<br />
Format: 9600baud 1E8 (8 daten, 1 stop-bit, even-parity)

### Protocol Flow ###

#### Typical Sequence ####
<table >
	<thead>
	<tr >
		<th  colspan="5"> Normal CCU to CAM flow </th>
	</tr>
	</thead>
	<tr >
		<th > Direction (seen from OCP) </th>
        <td >  TX       </td>
        <td >  RX  </td>
        <td >  TX   </td>
        <td >  RX  </td>
	</tr>
	<tr >
		<th > length (in Byte)            </th>
        <td >  1        </td>
        <td >  1   </td>
        <td >  3-4  </td>
        <td >  1   </td>
	</tr>
	<tr >
		<th > Purpose </th>
        <td > Startbyte </td>
        <td > ACK  </td>
        <td > Data </td>
        <td > ACK  </td>
	</tr>
</table>
Note: there is also the possibility to do CAM to CCU communication, <br />
which seems to be requested by a special char (0x90)


<table >
	<thead>
	<tr >
		<th  colspan="9">  Startbyte    </th>
	</tr>
	</thead>
	<tr >
		<th > Bit      </th>
        <td >  0        </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
	</tr>
	<tr >
		<th > Purpose </th>
        <td >  always 1 </td>
        <td colspan="4"> 0 </td>
        <td colspan="3"> number of data bytes </td>
	</tr>
</table>

##### Speculative interpretation of ACK byte: #####
<table>
   <tr>
    <th colspan="9">ACK byte</th>
   </tr>
   <tr>
    <th>Bit</th>
    <td>0</td>
    <td>1</td>
    <td>2</td>
    <td>3</td>
    <td>4</td>
    <td>5</td>
    <td>6</td>
    <td>7</td>
  </tr>
  <tr>
    <th>Funktion</th>
    <td> ACK</td>
    <td> UNIMPL </td>
    <td> ACK </td>
    <td> UNIMPL </td>
    <td colspan="2">0</td>
    <td> UNIMPL </td>
    <td> 0 </td>
  </tr>
</table>

0xA0 => transmission understood, everything OK<br />
0xF2 => transmission understood, but Feature not implemented

##### Data bytes: #####
4 Byte:

<table >
	<thead>
	<tr >
		<th  colspan="33">  Daten    </th>
	</tr>
	</thead>
	<tr >
		<th > Byte     </th>
        <td  colspan="8">  0  </td>
        <td  colspan="8">  1  </td>
        <td  colspan="8">  2  </td>
        <td  colspan="8">  3  </td>
	</tr>
	<tr >
		<th > Bit      </th>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
	</tr>
	<tr >
		<th > Purpose </th>
        <td  colspan="12"> key </td>
        <td  colspan="12"> value </td>
        <td  colspan="8"> checksum </td>
	</tr>
</table>

3 Byte:


<table >
	<thead>
	<tr >
		<th  colspan="25"> Data </th>
	</tr>
	</thead>
	<tr >
		<th > Byte     </th>
        <td  colspan="8">  0  </td>
        <td  colspan="8">  1  </td>
        <td  colspan="8">  2  </td>
	</tr>
	<tr >
		<th > Bit      </th>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
        <td >  0  </td>
        <td >  1  </td>
        <td >  2  </td>
        <td >  3  </td>
        <td >  4  </td>
        <td >  5  </td>
        <td >  6  </td>
        <td >  7  </td>
	</tr>
	<tr >
		<th > Purpose </th>
        <td  colspan="8">  Command  </td>
        <td  colspan="4">  Bitflags  </td>
        <td  colspan="4">  Set Value </td>
        <td  colspan="8">  Checksum  </td>
	</tr>
</table>

Flags are mostly set to 0x4, <br />
but sometimes 0x6

                                                                       

### Funktionen ###

from cmds.csv

cmd => 3 byte<br />
key => 4 byte

|cmd type|key|value|bitfield|cam response|topic|setting|
|--------|---|-----|--------|------------|-----|-------|
|cmd|0x00|0x0|0b0100|IMPL|Colorbars||
||||||||
|cmd|0x01|0x0|0b0100|IMPL|Detail||
||||||||
|cmd|0x02|0x0|0b0100|IMPL|Autoiris||
|cmd|0x02|0x1|0b0100|IMPL|Autoiris||
||||||||
|cmd|0x03|0x0|0b0100|IMPL|White Bal||
|cmd|0x03|0x1|0b0100|IMPL|White Bal|Preset|
|cmd|0x03|0x2|0b0100|IMPL|White Bal|A|
|cmd|0x03|0x3|0b0100|IMPL|White Bal|B|
|cmd|0x03|0xf|0b0100|IMPL|White Bal|full auto|
||||||||
|cmd|0x06|0x0|0b0110|UNIPLM|Auto White||
|cmd|0x06|0x1|0b0110|IMPL|Auto White||
||||||||
|cmd|0x07|0x0|0b0100|IMPL|Gain|0dB|
|cmd|0x07|0x1|0b0100|IMPL|Gain|6dB|
|cmd|0x07|0x2|0b0100|IMPL|Gain|9dB|
|cmd|0x07|0x3|0b0100|IMPL|Gain|12dB|
|cmd|0x07|0x4|0b0100|IMPL|Gain|18dB|
|cmd|0x07|0x5|0b0100|UNIPLM|Gain||
|cmd|0x07|0x6|0b0100|UNIPLM|Gain||
|cmd|0x07|0x8|0b0100|IMPL|Gain||
|cmd|0x07|0xa|0b0100|IMPL|Gain|3dB|
|cmd|0x07|0xe|0b0100|UNIPLM|Gain||
||||||||
|cmd|0x08|0x0|0b0100|IMPL|||
|cmd|0x08|0x1|0b0100|IMPL|||
||||||||
|cmd|0x09|0x0|0b0100|IMPL|Call||
|cmd|0x09|0x1|0b0100|IMPL|Call||
||||||||
|cmd|0x0b|0x0|0b0110|UNIPLM|||
||||||||
|cmd|0x0c|0x0|0b0100|IMPL|Shutter|off|
|cmd|0x0c|0x1|0b0100|UNIPLM|Shutter||
|cmd|0x0c|0x2|0b0100|IMPL|Shutter|1/120|
|cmd|0x0c|0x3|0b0100|IMPL|Shutter|1/250|
|cmd|0x0c|0x4|0b0100|IMPL|Shutter|1/500|
|cmd|0x0c|0x5|0b0100|IMPL|Shutter|1/1000|
|cmd|0x0c|0x6|0b0100|IMPL|Shutter|1/2000|
|cmd|0x0c|0xf|0b0100|UNIPLM|Shutter||
||||||||
|cmd|0x0f|0x0|0b0100|IMPL|black mod|unmod|
|cmd|0x0f|0x1|0b0100|IMPL|black mod|stretch|
|cmd|0x0f|0x2|0b0100|IMPL|black mod|compress|
||||||||
|cmd|0x1b|0x0|0b0100|UNIPLM|||
|cmd|0x1b|0x1|0b0100|UNIPLM|||
||||||||
|cmd|0x1c|0x0|0b0100|IMPL|Auto Knee||
||||||||
|cmd|0x1d|0x0|0b0100|IMPL|||
||||||||
|cmd|0x4a|0x0|0b0100|IMPL|DNR||
||||||||
|cmd|0x4b|0x0|0b0100|UNIPLM|||
|cmd|0x4b|0x1|0b0100|UNIPLM|||
|cmd|0x4b|0x2|0b0100|UNIPLM|||
|cmd|0x4b|0xf|0b0100|UNIPLM|||
||||||||
|cmd|0x4c|0x0|0b0100|IMPL|||
|cmd|0x4c|0x1|0b0100|IMPL|||
|cmd|0x4c|0x2|0b0100|IMPL|||
|cmd|0x4c|0xf|0b0100|UNIPLM|||
||||||||
|cmd|0x4d|0x0|0b0100|IMPL|Skin Detail||
||||||||
|cmd|0x4e|0x1|0b0100|UNIPLM|||
||||||||
|cmd|0x4f|0x0|0b0100|UNIPLM|||
|cmd|0x4f|0x1|0b0100|UNIPLM|||
|cmd|0x4f|0x2|0b0100|UNIPLM|||
||||||||
|cmd|0x50|0x1|0b0100|IMPL|||
||||||||
|cmd|0x51|0x0|0b0100|UNIPLM|||
|cmd|0x51|0x1|0b0100|UNIPLM|||
||||||||
|cmd|0x52|0x0|0b0100|IMPL|||
||||||||
|cmd|0x53|0x0|0b0100|IMPL|||
|cmd|0x53|0x1|0b0100|IMPL|||
||||||||
|cmd|0x7d|0x1|0b0100|IMPL|||
||||||||
|key|0x00|0x340||IMPL|Iris||
||||||||
|key|0x02|0x33c||IMPL|||
||||||||
|key|0x03|0x368||IMPL|||
||||||||
|key|0x06|0x310||IMPL|Black||
||||||||
|key|0x12|0x530||UNIPLM|||
||||||||
|key|0x14|0x400||IMPL|||
||||||||
|key|0x16|0x400||IMPL|||
||||||||
|key|0x26|0x328||IMPL|Red||
|key|0x26|0x404||IMPL|Red||
||||||||
|key|0x27|0x230||IMPL|Blue||
|key|0x27|0x41c||IMPL|Blue||
||||||||
|key|0x32|0x604||IMPL|||
||||||||
|key|0x36|0x114||IMPL|||
||||||||
|key|0x40|0x340||IMPL|Autoiris||
||||||||
|key|0x56|0x26e||UNIPLM|||
||||||||
|key|0x74|0x801||UNIPLM|||
||||||||
|key|0xf2|0x008||UNIPLM|||
|key|0xf2|0x00c||UNIPLM|||
|key|0xf2|0x80c||UNIPLM|||
||||||||
|key|0xf3|0x00c||UNIPLM|||
|key|0xf3|0xf7c||UNIPLM|||
