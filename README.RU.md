# ESP32Focuser Оборудование

Это репозиторий для хранения документации для моего проекта [ESP32Focuser](https://github.com/semenmiroshnichenko/ESP32Focuser).

# О чем это вообще
Электрофокусёр для телескопа на базе контроллера ESP32. Совместимость с Indilib (http://indilib.org/) и ASCOM (https://ascom-standards.org/).
Контроллер использует протокол Moonlite (как описано в проекте Indilib).

# Какое оборудование мне нужно
Фокусер работает на плате [ESP32-DevKitC](https://www.espressif.com/en/products/devkits/esp32-devkitc/overview). Он также использует [Драйвер шагового двигателя BIGTREETECH TMC2209 V1.2](https://github.com/bigtreetech/BIGTREETECH-TMC2209-V1.2) для бесшумного и безвибрационного управления двигателем. По сути, вам понадобятся только эти две платы, чтобы начать использовать фокусер. Если вы хотите спаять надёжнее, следуйте инструкциям ниже.

# Схема
Схему в формате проекта KiCad сожно найти [тут](/schematics). Вы можете загрузить схему в формате pdf [здесь](/schematics/ESP32Focuser.sch.pdf).

Схема довольно проста. Вы просто соединяете контакты платы разработчика ESP32 с платой TMC2209, добавляете источник питания и подключаете двигатель - с этого момента вы можете управлять фокусером с компьютера через драйвер ASCOM / INDI. Если вы хотите использовать оптический кодировщик в качестве ручного контроллера (что я бы действительно посоветовал вам, если вы хотите избавиться от вибраций при прикосновении к ручке фокусера телескопа), также подключите его к контактам на плате ESP32.

## Таблица подключения
Пожалуйста, используйте таблицу соединений в качестве справочной информации, она может устареть. Самую последнюю версию схемы смотрите в проекте KiCad.

| Описание | Плата ESP32 | Плата TMC2209 | Примечание |
| ----------- | ----------- | ------------- | ---- | 
| DIR         | 32          | DIR           |      |
| STEP        | 33          | STEP          |      |
| CLK         | 25          | CLK           | не используется |
| PDN         | 26          | PDN + PDN     | не используется |
| MS2         | 14          | MS2           |      |
| MS1         | 12          | MS1           |      |
| EN          | 13          | EN            |      |
| ENC1        | 2           |               | Выход энкодера 1 |
| ENC2        | 15          |               | Выход энкодера 12 |
| 5V          | 5V          | VDD           |      |
| 12V         |             | VM            | Электропитание двигателя |

## Шаговый двигатель
Я использую шаговый двигатель 17HS2408, так как он хорошо подходит для питания 12 В: он имеет сопротивление 8 Ом, что приводит к току 1,5 А, это немного превышает спецификацию (номинальный ток 0,6 А), но поскольку он не должен работать постоянно на высоких скоростях, он отлично работает, имеет достаточный крутящий момент и делает плавные движения.

## BOM
Необходимые материалы (может вариироваться в зависимости от исполнения)

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


# Фотографии
![board1.jpg](/pictures/board1.jpg)
![board2.jpg](/pictures/board2.jpg)
![handcontroller.jpg](/pictures/handcontroller.jpg)
![assembled.jpg](/pictures/assembled.jpg)
![assembled2.jpg](/pictures/assembled2.jpg)
![assembled3.jpg](/pictures/assembled3.jpg)
![assembled4.jpg](/pictures/assembled4.jpg)