work-in-progress

## Hintergrund

OpenKNX bietet ein Modulkonzept, dass es erlaubt, fertige Teilapplikationen (OpenKNX Function Modules, kurz OFM) in andere Applikationen zu integrieren und somit auf einfache Weise einen Mehrwert zu generieren.

Derzeit gibt es bereits Module, die einfach in andere Applikationen integrierbar sind:

* OFM-LogicModule - universelle Logik
* OFM-PresenceModule - virtueller Präsenzmelder
* OFM-Updater - erlaubt Applikationsupdate über den KNX-Bus
* OFM-VirtualButton - virtueller Taster
* OFM-BinaryInput - generischer Binäreingang

Die Liste ist nicht vollständig und es werden immer wieder Module ergänzt. Alle OFM haben die Gemeinsamkeit, dass sie nicht nur Implementierungen (Coding) ihrer Funktionalität bieten, sondern auch die entsprechende Parametrisierungsoberfläche für die ETS-Applikation.

Wird ein (oder mehrere) OFM von einer OpenKNX-Applikation (OAM - OpenKNX Application Module) verwendet, muss diese nicht nur dafür sorgen, dass entsprechendes Coding des OFM zur Prozessierung der Funktionalität aufgerufen werden muss, sondern dass auch in der ETS-Applikation des OAM die passende Parametrisierungsoberfläche zur Verfügung gestellt wird. 

Da ETS-Applikationen selbst kein Modularisierungskonzept bieten - es gibt nur genau ein großes XML, dass alle Daten enthalten muss - wird das Zusammenbauen der Applikation aus mehreren Teilen von einem Werkzeug unterstützt (OpenKNXproducer). 

Das OpenKNX-Toolset erlaubt dadurch auf einfach Weise das zusammenbauen von Firmware (per include von Coding) und das zusammenbauen von Applikationen (per include von Applikations-XML). Dieser Prozess erlaubt auch auf einfache Weise ein Update einer Applikation+Firmware, wenn sich eines der beteiligten Module geändert haben sollte.

## Problembeschreibung

Derzeit werden alle OFM einfach per include referenziert, ohne dass es eine Versionsprüfung gibt. Als das Team noch klein war und es kaum Module gab, war es einfach, alles in Sync zu halten und alle OFM-Nutzer zu informieren, dass sich was geändert hat. 

Im Folgenden wird eine Versionierung von OFM beschrieben, die es erlaubt, bereits zur Compilezeit (Firmware) bzw. durch den OpenKNXproducer (Applikation) darüber informiert zu werden, dass sich abhängige Teile geändert haben.

## Versionierung eines OFM 

Ein OFM muss für die Versionierung in src eine Datei zur Verfügung stellen, die eine Version des OFM enthält und das Coding bereitstellt, um die Überprüfung beim Bauen der Firmware zu realisieren. 

### Die Versionsdatei

Die Namenskonvention für den Dateinamen ist ModuleVersion.h. Das OFM-VirtualButton würde somit die Datei

    src/ModuleVersion.h

enthalten. 

Der Inhalt der Datei ist:

    // change this, if OFM changed its ETS-Application the way it influences the Application of an OAM
    #define ModuleVersion 25 

    // Optional: change this if just coding is changed (bugfix in C++)
    #define ModuleRevision 3 

    // ATTENTION: This file is evaluated during build, by OpenKNXproducer and some build scripts.
    // Do not add any other information than the module version/revision of this OFM.
    #define VALUE_TO_STRING(x) #x
    #define VALUE(x) VALUE_TO_STRING(x)

    #if BTN_ModuleVersion != ModuleVersion
    #pragma message "\n\n\nYou need to >>> INCREASE YOUR <<< ETS ApplicationVersion and manually synchronize op:verify of the LOG Module to ModuleVersion " VALUE(ModuleVersion) "\n\n( see https://github.com/OpenKNX/OpenKNX/wiki/Versionierung-von-Modulen-(OFM)#fehler-vom-compiler )\n\n\n"
        #pragma GCC error "\n\nETS Application Version problem (see next message)\n\n"
    #endif

Dabei ist das #define ModuleVersion notwendig, die ModuleRevision ist optional (zu Dokumentationszwecken über reine Coding-Änderungen).

Der Wertebereich für ModuleVersion ist der selbe wie der für ETS-Applikationen, XML-Tag "ApplicationVersion": 0-255. Der Wert sollte nur erhöht werden, wenn man im OFM an der Applikation etwas geändert hat, dass Auswirkungen auf die Nutzer (OAM) dieses OFM haben, da bei 255 Schluss ist! Man sollte auch immer bedenken, das eine Änderung dieses Wertes für alle nutzenden OAM eine Anpassung der eigenen Applikationsversion erfordert. Bitte also umsichtig mit Änderungen umgehen.

Die ModuleRevision hat den Wertebereich von 0-31, angelehnt an den Revisions-Wertebereich in der ETS.

Das Coding nach "ATTENTION" sorgt nur für eine halbwegs menschenwürdige Fehlermeldung beim Build und einem Buid-Abbruch und muss nicht angepasst werden. 

### Die Nutzung der Versionsdatei im OFM

Jedes OFM hat eine Klasse, die die Funktionalität des OFM repräsentiert, meist in einer Datei mit der Namenskonvention ***Modulname***Module.cpp (Hauptdatei). Im OFM-VirtualButton wäre das somit

    src/VirtualButtonModule.cpp

In dieser Datei muss die Versionsdatei per #include eingefügt werden. Wichtig ist dass das Include nach dem Include für OpenKNX.h ist, also:

    #include "OpenKNX.h"

    #inlcude "ModuleVersion.h"

(Die Leerzeile ist auch wichtig, sie verhindert, dass die Includereihenfolge beim Speichern automatisch umsortiert wird).

### Zusätzliche Nutzung der Version (optional)

Da die Versionsdatei sowieso schon in der Hauptdatei referenziert wird, und die dort implementierte Klasse von OpenKNX::Module ableitet, kann diese Klasse eine Version implementieren

    const std::string version() override;

Per default bekommt man als Version die library-Version und den git-hash, wenn man aber ModuleVersion und ModuleRevision zurückgibt, bekommt man eine semantische Version (diese wird auf der Console zur Laufzeit ausgegeben):

    const std::string VirtualButtonModule::version()
    {
        // do not use any string functions, especially strigstream, it uses 120k Flash
        char lVersion[9];
        // example implementation using ModuleVersion and ModuleRevision will be provided
        return lVersion; // would be "1.9.3" for ModuleVersion 25 and Revision 3
    }

## Nutzung der Version des OFM im einem OAM

Ein OAM baut die ETS-Applikation aus den einzelnen OFM zusammen. Die ETS-Applikation muss immer eine neuere Version bekommen, wenn sich etwas an dieser Applikation ändert. Somit hat jede Änderung einer OFM-Applikation (Teilapplikation) direkt eine neue Version der OAM-Applikation zufolge. Mit der Versionierung wird das sichergestellt.


Um die Versionierung auf OAM Ebene zu aktivieren, muss in der XML-Hauptdatei (das ist die, die das op:define-Tag enthält, dass das OFM definiert), das op:define-Tag erweitert werden. Aus

    <op:define prefix="BTN" header="VirtualButtonModuleKnxprod.h" NumChannels="10" KoOffset="400" ModuleType="2" />

wird

    <op:define prefix="BTN" header="VirtualButtonModuleKnxprod.h" NumChannels="10" KoOffset="400" ModuleType="2">
        <op:verify File="../lib/OFM-VirtualButton/src/ModuleVersion.h" ModuleVersion="25" />
    </op:define>

Dabei bedeuten

* op:verify - neuer Tag, der OpenKNXproducer anweist, die Version eines benutzten OFM zu prüfen
* File - Dateiname der .h-Datei, die das **#define ModuleVersion** enthält. Der Pfad sollte immer relativ formuliert werden.
* Version - (optional) - Enthält die Version, mit der die OAM-Applikation das letzte mal compiliert wurde. Für den Fall, dass die Version in der .h-Datei und die hier angegebene nicht gleich sind, meldet der OpenKNXproducer einen Fehler. 
Für den Fall, dass die Version nicht angegeben wurde, wird immer die aktuellste Version angenommen und es gibt keine Fehlermeldung, sondern eine Warnung. Das ist ein Modus, der während der Entwicklung helfen kann, wenn man intensiv am UI arbeitet, an vielen Stellen ändert und nicht immer von Versionierungsfehlern tangiert werden will. **Das sollte man im produktiven Betrieb nicht nutzen**

* Regex - (optional) Falls in der .h-Datei die Version nicht über eine Variable **ModuleVersion** sondern über ein anderes Konstrukt definiert wird, kann hier ein Regex stehen, dass dieses Konstrukt findet. Der Default für Regex ist 
  
        #define\s*ModuleVersion\s*(\d{1,3})"

> **WICHTIG:** Diese Funktionalität steht erst ab der Version 2.3.5 des OpenKNXproducer zur Verfügung.
### Zusammenfassung

Mit dem Einbinden eines passenden ModuleVersion.h Files auf der OFM-Seite und der Erweiterung des **op:define**-Tags mit **op:verify** auf der OAM-Seite wird die Infrastruktur so erweitert, dass sowohl beim Bauen der Firmware (compilieren) wie auch beim Bauen der ETS-Applikation (OpenKNXproducer) Versionsunstimmigkeiten erkannt werden, die sonst zur Laufzeit zu unerwarteten Auswirkungen führen können.

## Vorgehen bei einer aus der Versionsprüfung resultierenden Fehlermeldung

Wenn man die Versionsprüfung nutzt, gibt es Fehler beim Compilieren oder vom OpenKNXproducer, falls Versionen nicht übereinstimmen.

### Fehler vom Compiler

Der Compiler meldet

        ETS Application Version problem (see next message)

        You need to >>> INCREASE YOUR <<< ETS ApplicationVersion and manually 
        synchronize op:verify to ModuleVersion 25

        ( see https://github.com/OpenKNX/OpenKNX/wiki/Versionierung-von-Modulen-(OFM)#fehler-vom-compiler )

### Fehler vom OpenKNXproducer

Der OpenKNXproducer meldet

    You need to >>> INCREASE YOUR <<< ETS ApplicationVersion and manually synchronize op:verify of the BTN Module to ModuleVersion 25

### Notwendige Aktivitäten bei einem Versionsfehler

1. im OAM-Haupt-XML die Applikationsversion des OAM zwingend erhöhen, damit in der ETS eine neue Version geladen werden muss.
2. im OAM-Haupt-XML die ModuleVersion im op:verify-Tag auf die Version setzen, die in der Meldung angegeben wurde (im Beispiel 25)
3. Mit dem OpenKNXproducer eine neue ETS-Applikation bauen und anschließend das Projekt neu compilieren.

> **WICHTIG: Immer wenn im op:verify-Tag die ModuleVersion angepasst wird, muss gleichzeitig auch die ApplicationVersion der Applikation erhöht werden.**
## Wie funktioniert das Ganze?

Im Prinzip realisieren die obigen Ergänzungen eine 3-Punkte-Prüfung. 


Wenn der OpenKNXproducer innerhalb eines op:define einen op:verify-Tag findet, liest er zuerst das angegebene File und holt sich daraus anhand des angegebenen Regex die ModuleVersion raus. In dem knxprod.h-File, dass der OpenKNXproducer für die Firmware generiert, wird ein Eintrag "#define ***Modulpräfix***_ModuleVersion ***gelesene Version***" generiert, in unserem Beispiel

    #define BTN_ModuleVersion 25

Das ist letztendlich genau das, was in dem ModuleVersion.h-File steht, nur ergänzt durch den Modulpräfix. Durch dieses Define kann beim Compilieren der Firmware die in dem ModuleVersion.h-File enthaltene Prüfung funktionieren:

    #if BTN_ModuleVersion != ModuleVersion

Hat sich an *ModuleVersion* was geändert, ohne dass der OpenKNXproducer gelaufen ist, ist in der knxprod.h noch ein *BTN_ModuleVersion* mit einem alten Wert enthalten und das Compilieren schlägt fehl. 

Somit muss man erst einmal den OpenKNXproducer laufen lassen, der dann einen neuen *BTN_ModuleVersion*-Eintrag generiert, der aber auch noch die neuste knxprod.h generiert und eine neue ETS-Applikation mit dem aktuellsten Stand baut.

Nachdem der OpenKNXproducer das .h-File gelesen hat, vergleicht er den Wert auch mit dem Wert von ModuleVersion, der in dem op:verify-Tag angegeben ist. Wenn die Versionen unterschiedlich sind, bedeutet das (indirekter Schluss), dass die Applikationsversion des OAM nicht korrekt ist (weil sich ja das darunterliegende OFM geändert hat).

Bei einem Unterschied muss man manuell die Version anpassen, wobei man dabei auch immer die Applikationsversion des OAM erhöhen muss. Das ist auch der Grund, warum dieser Schritt manuell zu erfolgen hat.

