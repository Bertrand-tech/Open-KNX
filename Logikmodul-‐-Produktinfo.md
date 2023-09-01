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

Alle Ein- und Ausgänge können ihre Werte invertieren

Eingänge können aktiv Werte lesen

* beim Startup
* Zyklisch mit einstellbarer Zeit
* Zyklisch bis die erste Antwort kommt

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

* SUM
* Es ist möglich bentzterdefinierte Formeln in die Firmware einbauen

Sonderfunktionen

Die Funktion "Gerät zurücksetzen" (sonst nur über die ETS machbar)
Akustische Signalisierung über einen Buzzer
Optische Signalisierung mittels einer RGB-LED
Zeitschaltuhren
Als Jahresschaltuhr mit 4 oder als Tages/Wochenschaltuhr mit 8 Schaltzeiten definiert werden
Feiertage berücksichtigen (oder ignorieren)
Urlaub berücksichtigen (oder ignorieren)
Tag/Monat berücksichtigen (bei Jahresschaltuhren)
Wochentag/Stunde/Minute berücksichtigen (bei allen Schaltuhren)
Sonnenstandsbezogene Schaltzeiten:
Sonnenauf-/-untergang +/- Stunden/Minuten
Sonnenauf-/-untergang, aber frühstens/spätestens um ...
Jede Stunde zu bestimmten Minuten schalten
Jeder Schaltvorgang kann dann wie bei jedem Logikkanal auch alle Ausgangsfunktionen haben
Beim Neustart des Logikmoduls den zeitlich letzten Schaltzeitpunkt berechnen und erneut ausgeben


## Applikationsbeschreibung

## Hardware

## Verwendet

## Varianten





