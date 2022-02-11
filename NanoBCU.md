![NanoBCU_V00_10_soldered_top_-_Small](uploads/5bea8b60a5be1ba456cdcb73a39048fb/NanoBCU_V00_10_soldered_top_-_Small.jpg)

## Description 
A very compact bus coupling unit for KNX building automation based on the NCN5120 knx transceiver. It serves as a power supply and UART access to KNX bus, only 18mmx18mm.

## Hardware features
* IC: NCN5120 (ready for NCN5121 / 5130)
* Size: 18 x 18 x 9 mm (18 x 18 x 5 mm  see Superflat assembling option)
* Weight: about 4g
* Voltage 1: 3.3V
* Voltage 2 (optional): 5V (default), can be changed: 3.3V - 21V
* Ripple at VCC1+2: about 50-100mV (depends on load)
* Max. current: up to 100mA
* UART: 19200bps 8E1 / **3.3V**


## Sourcing
You can get soldering kits with almost all parts already be soldered [http://shop.sirsydom.de here] for a donation. Some soldering skills are still  neccessary.

## Final assembly

NanoBCU comes as a kit where the big parts on the bottom side have to be soldered:
* C4 - 100µF / 35V electrolytic capacitor. Polarization is important, refer to silkscreen or photo
* L1 and L2 - 220µH inductors
* R1 - 22R resistor 2512
* J1 - 7x1 2.54 pin header (or whatever you need to connect to your host PCB)
* D1 - SS16 reverse polarity protection diode. . Polarization is important, refer to silkscreen. The bar on the diode should match the bar on silkscreen.
* D2 - SMAJ40CA TVS diode

I recommend to solder the parts in this order: L2, L1, C4, R1, D1, D2, J1

A video showing the soldering process of the bottom parts is at [Youtube](https://www.youtube.com/watch?v=7OlGxEtVLzo)

### Superflat assembling option
alternative parts can be assembled to get a superflat version of the NanoBCU with only 5mm total height:
* C4 100µF / 35V tantalum cap: AVX TCN4107M035R0100E
* L1 and L2: Bourns SRR4028-221Y


### Change VCC2
To change VCC2, change R4 and R5 according the NCN5120 dataheet. When VCC2 is greater than 10V, C11 must be changed so that the voltage rating matches or exceeds VCC2 (e.g. when VCC2 = 12V, use a 16V MLCC)

### Enable High Bus current
For bus current consumption up to 20mA, J3 must be closed (This is the default, closed by a 0R resistor).

For bus current consumption of 10mA or less, J3 can be open.

## Ressources
* [Schematic V00.11](uploads/02566a04075eb806c84c439b383d20e7/NanoBCU_Schematic_V00.11.pdf)
* [[OpenKNX-KiCad-Lib]] symbol and footprints for different mounting options

## Software
There are various possibilities to use the NanoBCU.  
For embedded use we recommend the [OpenKNX stack](https://github.com/thelsing/knx)  
The protocol of the NCN5120 is compatible in almost every case to the TPUart, so it can replace the use of the Siemens BCU or other products featuring TPUart.


## Developer Documentation
### Version history
* V00.10 - first prototype series and first public beta series
* V00.11 - changed C4 cap footprint for alternative use of a flat tantalum cap, reduced PCB thickness to 1.0mm

### Use with NCN5121/5130
The NanoBCU PCB also works with NCN5121 and NCN5130 with following adaptions:
* R1 27R (was: 22R)
* C2 220nF (was: 4.7nF)
* R4 180k (was: 33k)
* R5 56k (was: 180k)

### Accessories

* BCU Breadboard Adapter
* ItsyBitsy BCU Connector
* PiPico BCU Connector

### Devices using NanoBCU

* DualKNX RasPi HAT
* OpenKNX UP1 devices

## Links

[Vorstellungs- / Entwicklunsthread im KNX User Forum](https://knx-user-forum.de/forum/projektforen/konnekting/1603350-nanobcu-ncn5120-weiterentwicklung-der-microbcu2)

[1. Sammelbestellung im KNX User Forum](https://knx-user-forum.de/forum/projektforen/konnekting/1575881-sammelbestellung-microbcu2-knx-transceiver-für-ardunio-raspberry-co)

[OnSemi NCN5120 Datasheet](https://www.google.de/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&cad=rja&uact=8&ved=2ahUKEwjZ_46X2aftAhUxvlkKHbOJCF4QFjAAegQIBBAC&url=https%3A%2F%2Fwww.onsemi.com%2Fpub%2FCollateral%2FNCN5120-D.PDF&usg=AOvVaw0KUimWgup68HXisop9pYTW)

## Pictures
![NanoBCU_V00_10_soldered_top](uploads/39cf40b113a667caeb40db8885e14c2f/NanoBCU_V00_10_soldered_top.jpg)

![NanoBCU_V00_11_soldered_bottom_superflat](uploads/4eb3e9b17a80af47826e34e76cc09f6a/NanoBCU_V00_11_soldered_bottom_superflat.jpg)