# ESP32Focuser-Hardware
Dies ist ein Repository zum Speichern der Dokumentation für mein Projekt [ESP32Focuser](https://github.com/semenmiroshnichenko/ESP32Focuser).

# Worum geht es?
Fokussierer für Teleskop basierend auf ESP32-Controller. Kompatibel mit Indilib (http://indilib.org/) und ASCOM (https://ascom-standards.org/).
Der Controller verwendet das Protokoll Moonlite (wie im Indilib-Projekt dokumentiert).

# Welche Hardware brauche ich?
Die Firmware läuft auf einer [ESP32-DevKitC](https://www.espressif.com/de/products/devkits/esp32-devkitc/overview) Leiterplatte. Es verwendet auch den [BIGTREETECH TMC2209 V1.2 Schrittmotortreiber](https://github.com/bigtreetech/BIGTREETECH-TMC2209-V1.2), um den Motor super leisen und vibrationsfrei anzutreiben. Grundsätzlich benötigen Sie nur diese beiden Leiterplatten, um den Fokussierer zu bauen. Wenn Sie es auf eine stabilere Art und Weise bauen möchten, können Sie den folgenden Anweisungen folgen.

# Schaltplan
Das Schaltplandiagramm befindet sich als KiCad-Projekt [Ordner](/schematics). Sie können den Schaltplan als pdf [hier](/schematics/ESP32Focuser.sch.pdf) herunterladen.

Das Schema ist ziemlich einfach. Sie verbinden einfach die Pins der ESP32-Entwicklungskarte mit der TMC2209-Karte, fügen ein Netzteil hinzu und schließen den Motor an - von diesem Punkt aus können Sie den Fokussierer vom Computer über den ASCOM / INDI-Treiber steuern. Wenn Sie einen optischen Encoder als Handcontroller verwenden möchten (was ich Ihnen wirklich empfehlen würde, wenn Sie Vibrationen beim Berühren des Teleskop-Fokussierknopfs beseitigen möchten), schließen Sie ihn ebenfalls an die Stifte auf der ESP32-Platine an.

## Verdrahtungstabelle
Bitte verwenden Sie die Verkabelungstabelle als Referenz, da diese möglicherweise veraltet ist. Die neueste Schaltplanversion finden Sie im KiCad-Projekt.

| Description | ESP32 board | TMC2209 board | Note |
| ----------- | ----------- | ------------- | ---- | 
| DIR         | 32          | DIR           |      |
| STEP        | 33          | STEP          |      |
| CLK         | 25          | CLK           |      |
| PDN         | 26          | PDN + PDN     | not used |
| MS2         | 14          | MS2           |      |
| MS1         | 12          | MS1           |      |
| EN          | 13          | EN            |      |
| ENC1        | 2           |               | Encoder output 1 |
| ENC2        | 15          |               | Encoder output 2 |
| 5V          | 5V          | VDD           |      |
| 12V         |             | VM            | Motor power supply |

## Schrittmotor
Ich verwende den Schrittmotor 17HS2408, da er gut für die 12-V-Versorgung geeignet ist: er hat einen Phasenwiderstand von 8 Ohm, was zu einem Phasenstrom von 1,5 Ampere führt. Er liegt etwas über der Spezifikation (Nennstrom 0,6 Ampere), soll aber nicht kontinuierlich auf eine hohe Geschwindigkeit laufen, es funktioniert gut, hat genug Drehmoment und macht sanfte Bewegungen.

## Stückliste
|     Description           |                   AliExpress link                    |  Notes          |
| ------------------------- | ---------------------------------------------------- | --------------- | 
| ESP32-DevKitC             | https://www.aliexpress.com/item/4000103411061.html   | ![](/pictures/parts/esp32-devkitc.png) |
| 17HS2408 stepper motor    | https://www.aliexpress.com/item/33033986185.html     | ![](/pictures/parts/17HS2408.png) |
| 7 M3 screws for motor and encoder  | https://www.aliexpress.com/item/32965979997.html     | M3 50pcs + 5mm  |
| TMC2209 board             | https://www.aliexpress.com/item/33029587820.html     | ![](/pictures/parts/TMC2209.jpg) |
| Optical rotary encoder CALT ES38    | https://www.aliexpress.com/item/33028641351.html | 5v 600ppr ![](/pictures/parts/encoder.png) |
| 13x32mm Encoder knob | https://www.aliexpress.com/item/33039964137.html |![](/pictures/parts/encoder-knob.png) |
| Motor shaft coupler 5mm x ?? mm| https://www.aliexpress.com/item/32913158582.html |![](/pictures/parts/shaft-coupler.png)|
| OR alternatively to the direct coupling your motor with the focuser, you could use a belt like this below|||
| GT2 Pulley 20 tooth ø 5mm| https://www.aliexpress.com/item/32724156349.html |![](/pictures/parts/pulley-20-tooth.png)|
| GT2 Closed Loop Timing Belt | https://www.aliexpress.com/item/32950422029.html |![](/pictures/parts/belt.png)|
| 12v female plug 5.5mm x 2.1mm | | ![](/pictures/parts/12v-connector.png) |
| 12v→5v DC-DC step down converter board| https://www.aliexpress.com/item/32742116421.html |![](/pictures/parts/12v-to-5v-step-down-converter.png)|
| Hand controller connector M GX12 5 pin for encoder | https://www.aliexpress.com/item/32869491577.html |![](/pictures/parts/gx12-connector.png) |
| Hand controller connector M GX12 4 pin for motor | https://www.aliexpress.com/item/32869491577.html |![](/pictures/parts/gx12-connector.png) |
| 115 90 55mm plastic enclosure case | https://www.aliexpress.com/item/32709832386.html | ![](/pictures/parts/box1.png) |
| 100x68x50mm plastic enclosure case for encoder | https://www.aliexpress.com/item/32792270384.html |![](/pictures/parts/box2.png) |
| Push button for handcontroller | https://www.aliexpress.com/item/32965284265.html |![](/pictures/parts/push-button.png)|
| Micro USB cable | tbd | |
| 2.54mm Wire Cable Connector 4 pin | https://www.aliexpress.com/item/32954418743.html | ![](/pictures/parts/2.54mm-wire-cable-connector.png)|
| Prototyping board 5x7 cm | https://www.aliexpress.com/item/32853911495.html | ![](/pictures/parts/5x7-board.png) |
| Cable for motor 4 cores 0.3mm 22awg | https://www.aliexpress.com/item/4000714461664.html |![](/pictures/parts/motor-cable.png) |


# Bilder

![board1.jpg](/pictures/board1.jpg)
![board2.jpg](/pictures/board2.jpg)
![handcontroller.jpg](/pictures/handcontroller.jpg)
![assembled.jpg](/pictures/assembled.jpg)
![assembled2.jpg](/pictures/assembled2.jpg)
![assembled3.jpg](/pictures/assembled3.jpg)
![assembled4.jpg](/pictures/assembled4.jpg)