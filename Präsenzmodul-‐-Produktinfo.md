## Vorstellung

OAM-PresenceModule implementiert einen virtuellen Präsenzmelder (VPM). Es ist eine Präsenzmelder-Applikation, die Präsenz-, Bewegungs- und Helligkeits-Informationen von einem Gerät empfangen kann und anschließend wie ein Präsenzmelder agiert. Dadurch ergeben sich einige Anwendungsbereiche:

* VPM als Ersatz-Applikation für den Steinel True Presence (das war die Initial-Idee für diese Applikation)
* VPM als Applikation für 230V-Bewegungsmelder, die nur über einen Binäreingang am KNX angeschlossen sind (z.B Außenbeleuchtung)
* VPM als eine frische/neue Applikation für existierende ältere PM bzw. BWM, die mit ihrer eigenen Applikation nur die Grundbedürfnisse abdecken können und für die man neuere/modernere Funktionen erhalten möchte, ohne sich neue Hardware kaufen zu müssen
* PM-Applikaiton für unseren OpenKNX-RealPresence (nicht virtuell). Es hat inzwischen eine PM-Hardware-Eigenentwicklung vom OpenKNX-Projekt begonnen, die es auch ernöglicht, Präsenz ohne Bewegung festzustellen

## Übersicht Funktionen

## Applikationsbeschreibung

Die aktuelle Applikationsbeschreibung ist hier zu finden: [Applikationsbeschreibung-Logik](../../OAM-PresenceModule/blob/main/doc/Applikationsbeschreibung-Praesenz.md)
 
## Hardware

Die Software läuft auf folgender Hardware "out-of-the-box":

* **Smart-MF Sensormodul** [www.smart-mf.de](https://www.smart-mf.de), als Logikmodul mit der Option, über eine Zwischenplatine einen Buzzer und/oder einen RGB-LED-Signalgeber zu erhalten
* **PiPico-BCU-Connector** [OpenKNX-Wiki](https://github.com/OpenKNX/OpenKNX/wiki/PiPico-BCU-Connector), als Logikmodul
* **1TE-RP2040-Smart-MF** [www.smart-mf.de](https://www.smart-mf.de), auf allen Varianten als Logikmodul lauffähig
* **OpenKNX-UP1-System** [OpenKNX-Wiki](https://github.com/OpenKNX/OpenKNX/wiki/OpenKNX-UP1), auf allen Varianten als Logikmodul lauffähig

## Verwendet

Das Logikmodul wird in vielen OpenKNX-Modulen verwendet, in unterchiedlicher Kanalanzahl. Die Funktionalität ist somit auch in diesen Modulen verfügbar.
Die folgende Liste erhebt keinen Anspruch auf Vollständigkeit:

* OAM-PresenceModule - Präsenzmelder
* OAM-SensorModule - Sensormodul
* OAM-EnoceanGateway - Enocean Gateway
* OAM-ModubusGateway - Modbus RTU Gateway
* BEM-GardenControl - Bewässerungsautomat
* OAM-VirtualButton - Tastsensor
* OAM-SmartHomeBridge - HomeKit- and Philips-Hue-Bridge
* OAM-Dummy - Beispielprojekt für Neuentwicklungen

## Varianten

Das Logikmodul ist in der Version 1.5.1 verfügbar.




