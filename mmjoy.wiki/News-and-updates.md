#News and updates

## MMJOY2 [v20150928update1]
Posted on Sep 27. 2015 22:49 User mega mozg [updated Sep 28. 2015 3:17]
### MMJOY2 [v20150928]
Fixed hang-ups after rebooting the OS.
Added Croatian translation (Hrvatski).
Now you can activate debounce mode for simple buttons (select one of the timers, and select the desired delay interval).
Added the ability to output to the 7-segment 8 character LED screens MAX7219 up to 32 characters.

### MMJOY2 [v20150928update1]
added a small module "Calibration assistant"

## MMJOY2 [v20150727 Firmware update]
Posted on July 28, 2015, 11:51 user mega mozg
Insignificant firmware correction, concerns only the calculation of magnet poles change.

## Update MMJOY2 [v20150727]
Posted on July 26, 2015, 23:22 user mega mozg [Updated July 26, 2015, 23:23]

Small optimizations:
Keyboard and mouse are activated only after their resources are enabled in Configurator;
Delay timers for buttons are set up as a multiplication of 10ms;
Modifiers for keyboard are revised, added distinction between left and right ctrl / alt / shift;
Added program "MMjoyWarthunder" to output information from the game "Warthunder" by custom rules to to LED strips WS2811 (example of work can be seen on Volodya @DVik channel: https://www.youtube.com/watch?v=c2v0dfKvG3Y)

## Update MMJOY2 [v20150722]
Posted on July 22, 2015, 12:09 user mega mozg [Updated July 22, 2015, 12:22]

Keyboard emulator adds capability to select modifiers (Shift / Control / Alt / GUI (win)).
Mouse scroll emulation is added for mouse emulator, as well as full mouse control with buttons (axes and scroll).
The number of controllable WS2812 LEDs is increased to 20 pieces.
Shift setting for buttons are now extended. Firmware allows you to assign a button to shift and distinguish its on and off states.

## Update MMJOY2 [v20150717]
Posted on July 17, 2015, 11:06 user mega mozg

Added emulation of mouse and keyboard.
Two axis X and Y and up to 3 buttons can be assigned to mouse emulation
Up to 10 keys can be assigned to a keyboard.

## Update MMJOY2 [v20150709]
Posted on July 9, 2015, 2:24 User mega mozg [Updated July 9, 2015, 2:24]

The ability to output sine and cosinefor is added for TLE5010 / TLE5011 (sensor type "S / C-TLE5010 / 5011") Additional field to set up channel 1 or channel 2 is added.
This makes it possible to use one sensor to receive input as two axes, according to the same scheme as in the Logitech G940, Thrustmaster Warthog / T16000, Saitek X55 / Rhino 
![example](http://i.imgur.com/1fwpORc.png)


## Update MMJOY2 [v20150706]
Posted on July 6, 2015, 0:47 to Alexander Makarov [Updated July 6, 2015, 0:48]

Fixed "kma200" work. Added forced calibration for kma200, kmz60 and tle5010.
## Update MMJOY2 [v20150701]
Posted on July 1, 2015, 3:38 User mega mozg

Changed the connection of shift registers to the controller because of frequent errors began to appear. E.g. for "incompatible SPI sensors"   (eg mcp3208 or TLE5010 / 5011) and shift registers (as in the handle of "Cobra M5" or "Thrustmaster").
Changed one leg, that was previously connected to the "SPI-MISO" and is now connected to the "SPI-MOSI" - in such an embodiment, the shift registers do not interfere with other SPI periphery.
Pictures "[Shift_register]_DefenderCombaM5" and "[Shift_register]_Thrustmaster Warthog_Cougar" are corrected.

## Update MMJOY2 [v20150626]
Posted on June 26, 2015, 11:47 user mega mozg

Work with the buttons - added "Toggle" mode, timer delay and shift keys.
Working with axes - manual calibration is now really manual (you need to enter raw values in the field  for a sensor), added communication check for sensors TLE5010 / TLE5011.
Minor configurator interface fixes.

