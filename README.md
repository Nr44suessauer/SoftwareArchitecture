# Software Architecture

Manual Use PlantUML

### Diagramme/PlantUML
Diagramme werden mit dem PlantUML Tool erstellt. Dazu werden die letztendlichen Bilder aus einer Quelldatei generiert, welche vorher vom dokumentierenden Entwickler erstellt werden müssen. 

Das Tool lässt sich als [VSCode Erwweiterung](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) (empfohlen), bzw. auch über die [PlantUML Webseite](https://plantuml.com/download) herunterladen und installieren. Auf dieser finden sich auch Informationen dazu, wie sich PlantUML Diagramme schreiben lassen.

#### Voraussetzungen
- Eine installierte und in den **_Umgebungsvariabeln_** hinterlegte **JAVA Runtime Environment**.
- Die [**PlantUML JAR**](https://plantuml.com/download) Datei.

Weitere Informationen zur Installation und Vorraussetzungen der VSCode Erweiterung finden sich [hier](https://github.com/qjebbs/vscode-plantuml/blob/master/README.md)

</br>

---

#### Java Umgebungsvariabeln Windows
Nachdem **JAVA** über deren [Webseite](https://www.java.com/de/download/) heruntergeladen und installiert wurde, müssen die **Path** und **JAVA_HOME** Umgebungsvariablen angelegt bzw. erweitert werden. (Unter Linux sollte dies bei der Installation automatisch passieren.)

Unter Windows gehen sie dazu in die **Systemeinstellungen -> Erweiterte Systemeinstellungen -> Umgebungsvariabeln**.

##### JAVA_HOME
Entweder unter den Nutzer- oder System-Variabeln einen neuen Eintrag mit Namen **JAVA_HOME** anlegen. In diesem wird der Pfad zum Hauptverzeichnis der installierten **Java Runtime Environment** hinterlegt.

Dieser könnte beispielsweise so aussehen:
```
C:\Programme\Java\jre-1.8\
```

##### Path
Die entweder schon existente **Path** Variable per **_bearbeiten_** Feld erweitern, oder falls die Variable noch nicht existiert diese neu anlegen. Diese Variable beinhaltet den Pfad zur ausführbaren Java Datei.

Beispielsweise:
```
C:\Programme\java\jre-1.8\bin\
```
lässt sich alternativ schreiben als:
```
%JAVA_HOME%\bin\
```

</br>

---

#### PlantUML JAR
Um die PlantUML JAR Datei zu verwenden, laden sie diese über deren [Webseite](https://plantuml.com/download) herrunter (Lizens kann frei gewählt werden). Nachdem diese herrunter geladen wurde, speichern sie diese in einem bekannten Ort ihres Dateisystems.

Beispielsweise:
```
C:\Users\Benutzer\JAR-Files\plantuml.jar
```
Dieser Pfad ist wichtig um den **lokalen Renderer** der VSCode Erweiterung für PlantUML nutzen zu können. Oder wird gebraucht wenn mit die JAR Datei PlantUML direkt ausgeführt werden soll.


</br>

---

<!-- ##### GraphVIZ


</br>

--- -->

#### PlantUML VSCode Erweiterungseinstellungen
Wenn PlantUML als VSCode Erweiterung verwendet wird, müssen noch einige Anpassungen in den Erweiterungseinstellungen vorgenommen werden. Klicken sie dazu nachdem die VSCode Erweiterung installiert wurde, unter Erweiterungen -> PlantUML auf das Zahnrad neben dem **_Deinstalieren_** Feld und wählen sie **Erweiterungseinstellungen**.

**Export Einstellungen**</br>
Tragen sie dazu:

unter **Diagrams Root**:
```
docs/diagramms/src
```
</br>

und unter **Export Out Dir**:
```
docs/diagrams/out
```
ein.


Weitere Einstellungen (sollten Standard sein) sind:
- Export Concurrency: **3**
- Export Include Folder Heirarchy: **true**
- Export Sub Folder: **true**

Damit sollten beim exportieren der Diagramme alle nötigen Unterordner und der **out/** Ordner selbst richtig erstellt werden.

**Generierungs Einstellungen**</br>
Um aus den Quelldateien Bilder zu generieren und sich eine Vorschau des Diagramms anzeigen zu lassen, müssen die PlantUML JAR sowie Java hinterlegt und ein Render Modus gewählt werden.

Dazu unter **Jar** den Pfad zu der herunter geladenen **plantuml.jar** Datei angeben.

Beispielsweise:
```
C:\Users\Benutzer\JAR-Files\plantuml.jar
```
##### Wichtig
> Den vollen Datei Pfad inklusive Datei Name und Endung angeben.

Unter **Java** den Pfad zu ihrer **Java Executable**,
```
C:\Programme\java\jre-1.8\bin\java
```
oder bei korrekt hinterlegten Umgebungsvariabeln einfach
```
java
```
angeben.

Abschließend unter:
- **Render** die Option **Local** auswählen.

----

</br>

Abschließend sollte VSCode einmal neugestartet werden um die Veränderungen zu übernehmen.


---

### Diagramme Struktur
Im Unterordner **diagrams/** finden sich die erstellten Diagramme in PlantUML Format. Dazu ist dieser in **src/** und **out/** Ordner unterteilt. 

Der **src/** Ordner ist aufgeteilt in Ordner der entsprechenden Teilprojekte und in diesen befinden sich die Quelldateien der Diagramme, mit **.puml** Dateiendung.

</br>

In einer **.puml** Datei können sich mehrere Diagramme befinden und jede Datei wird beim Exportieren zu einem eigenen Ordner im **out/** Verzeichnis. Dadurch kann eine Datei für mehrere Diagramme eines (Sub-)Systems oder einer Komponente verwendet werden.

Beispielhaft ließe sich für ein **CLI** im **docs/diagrams/src/ufo_python/** Ordner eine Datei mit Namen **CLI.puml** erstellen. Diese kann dann zum einen ein Ablauf Diagramm sowie ein Komponenten Diagramm beinhalten um darzustellen, wie der Ablauf der **CLI** ist und aus welchen Komponenten diese besteht.

Werden die Diagramme dieser Datei nun exportiert, dann finden sich diese (Vorrausgesetzt die oben genannten Einstellungen stimmen) in einem Ordner mit Pfad **docs/diagramms/out/ufo_python/CLI/**. Folglich würde der genannte Ordner nun eine Bilddatei für das Ablauf Diagramm und eine Bilddatei für das Komponenten Diagramm beinhalten.

---

### C4 Diagram

Documentation :```https://github.com/plantuml-stdlib/C4-PlantUML/blob/master/README.md ```

Example:

```
@startuml system_context python client
!include <C4/C4_Container>

Container(pythonApi, "Python API", "Python API used to send commands to proxy")
Container(proxy, "Proxy Node", "nrF Chip links main system with BT-mesh")

Rel(pythonApi, proxy, "send commands", "Serial connection")

Rel(proxy,Mesh,"BT-Mesh")
System_Boundary(Mesh, "Mesh") {

Container(BTnode, "BT Node", "nrF Chip connected with proxy & mesh")
Container(BTnode1, "BT Node", "nrF Chip connected with proxy & mesh")
Container(BTnode2, "BT Node", "nrF Chip connected with proxy & mesh")
}
@enduml
```

### Useage

``` Hotkey: ALT + D ```
