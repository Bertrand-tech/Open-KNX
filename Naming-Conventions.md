## Device names
all devices should be named reagrding this rules

### Device-Class:

* TAS - Taster
* SA - Schaltaktor 
* JA - Jalousieaktor
* HA - Heizungsaktor
* GW - Gateway
* VIS - Visualisierung
* DIM - 230V Dimmer  
* LED - LED-Controller  
* BE - Binäreingang  
* SYS - Systemgeräte IP USB SER
* SEN - Sensor-Modul
* BM - Bewegungsmelder
* PM - Präsenzmelder
* VPM - Virtueller Präsenzmelder
* LM - Logik-Modul
* BEM - Bewässerungsmodul

### System:

* REGn - Reiheneinbaugerät für Hutschiene 35mm, n = Anzahl TE
* UP - Unterputzgerät für den Einbau in Schalterdosen
* UP1 - OenKNX-UP1 System

### Naming of a complete device

`<Device-Class>-[<System>]-[<NumberOfChannels>x]<Channeldescription>`

(parts in [] are optional)

**Examples:**  
* BE-REG4-28xPOT
* GW-30xENOCEAN
* LED-UP1-6x24V
* SA-UP-1x230V
* JA-RF-2x230V
* SEN-UP1-8xTH
* TAS-UP1-TouchRGB
* LED-REG9-24x24V
* GW-DALI

## Software modules

OpenKNX will also provide reusable software modules, which can be adopted to community hardware.
The following prefixes will classify the repositories:

* OAM - OpenKNX Application Module - Contains usually a complete application (firmware and ETS-Application), which can be combined with other OAM, but can also be used standalone
* OFM - OpenKNX Function Module - Contains usually a reusable part for an application (firmware and ETS-parts) like an IO-channel or a humidity sensor. Can be used in an own application or as an implementation idea.
* OGM - OpenKNX Generic Module - any generic or common implementations used in OpenKNX

## Manufacturer ID 

OpenKNX uses 0x00 FA

##  Hardware Type 

The Hardwaretype Property is 6 bytes long where the first is reserved.  
OpenKNX uses 0x00 00 Ap xx xx xx  
where p is unique for one developer  
and xx is any value

It is recommende to use
0x00 00 Ap nn vv 00  
where Ap nn is the ApplicationNumber  
and vv is the ApplicationVersion 