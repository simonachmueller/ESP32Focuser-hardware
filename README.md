# ESP32Focuser Hardware
This is a repository for storing documentation for my [ESP32Focuser](https://github.com/semenmiroshnichenko/ESP32Focuser) project.

Описание ![на русском](/README.RU.md)

# What is that about
Focuser for astronomy telescope based on ESP32 controller. Comportable with Indilib (http:/indilib.org/) and ASCOM (https://ascom-standards.org/).
The controller uses the protocol Moonlite (as documented in the indilib project).

# What hardware do I need
The firmware runs on a [ESP32-DevKitC](https://www.espressif.com/en/products/devkits/esp32-devkitc/overview) board. It uses also the [BIGTREETECH TMC2209 V1.2 Stepper Motor Driver](https://github.com/bigtreetech/BIGTREETECH-TMC2209-V1.2) to drive the motor on a super-silent and vibrationless way. Basically, you only need this two boards to start using the focuser. If you want to build it on a more resilient way, you can follow intructions below.

# Schematics
Schematics diagram can be found as a KiCad project [folder](/schematics). You can donwload shematics as pdf [here](/schematics/ESP32Focuser.sch.pdf).

The schematics is pretty easy. You just connect the pins of the ESP32 dev board with the TMC2209 board, add power supply and connect motor - from this point you can control the focuser from the computer over ASCOM/INDI driver. If you want to use an optical encoder as a handcontroller (what I would really advise you if you want to get rid of vibrations when you touch the telescope focuser knob), connect it to the pins on the ESP32 board as well.

## Wiring table
Please use the wiring table as reference, it might get outdated. For the most latest schematics version, check the KiCad project.

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

## Stepper motor
I use the 17HS2408 stepper motor, as it fits well for 12v supply: it has 8 Ohm phase resistance what leads to 1.5 Amps phase current, it's a bit over the specification (rated current 0.6 Amps) but as it's not supposed to continuously work on high speed in this project,it works just fine, has enough torque and does smooth movements. 

## BOM
Aka bill of material

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


# Pictures

![board1.jpg](/pictures/board1.jpg)
![board2.jpg](/pictures/board2.jpg)
![handcontroller.jpg](/pictures/handcontroller.jpg)
![assembled.jpg](/pictures/assembled.jpg)
![assembled2.jpg](/pictures/assembled2.jpg)
![assembled3.jpg](/pictures/assembled3.jpg)
![assembled4.jpg](/pictures/assembled4.jpg)