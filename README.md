# ESP32Focuser Hardware

This is a repository for storing documentation for my [ESP32Focuser](https://github.com/semenmiroshnichenko/ESP32Focuser) project.

# What is that about
Focuser for astronomy telescope based on ESP32 controller. Comportable with Indilib (http://indilib.org/) and ASCOM (https://ascom-standards.org/).
The controller uses the protocol Moonlite (as documented in the indilib project).

# What hardware do I need
The firmware runs on a [ESP32-DevKitC](https://www.espressif.com/en/products/devkits/esp32-devkitc/overview) board. It uses also the [BIGTREETECH TMC2209 V1.2 Stepper Motor Driver](https://github.com/bigtreetech/BIGTREETECH-TMC2209-V1.2) to drive the motor on a super-silent and vibrationless way. Basically, you only need this two boards to start using the focuser. If you want to build it on a more resilient way, you can follow intructions below.

# Schematics
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
I use the 17HS2408 stepper motor, as it fits well for 12v supply: it has 8 Ohm phase resistance what leads to 1.5 Amps phase current, it's a bit over the specification (rated current 0.6 Amps) but as it's not supposed to continuously work on high speed in this project ,it works just fine, has enough torque and does smooth movements. 

## KiCad project
Schematics diagram can be found in the KiCad project [folder](/schematics) 

# Pictures

![board1.jpg](/pictures/board1.jpg)
![board2.jpg](/pictures/board2.jpg)
![handcontroller.jpg](/pictures/handcontroller.jpg)
![assembled.jpg](/pictures/assembled.jpg)