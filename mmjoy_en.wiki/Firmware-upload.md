#Driver installation
1) Download the [firmware archive](https://github.com/gordonhch/mmjoy_en/tree/master/firmware%20and%20software%20release) and unzip it.
You must not use spaces and any symbols other than English in the folder path.
Use something as simple as C:\mmjoy2[v20150626]:

![folder to unpack](https://github.com/gordonhch/mmjoy_en/blob/master/img/firmware/01%20-%209743DOG.png?raw=true)

2) Connect the board to the USB port
Windows will detect a new hardware as "Arduino Leonardo (COMXX)" or just "USB serical device (COMxx)" under "Ports (COM & LPT)" and is most likely to offer to install the driver. If it doesn't, use Control Panel -> Device Manager. Choose your board, right click on the unrecognised device it and choose "Update driver"->"Browse my computer for driver software".

![device manager update drivers](https://github.com/gordonhch/mmjoy_en/blob/master/img/firmware/02%20-%206GnogvK.png?raw=true)

The next step is to specify where to find the driver (in the folder where we extracted project files, e.g.  "C:\MMJOY2[v20150626]").

During installation, Windows may warn that it could not verify the publisher of this driver. Click "Install anyway".

Please note that COM port number is assigned randomly, and may differ from my example

#Updating firmware

##Switching to service mode
The compatible boards work in two modes: operational mode for day-to-day use and service (bootloader) mode for firmware updates. When you switch your board into service mode, it will be active for 8 seconds and then the board will switch to operational mode automatically.

To turn service mode on, we must perform the following actions:

#####On ProMicro board
Briefly short GND and RST pins
#####On Leonardo and Micro boards
Preset RESET button

The device "Arduino Leonardo (COMxx)" will disappear, replaced by a new device and Windows will install new drivers. The L led will start blinking, slowly fading. If all goes well it will be a new device "Arduino Leonardo bootloader (COMyy)" or "USB serical device (COMyy)". Make sure your COM port number is different (xx!=yy)

Don't worry - for the first time you may NOT see the new device. Wait for a minute and repeat bootloader switching process - and Windows will eventually show it to you.

Do this several times to get used to the timing before you perform the actual update

##Performing the update
For Arduino Leonardo:<br>
1) Open the JoySetup.exe program, go to the "Firmware" tab <br>
2) Select the firmware file according to your chip. For me it was "Firmware_lufa_[MMJOY2.ATMEGA32U4].hex" (it will be in the folder where you unzipped the file). <br>
3) Select the chip of your board - on Arduino Leonardo its "atmega32u4" <br>
4) Choose loader type according to your board, in my case - "Arduino" <br>
5) Enter the number COMYY in com port section - the one that is assigned in service mode. The prefix "COM" is obligatory, and it must be in Latin!<br>
6) When all fields are filled in, switch your board to service mode.<br>

The device "Arduino Leonardo" will disappear from the list and if the COM port has been correctly specified the _field will be green_. 

![Configuration](https://github.com/gordonhch/mmjoy_en/blob/master/img/firmware/05%20-%20CLRmNw2.png?raw=true)

Now it is time to press the button "Upload firmware" in Configurator.
If everything was done correctly and on time, a console window will be displayed, logging the firmware update process.

Upon successful completion,  a new device "MMJOY2", or "HID-compliant vendor-defined device" will be displayed in device manager under HID devices, Windows will install the driver again and may ask for a reboot.

![HID setup](https://github.com/gordonhch/mmjoy_en/blob/master/img/firmware/09%20-%20stwzIYH.png?raw=true)

Congratulations!

#Known issues
Sometimes on Windows 8 you may receive an error notification about driver installation error (Windows can't add the driver to its storage). To fix this, you will need to disable driver signature enforcement  (https://learn.sparkfun.com/tutorials/disabling-driver-signature-on-windows-8/disabling-signed-driver-enforcement-on-windows-8)