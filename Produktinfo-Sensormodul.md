## Vorstellung

OAM-SensorModule implementiert ein Raum-Sensormodul, mit dem man verschiedene I²C-basierte Sensoren dem KNX-Bus zur Verfügung stellt.

Unterstützt werden derzeit:

* Temperatur - BME680, BME620, SHT3x, SCD4x, SCD30 (abgelöst)
* Luftfeuchte - BME680, BME620, SHT3x, SCD4x, SCD30 (abgelöst)
* Luftdruck - BME680, BME280
* VOC - BME680, IAQCore
* CO<sub>2</sub> - BME680, SCD4x, SCD30 (abgelöst)
* Helligkeit - OPT3001, VEML7700
* Entfernung - VL53L1X

## Übersicht Funktionen

Klassische Sensorapplikation mit Messung von:

* Temperatur
* Luftfeuchte
* Luftdruck
* VOC
* CO<sub>2</sub>
* Helligkeit
* Entfernung

Jeder Messwert kann

* über einen Offset kalibriert werden
* Zyklisch senden über Zeitangabe
* Zyklisch senden bei absoluter Abweichung von vorherigen Wert
* Zyklisch senden bei relativer Abweichung von vorherigen Wert

Es können berechnete Werte ermittelt werden

* Taupunktberechnung bei Verfügbarkeit von Temperatur und Luftfeuchte
* Behaglichkeitszone bei Verfügbarkeit von Temperatur und Luftfeuchte
* Luftqualitätsampel bei Verfügbarkeit von VOC oder CO<sub>2</sub>
* Gewichtete Berücksichtigung von bis zu 2 weiteren Messwerten
* Glättung von Messwerten (Glättung von Ausreißern)

Es gibt Sensormodul-Firmwarevarianten kombiniert mit dem 1-Wire-Modul, dem Präsenzmodul und dem Logikmodul.

## Applikationsbeschreibung

Die aktuelle Applikationsbeschreibung ist hier zu finden: [Applikationsbeschreibung-Sensor](../../OAM-SensorModule/blob/main/doc/Applikationbeschreibung-Sensor.md)

Die aktuelle Applikationsbeschreibung für das eventuell enthaltene OneWire-Modul ist hier zu finden: [Applikationsbeschreibung-Wire](../../OAM-OneWireModule/blob/main/doc/Applikationbeschreibung-Wire.md)

Die aktuelle Applikationsbeschreibung für das eventuell enthaltene Präsenzmodul ist hier zu finden: [Applikationsbeschreibung-Präsenz](../../OAM-PresenceModule/blob/main/doc/Applikationbeschreibung-Praesenz.md)

Die aktuelle Applikationsbeschreibung für das enthaltene Logikmodul ist hier zu finden: [Applikationsbeschreibung-Logik](../../OAM-LogicModule/blob/main/doc/Applikationsbeschreibung-Logik.md)
 
## Hardware

### Hardwareplattformen

Zur Hardwareplattform gilt das gleiche wie beim [Logikmodul](Logikmodul-%E2%80%90-Produktinfo#hardwareplattformen) beschrieben.

### Verfügbare Hardware

Die Software läuft auf folgender Hardware "out-of-the-box":

* **Smart-MF Sensormodul** [www.smart-mf.de](https://www.smart-mf.de), als virtueller Präsenzmelder, um die Applikationen von alten oder unzuverlässigen Präsenzmeldern zu verbessern. Das Sensormodul ist als v3.1 (SAMD) und als v4.0 (RP2040) verfügbar.

## Verwendet

Das Sensormodul wird in keinem anderen Modul verwendet.

## Releases

Das Sensormodul ist in der [Version 1.1.3](../../OAM-SensorModule/releases/tag/1.1.3-Release) freigegeben. 

Es gibt 3 Varianten des Sensormoduls:

* SensorModule-Big mit Sensoren, 30 1-Wire-Geräten, 40 Präsenzkanälen und 99 Logikkanälen, nur für den RP2040 verfügbar.
* SensorModule-OneWire mit Sensoren, 30 1-Wire-Geräten und 80 Logikkanälen, sowohl für den SAMD wie auch für den RP2040 verfügbar.
* SensorModule-Vpm mit Sensoren, 5 Präsenzkanälen und 70 Logikkanälen, sowohl für den SAMD wie auch für den RP2040 verfügbar.

> Hinweis: Wenn man den RP2040-Prozessor nutzt, sollte man die SensorModule-Big-Variante nutzen.

## Änderungshistorie

Eine detaillierte Änderungshistorie findet ihr immer am Anfang der [Applikationsbeschreibung-Sensor](../../OAM-SensorModule/blob/main/doc/Applikationbeschreibung-Sensor.md#änderungshistorie).

Im Folgenden werden nur größere Änderungen aufgeführt:

### Firmware 1.1.3, Applikation 1.1

* Erste offizielle OpenKNX-Firmware für das Sensormodul

