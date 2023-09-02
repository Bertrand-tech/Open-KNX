## Vorstellung

OAM-PresenceModule implementiert einen virtuellen Präsenzmelder (VPM). Es ist eine Präsenzmelder-Applikation, die Präsenz-, Bewegungs- und Helligkeits-Informationen von einem Gerät empfangen kann und anschließend wie ein Präsenzmelder agiert. Dadurch ergeben sich einige Anwendungsbereiche:

* VPM als Ersatz-Applikation für den Steinel True Presence (das war die Initial-Idee für diese Applikation)
* VPM als Applikation für 230V-Bewegungsmelder, die nur über einen Binäreingang am KNX angeschlossen sind (z.B Außenbeleuchtung)
* VPM als eine frische/neue Applikation für existierende ältere PM bzw. BWM, die mit ihrer eigenen Applikation nur die Grundbedürfnisse abdecken können und für die man neuere/modernere Funktionen erhalten möchte, ohne sich neue Hardware kaufen zu müssen
* PM-Applikaiton für unseren OpenKNX-RealPresence (nicht virtuell). Es hat inzwischen eine PM-Hardware-Eigenentwicklung vom OpenKNX-Projekt begonnen, die es auch ernöglicht, Präsenz ohne Bewegung festzustellen

## Übersicht Funktionen

"Klassischer Präsenzmelder" mit

* schalten bei Bewegung
* ausschalten nach einer gewissen Nachlaufzeit
* Helligkeitsgesteuert oder Helligkeitsunabhängig
* 2 Ausgängen pro Kanal mit unterschiedlichen DPT
* Halb- oder Vollautomat
* Durchgangsraum, einschalten erst nach einiger Zeit

Virtueller PM: Verwendbar mit einem oder mehreren (beliebig vielen) Slaves

* VPM ist dann Master für alle Slaves
* Das Präsenz-Signal kann schaltend oder triggernd sein
* Helligkeit kann vom gleichen Slave kommen oder von irgendeinem anderen Helligkeitssensor
* Falls die externe Quelle getrennt Bewegungs- und Präsenzinformationen liefern kann, wird das in dafür geeigneten Funktionen berücksichtigt.

Tagesphasen

* Es wird nicht nur Tag/Nacht, sondern es werden bis zu 4 Tagesphasen unterstützt (Morgens, Tag, Abend, Nacht)
* Tagesphasen können beliebig benannt werden und haben keine vorgegebene Bedeutung
* Jede Tagesphase unterstützt eigene Nachlaufzeiten, Helligkeiten, Kurzzeitpräsenz
* Falls mehr als 4 Tagesphasen benötigt werden, kann man das durch zusammenschalten von Kanälen erreichen

Innovative Adaptive Ausschaltschwelle über Helligkeit

* Erlaubt absolute oder relative Helligkeitsschwellen
* Abschaltung bei externen Lichteinflüssen
* Beachtet mehrere Lichtkanäle pro Raum

Automatik- und Manuell- und Sperrmodus

* Der Moduswechsel ist über Ein- und Zweitastenbedienung vorgesehen
* Der Moduswechsel kann auch über Szenen vorgenommen werden
* Einstellbare Rückfallzeiten für Manuell- oder Sperrmodus

Innovative "Raum verlassen"-Funktion

* Erlaubt dem Melder die Unterscheidung zwischen "Licht aus und im Raum bleiben" und "Licht aus und Raum verlassen".
* Schaltet damit das Licht genau dann erneut ein, wenn man es benötigt

Viele Parameter über GA modifizierbar

* aktuelle Helligkeitsschwelle
* aktuelle Nachlaufzeit
* aktuelle Tagesphase
* Sensibilität des HF-Sensors
* Szenario für HF-Sensor

Erweiterte Steuerungsmöglichkeiten

* alle Melderfunktionen sind über Szenen steuerbar
* Jeder Eingang (frei wählbar) kann bei Busspannungswiederkehr Werte lesen
* KO können auch intern verknüpft werden (Interne KO) und so die Buslast vermindern

Logikmodul mit vielen weiteren Funktionen

* mit dem integrierten Logikmodul können weitere Funktionen in den PM integriert werden
* Interne KO können auch zwischen PM und Logik verwendet werden

## Applikationsbeschreibung

Die aktuelle Applikationsbeschreibung ist hier zu finden: [Applikationsbeschreibung-Präsenz](../../OAM-PresenceModule/blob/main/doc/Applikationbeschreibung-Praesenz.md)
 
## Hardware

Die Software läuft auf folgender Hardware "out-of-the-box":

* **Smart-MF Sensormodul** [www.smart-mf.de](https://www.smart-mf.de), als virtueller Präsenzmelder, um die Applikationen von alten oder unzuverlässigen Präsenzmeldern zu verbessern
* **PiPico-BCU-Connector** [OpenKNX-Wiki](https://github.com/OpenKNX/OpenKNX/wiki/PiPico-BCU-Connector), als virtueller Präsenzmelder
* **1TE-RP2040-Smart-MF** [www.smart-mf.de](https://www.smart-mf.de), als virtueller Präsenzmelder auf allen Varianten lauffähig
* **OpenKNX-UP1-System** [OpenKNX-Wiki](https://github.com/OpenKNX/OpenKNX/wiki/OpenKNX-UP1), als virtueller Präsenzmelder auf allen Varianten lauffähig
* **Smart-MF RealPresence** [www.smart-mf.de](https://www.smart-mf.de), als vollständiger Präsenzmelder, der auch Personen ohne Bewegung zuverlässig erkennt.

## Verwendet

Das Präsenzmodul wird auch in einer Variante des Sensormoduls verwendet, als ein VPM mit 5 Kanälen. 

## Releases

Das Präsenzmodul ist in der [Version 1.11.1](../../OAM-PresenceModule/releases/tag/1.11.1-Release) freigegeben. 

Es gibt 2 Varianten des VPM:

* PresenceModule-Big mit 40 Präsenzkanälen und 99 Logikkanälen, nur für den RP2040 verfügbar.
* PresenceModule-Release mit 20 Präsenzkanälen und 30 Logikkanälen, sowohl für den SAMD wie auch für den RP2040 verfügbar.

## Änderungshistorie

Eine detaillierte Änderungshistorie findet ihr immer am Anfang der [Applikationsbeschreibung-Präsenz](../../OAM-PresenceModule/blob/main/doc/Applikationbeschreibung-Praesenz.md#änderungshistorie).

Im Folgenden werden nur größere Änderungen aufgeführt:

### Firmware 1.11.1, Applikation 1.11

* Die enthaltene Logik hat den Firmware-Stand 1.5.1
* Dieses Release profitiert primär von den Stabilitätsverbesserungen des KNX-Stack

### Firmware 1.7.6, Applikation 1.7

Die letzte zuvor offiziell freigegebene Firmware und ETS-Applikation


