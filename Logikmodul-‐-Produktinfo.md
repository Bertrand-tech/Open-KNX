## Vorstellung

OAM-LogicModule implementiert ein knx Logikmodul. Es stellt bis zu 99 Logikkanäle zur Verfügung, die jeweils 2 externe und 2 interne Eingänge und einen Ausgang haben. Somit erhält man viele einfache Kanäle, die zu größeren kombiniert werden können.

## Übersicht Funktionen

Logikfunktionen mit bis zu 4 Eingängen

* UND
* ODER
* EXOR
* TOR/Sperre
* Zeitschaltuhr
* Schalter (RS-Flip-Flop)

Einstellbare Ausgangstrigger

* Bei Wertänderung am Ausgang
* Bei jedem Eingangstelegramm
* Nur beim Eingangstelegramm am Eingang 1-4

Mehrere Kanäle können zu größeren Logikblöcken zusammengefasst werden

Eingänge unterstützen DPT 1, 2, 5, 5.001, 6, 7, 8, 9, 17

Ausgänge unterstützen zusätzlich noch DPT 16

Konvertierung zwischen Ein- und Ausgangs-DPT

Alle Ein- und Ausgänge 

* können ihre Werte invertieren
* sind als TRI-State-Versionen ausgeführt, sie verarbeiten bzw. senden erst Werte, wenn diese auf dem Signalweg definiert worden sind.

Eingänge können aktiv Werte lesen

* beim Startup
* Zyklisch mit einstellbarer Zeit
* Zyklisch bis die erste Antwort kommt

Eingänge können ihre Werte beim Stromausfall nichtflüchtig speichern, so dass diese nach einem Neustart zur Verfügung stehen  

Eingänge können intern direkt mit anderen KO verknüpft werden (ohne GA), wodurch keine Zwischenergebnisse auf den Bus erscheinen (reduzierung der Buslast)

Spezielle TOR-Funktionen

* TOR kann beim Öffnen und/oder beim Schließen zusätzliche Telegramme senden

  * konstant EIN
  * konstant AUS
  * Wert vom TOR-Eingang
  * nichts
  * Telegramme beim Öffnen sind unabhängig vom Schließen einstellbar

* TOR kann sofort nach dem Öffnen selbständig schließen (Impulseingang)

Wiederholfilter: Wenn mehrfach EIN- oder AUS-Telegramme hintereinander kommen, kann man

* Alle Wiederholungen durchlassen
* Nur EIN-Wiederholungen durchlassen, AUS nur einmal
* Nur AUS-Wiederholungen durchlassen, EIN nur einmal
* EIN- und AUS-Telegramm nur einmal durchlassen

Zeitglieder am Ausgang

* Treppenlicht mit Verlängerung und vorzeitigem Ausschalten (einstellbar)
* Einschaltverzögerung mit einstellbarer Aktion bei vorzeitigem AUS/wiederholtem EIN
* Ausschaltverzögerung mit einstellbarer Aktion bei vorzeitigem EIN/wiederholtem AUS
* Blinken mit wählbarem Puls-Pausen-Verhältnis
* Zyklisch senden getrennt einstellbar für EIN- und AUS-Telegramm
* Ausgangsfilter: nur EIN-, nur AUS oder beides durchlassen

Ausgangskonverter

* Für EIN oder AUS wird der Wert eines anderen DPT gesendet
* Für EIN oder AUS wird der Wert eines externen Eingangs gesendet
* Für EIN oder AUS wird der Wert eines beliebigen KO gesendet
* Für EIN oder AUS kann das Ergebnis einer Formel verwendet werden

Verfügbare Formeln

* Summe 
* Differenz
* Produkt
* Quotient
* Durchschnitt
* Modulo
* Bit-UND
* Bit-ODER
* Bit-EXOR
* Bit-Schieben nach links
* Bit-Schieben nach rechts
* Minimum
* Maximum
* 2-Bit zu Int 
* Glättung von Werten
* Es ist möglich bentzterdefinierte Formeln in die Firmware einbauen

Sonderfunktionen

* Die Funktion "Gerät zurücksetzen" (sonst nur über die ETS machbar)
* Akustische Signalisierung über einen Buzzer
* Optische Signalisierung mittels einer RGB-LED

Zeitschaltuhren

* Als Jahresschaltuhr mit 4 oder als Tages/Wochenschaltuhr mit 8 Schaltzeiten definiert werden
* Feiertage berücksichtigen (oder ignorieren)
* Urlaub berücksichtigen (oder ignorieren)
* Tag/Monat berücksichtigen (bei Jahresschaltuhren)
* Wochentag/Stunde/Minute berücksichtigen (bei allen Schaltuhren)
* Sonnenstandsbezogene Schaltzeiten:
  * Sonnenauf-/-untergang +/- Stunden/Minuten
  * Sonnenauf-/-untergang, aber frühstens/spätestens um ...
  * Sonnenauf-/-untergang +/- Sonnenwinkel über/unter dem Horizont
* Jede Stunde zu bestimmten Minuten schalten
* Jeder Schaltvorgang kann dann wie bei jedem Logikkanal auch alle Ausgangsfunktionen haben
* Beim Neustart des Logikmoduls den zeitlich letzten Schaltzeitpunkt berechnen und erneut ausgeben

## Applikationsbeschreibung

Die aktuelle Applikationsbeschreibung ist hier zu finden: [Applikationsbeschreibung-Logik](../../OAM-LogicModule/blob/main/doc/Applikationsbeschreibung-Logik.md)
 
## Hardware

### Hardwareplattformen

OpenKNX unterstützt standardmäßig 2 Prozessoren: 

* SAMD - Der erste von OpenKNX unterstützte Prozessor, für viele Anwendungen vollkommen ausreichend. Das Modulkonzept von OpenKNX, bei dem mehrere - normalerweise für sich stehende - Applikationen kombiniert werden können, bringt diesen Prozessor bei vielen Modulen an Grenzen. Dewegen haben die Module bei diesem Prozessor häufig eine geringere Kanalanzahl. 
* RP2040 - Der aktuell von OpenKNX favorisierte Prozessor. Die Ressorucen dieses Prozessors erlauben größere Applikationen und mehr Kanäle. Ferner bietet dieser Prozessor auch die Möglichkeit eines Updates über den Bus. Falls es Installationspakete für SAMD und für RP2040 gibt, sind die für den RP2040 meist mit "Big" oder "Gross" gekennzeichnet. Diese sollten für einen RP2040 bevorzugt verwendet werden.

### Verfügbare Hardware

Die Software läuft auf folgender Hardware "out-of-the-box":

* **Smart-MF Sensormodul** [www.smart-mf.de](https://www.smart-mf.de), als Logikmodul mit der Option, über eine Zwischenplatine einen Buzzer und/oder einen RGB-LED-Signalgeber zu erhalten. Das Sensormodul ist als v3.1 (SAMD) und als v4.0 (RP2040) verfügbar.
* **PiPico-BCU-Connector** [OpenKNX-Wiki](https://github.com/OpenKNX/OpenKNX/wiki/PiPico-BCU-Connector), als Logikmodul auf RP2040.
* **1TE-RP2040-Smart-MF** [www.smart-mf.de](https://www.smart-mf.de), auf allen Varianten als Logikmodul lauffähig (RP2040)
* **OpenKNX-UP1-System** [OpenKNX-Wiki](https://github.com/OpenKNX/OpenKNX/wiki/OpenKNX-UP1), auf allen Varianten als Logikmodul lauffähig (RP2040)

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

Das Logikmodul ist in der Version 1.5.3 verfügbar.

## Releases

Das Logikmodul ist als [LogicModule-Release-1.5.3](../../OAM-LogicModule/releases/tag/1.5.3-release) freigegeben. 

> Empfehlung: Falls das Logikmodul standalone auf einer RP2040-Hardware installiert werden soll, sollte man [gleich zum VPM greifen](Präsenzmodul-‐-Produktinfo). Man erhält exakt die selbe Logik mit gleich vielen Logikkanälen, bekommt aber noch weitere 40 Präsenzkanäle dazu. Falls man die nicht nutzt, ist das kein Nachteil, aber falls man mal was in der Richtung machen will, hat man VPM-Kanäle verfügbar.

## Änderungshistorie

Eine detaillierte Änderungshistorie findet ihr immer am Anfang der [Applikationsbeschreibung-Logik](../../OAM-LogicModule/blob/main/doc/Applikationsbeschreibung-Logik.md#änderungshistorie).

Im Folgenden werden nur größere Änderungen aufgeführt:

### Firmware 1.5.3, Applikation 1.5

* FIX: Der Delta-Input-Converter hat beim Start keinen ReadRequest auf einem Eingang gesendet, wenn auf dem anderen Eingang ein Wert empfangen wurde.
* NEU: TOR hat jetzt einen Tri-State-Eingang zum öffnen vom Tor: Das Tor ist beim Neustart weder offen noch geschlossen und agiert somit beim ersten Telegramm erwartungskonform
* NEU: TOR ist bei Neustart am Ausgang undefiniert und wird mit dem ersten öffnen/schließen erst initialisiert.
* NEU: Mathematische Funktion "Glättung" von Werten eingeführt
* Dieses Release profitiert primär von den Stabilitätsverbesserungen des KNX-Stack

### Firmware 1.4.2, Applikation 1.4

Die letzte zuvor offiziell freigegebene Firmware und ETS-Applikation



