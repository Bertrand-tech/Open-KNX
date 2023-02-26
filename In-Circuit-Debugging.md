Currently in the OpenKNX project two ICEs are used:

* The Segger J-Link Mini Edu, availible for 40€ at [AK MODUL-BUS](https://www.ak-modul-bus.de/cgi-bin/iboshop.cgi?showd0!0,955193676423176,J-Link_EDU__MINI)

* PicoProbe

both work "out-of-the-box" with PLattform I/O, use
`debug_tool = jlink` or `debug_tool = picoprobe` in the plattformio.ini

## Hints

* Flashing an empty RP2040 with J-Link seems to be not possible
* J-Link does not supply 3.3V, device must be powered seperately
* be carefull with potential differences, use USB isolators
