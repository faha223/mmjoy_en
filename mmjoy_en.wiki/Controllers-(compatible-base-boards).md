The supported chips are made by ATMEL:
at90usb646
at90usb1286
atmega32u4 (at 5 volt power supply and 16 MHz quartz).

These chips have hardware USB support for the updating their firmware. All you need is to flash the board and connect it to your PC.
Althoug you can solder the board for the chips yourself, it is more cost-effective to use existing boards based on these chips:

![Sparkfun "ProMicro"](https://github.com/gordonhch/mmjoy_en/blob/master/img/Board%20pinouts/Pins_Sparkfun%5Bpromicro%5D.png?raw=true)
Sparkfun "ProMicro" (atmega32u4, 18 pins available, 9 of them are available for the axes of the internal ADC directly)

![Arduino "Leonardo"](https://github.com/gordonhch/mmjoy_en/blob/master/img/Board%20pinouts/Pins_Arduino%5Bleonardo%5D.png?raw=true)
Arduino "Leonardo" (atmega32u4, 20 pins total, 12 of them are available for the axes of the internal ADC directly)

![Arduino "Micro"](https://github.com/gordonhch/mmjoy_en/blob/master/img/Board%20pinouts/Pins_Arduino%5Bmicro%5D.png?raw=true)
Arduino "Micro" (atmega32u4, 24 pin total, 12 of them are available for the axes of the internal ADC directly)

![PJRC "Teensy 2.0"](https://github.com/gordonhch/mmjoy_en/blob/master/img/Board%20pinouts/Pins_PJRC%5BTeensy2.0%5D.png?raw=true)
PJRC "Teensy 2.0" (atmega32u4, 25 pin total, 12 of them are available for the axes of the internal ADC directly)

![PJRC "Teensy ++ 2.0"](https://github.com/gordonhch/mmjoy_en/blob/master/img/Board%20pinouts/Pins_PJRC%5BTeensy_pp_2.0%5D.png?raw=true)
PJRC "Teensy ++ 2.0" (at90usb1286, 46 pin total, 8 of them are available for the axes of the internal ADC directly)

"B6" for TLE5010-GEN - this pin are shared for all TLE5010/5011 sensors.
"B3" for SPI-MISO - this pin are shared for all "SPI" sensors (TLE5010/5011/kma200/mcp3201-3208).
"B1" for SPI-SCK - this pin are shared for all "SPI" sensors (TLE5010/5011/kma200/mcp3201-3208).
"SPI-CS" - you can connect as you like, and where you connect CS-pin need to setup at configurator. this pin are individual to sensor. (F4 & F5 - just a sample).
also additional data line "SPI-MOSI" shared for "SPI" sensors mcp3202-3208.
(http://simhq.com/forum/ubbthreads.php/topics/3903870/32)


What is the difference between the controllers?
All the functions of the joystick work the same on all boards and chips. The only difference is in quantity of abailable pins on a particular circuit board, the greater it is, the more legs can be connected directly to the buttons and axes.