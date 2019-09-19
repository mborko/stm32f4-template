# Schritt für Schritt Anleitung für das STM32F4-Template

## Einleitung

In diesem Dokument werden alle Schritte beschrieben, die notwendig sind um das [STM32F4Discovery board](https://www.st.com/en/evaluation-tools/stm32f4discovery.html#sw-tools-scroll) mittels des Templates, welches sich auf [GitHub](https://github.com/mborko/stm32f4-template) befindet, arbeiten zu können. 

Diese Anleitung beschränkt sich auf eine Linux-Distribution (in unserem Fall [Ubuntu](https://ubuntu.com/)), daher wird ersucht mit Linux oder einer virtuellen Instanz von Linux zu arbeiten.

#### Alternativen

Falls man jedoch dies nicht will kann man natürlich auch die [STM Workbench](https://www.st.com/en/evaluation-tools/stm32f4discovery.html#sw-tools-scroll) als Alternative benutzen. 

## "Tutorial"

### Schritt 1: Das Repository klonen

Bei diesem Schritt wird empfohlen sich ein eigenes Verzeichnis mittels `mkdir` zu erstellen. Dies sorgt für eine bessere Übersicht.

Um die Repository zu klonen muss man den Befehl `git clone https://github.com/mborko/stm32f4-template` in die Konsole eingeben.

![alt text](https://i.gyazo.com/6a8e503540638f0e0a0c45e4f69d3085.png "Konsolenbefehle für den ersten Schritt")

### Schritt 2: Alle erforderlichen Pakete herunterladen

Um alle notwenigen Pakete herunterzuladen kann man dies einfach mit dem Befehl `
apt install cmake libusb-dev libusb-1.0.0-dev build-essential autoconf\
     cutecom git binutils-arm-none-eabi gcc-arm-none-eabi
`

### Schritt 3: STM32CubeF4 Library installieren

#### Schritt 3.1 ~/opt-Directory erstellen

Für den nächsten Schritt braucht man das *~/opt*-Verzeichnis, dieses muss mittels `mkdir` erstellt werden.
#### Schritt 3.2
Danach muss man das ZIP-Archiv von der Website [herunterladen](https://www.st.com/en/embedded-software/stm32cubef4.html#). 

![alt text](https://i.gyazo.com/1e8f3ba671040f60ab8f4cee1446c989.png "Der Download")

Beim Download wird man aufgefordert Benutzerdaten einzugeben, hier reicht es nur seine eigene Email Adresse einzugeben. Den Downloadlink erhält man mit einer Email.

![img](https://i.gyazo.com/6d3343f34a63589a9976e51b6ec71aa8.png "Die Aufforderung seine Daten einzugeben")

Man extrahiert nun den STM32CubeF4-Ordner in *~/opt*.

![Extrahieren](https://i.imgur.com/bW57UEX.gif)

Der letzte Teil dieses Schrittes ist den Owner des Verzeichnisses zu ändern. Der Command dafür ist `chown -R username filename`

![img](https://i.gyazo.com/b62af3522361138ea991102377fb3a16.png)

### Schritt 4: Flash-Tool installieren

Das letzte Tool was man braucht ist das Flash-Tool. Hierfür muss man nur eine Abfolge von Befehlen in die Konsole eingeben. Da man hier wieder ein Repository herunterlädt empfehle ich wieder ins Repository-Verzeichnis zu gehen.

Folgende Befehle sind notwendig.

```
  git clone https://github.com/texane/stlink  
    cd stlink  
    make clean  
    make package  
    sudo dpkg -i build/Release/stlink-*-amd64.deb  
    sudo ldconfig # refresh library list for st-link  
```

### Schritt 5: Makefile verändern

Damit es zu keinen Komplikationen kommt muss man noch das Makefile, welches sich im STM32F4-Template befindet, verändern. Einfach das Makefile öffnen und die Version anpassen. Im Makefile steht, dass wir die Version 21.0 haben: dies muss auf 24.0 umgeschrieben werden.

![Veränderung am Makefile](https://i.imgur.com/TrIyqRw.gif)

### Schritt 6: Testen

Um zu testen ob alles funktioniert hat kann man den Befehl `make` ausführen. Der Output bei erster Ausführung sollte ungefähr so aussehen.

![Output](https://i.gyazo.com/30fb943113c6e4506b1f288ef14d2f36.png)



## Makefile Parameter

* `clean`: Die vorige Kompilierung wird entfernt?
* `flash`: Das Kompilierte wird auf den Mikrocontroller geflasht.
* `PROJ=`: Pfad zum Projekt, der kompiliert werden soll (vzw. im *src* Ordner innerhalb der Template Repository)

## Quellen

* https://github.com/mborko/stm32f4-template

* https://github.com/texane/stlink
* https://www.st.com/en/embedded-software/stm32cubef4.html#













