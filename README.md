# Software Architecture

Manual Use PlantUML

### Diagrams/PlantUML

Diagrams are created using the PlantUML tool. The final images are generated from a source file, which must be created beforehand by the documenting developer.

The tool can be downloaded and installed as a [VSCode Extension](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) (recommended) or via the [PlantUML Website](https://plantuml.com/download). On this website, you will also find information on how to write PlantUML diagrams.

#### Prerequisites

- An installed **JAVA Runtime Environment** listed in the **_environment variables_**.
- The [**PlantUML JAR**](https://plantuml.com/download) file.

For further information on the installation and prerequisites of the VSCode extension, click [here](https://github.com/qjebbs/vscode-plantuml/blob/master/README.md).

</br>

---

#### Java Environment Variables Windows

After **JAVA** has been downloaded and installed from their [website](https://www.java.com/de/download/), the **Path** and **JAVA_HOME** environment variables need to be created or expanded. (On Linux, this should happen automatically during installation.)

On Windows, go to **System Properties -> Advanced System Settings -> Environment Variables**.

##### JAVA_HOME

Create a new entry named **JAVA_HOME** under either user or system variables. In this, the path to the main directory of the installed **Java Runtime Environment** is stored.

For instance, it might look like this:

```
C:\Programme\Java\jre-1.8\
```


##### Path

Either expand the already existing **Path** variable using the **_edit_** field or create it anew if the variable does not exist yet. This variable contains the path to the executable Java file.

For example:

```
C:\Program files\java\jre-1.8\bin\
```
can alternatively be written as:

```
%JAVA_HOME%\bin\
```

</br>

---

#### PlantUML JAR

To use the PlantUML JAR file, download it from their [website](https://plantuml.com/download) (the license can be chosen freely). After downloading, save it in a known location on your file system.

For example:

```
C:\Users\USER\JAR-Files\plantuml.jar
```
This path is important for using the **local renderer** of the VSCode extension for PlantUML. It is also needed if you want to run PlantUML directly using the JAR file.



</br>

---

<!-- ##### GraphVIZ


</br>

--- -->

#### PlantUML VSCode Extension Settings

When using PlantUML as a VSCode extension, some adjustments need to be made in the extension settings. After the VSCode extension has been installed, click on Extensions -> PlantUML on the gear icon next to the **_Uninstall_** field and select **Extension Settings**.

**Export Settings**<br/>
Please enter:

under **Diagrams Root**:

```
docs/diagramms/src
```
</br>


and under **Export Out Dir**:

```
docs/diagrams/out
```

Additional settings (which should be default) include:
- Export Concurrency: **3**
- Export Include Folder Hierarchy: **true**
- Export Sub Folder: **true**

This should ensure that all necessary subfolders and the **out/** folder itself are correctly created when exporting the diagrams.

**Generation Settings**<br/>
To generate images from the source files and to display a preview of the diagram, the PlantUML JAR and Java must be specified and a render mode selected.

To do this, under **Jar**, specify the path to the downloaded **plantuml.jar** file.

For example:

```
C:\Users\USER\JAR-Files\plantuml.jar
```
##### Important
> Specify the full file path, including file name and extension.

Under **Java**, provide the path to your **Java Executable**,

```
C:\Program files\java\jre-1.8\bin\java
```
or, if environment variables are set correctly, simply

```
java
```

Lastly, under:
- **Render**, select the **Local** option.

----

Finally, VSCode should be restarted once to apply the changes.

----

</br>

Finally, VSCode should be restarted once to apply the changes.


---

### Diagram Structure
In the subfolder **diagrams/**, you'll find the created diagrams in PlantUML format. This is further divided into **src/** and **out/** folders.

The **src/** folder is divided into folders for the respective subprojects and contains the source files of the diagrams, with a **.puml** file extension.

<br/>

In a **.puml** file, several diagrams can be present, and each file is exported to its own folder in the **out/** directory upon export. This allows a file to be used for several diagrams of a (sub-)system or a component.

For example, a file named **CLI.puml** could be created for a **CLI** in the **docs/diagrams/src/ufo_python/** folder. This file could contain both a flow diagram and a component diagram to illustrate the flow of the **CLI** and its constituent components.

When the diagrams from this file are now exported, assuming the settings mentioned above are correct, they can be found in a folder with the path **docs/diagrams/out/ufo_python/CLI/**. Consequently, the specified folder would contain an image file for the flow diagram and an image file for the component diagram.


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
