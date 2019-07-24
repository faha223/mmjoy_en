# Connecting basic inputs
## Input types
[A button or a switch](https://en.wikipedia.org/wiki/Switch) sends the signal by creating a link between two pins, letting the force flow through it. (Some buttons may have more than two pins. Three pin buttons one central pin and two position indicators (one for on, one for off). 4-pin buttons have their pins connected in pairs (effectively, two buttons actuated by one press simultaneously).

An [encoder](https://en.wikipedia.org/wiki/Rotary_encoder) is a rotary switch that returns discrete values to the board.

An axis input  is a continuous signal that can be received from either an analogue [potentiometer](https://en.wikipedia.org/wiki/Potentiometer) or digital sensor (like [Hall sensor](https://en.wikipedia.org/wiki/Hall_effect_sensor)).

Here is the schematics of connection different inputs to arduino with gordonhch on board:
![Connection examples](https://github.com/gordonhch/mmjoy_en/blob/master/img/Hardware%20connection/common_hardware_connections.png)

## Connecting axis
Connection of axis is fairly straightforward: two pins of potentiometer/sensor are connected to power and ground, and center pin goes to Axis pin on the board (see [board pinouts](https://github.com/gordonhch/mmjoy_en/wiki/Controllers-(compatible-base-boards))) Please note that you can connect your axes to the pin that has AI (axis internal) mark on it.

If you want to increase the precision of your input source, you can use external analog-to-digital converter chip, like MCP 3208. This will allow you to crank the precision from 10 to 12, yay!

The example of connection between MCP3208 and ProMicro is right below. Pay attention to orientation!
![MCP3208](https://github.com/gordonhch/mmjoy_en/blob/master/img/Hardware%20connection/mcp3208.png)
The lay6 files are situated in [PCB folder in repo](https://github.com/gordonhch/mmjoy_en/tree/master/PCB)

## Connecting buttons
### Single button connection
Buttons and switches have at least 2 contacts and thus require 2 pins. They will send the signal by connecting them. Any board pin, except for the service ones (Reset/GND/VCC/AREF), can be used for a button

The connection of button to your board is fairly simple. To avoid ghost button presses you have to use diodes (e.g. 1N4148) after each button:
![One button connection](https://github.com/gordonhch/mmjoy_en/blob/master/img/Buttons%20and%20axis/Button_02.png?raw=true)

### Button matrix
To increase the number of buttons that can be connected to MMjoy, you can use a [button matrix](http://pcbheaven.com/wikipages/How_Key_Matrices_Works/), as in MMjoy predecessors MJoy8 and MJoy16:

![connection example](https://github.com/gordonhch/mmjoy_en/blob/master/img/Hardware%20connection/Button%20matrix%20fritzig.png)

Each button in matrix has its own ROW:COLUMN address. Again, to avoid ghost button presses you have to use diodes (e.g. 1N4148) after each button. You have to place it so that the line on the diode is aligned closer to buttons row wire.

MMJoy2 supports matrix of different sizes up to 10 by 10 buttons (e.g. 1 by 10 will work). Matrix size is chosen in JoySetup.exe configuration program.

Here is an example of button matrix on prototype board:
![button matrix photo](https://github.com/gordonhch/mmjoy_en/blob/master/img/Hardware%20connection/Button%20matrix%20photo.jpg)


### Shift registers
[A shift register](https://learn.sparkfun.com/tutorials/shift-registers) is another way to connect a huge amount of buttons to limited inputs. It reads the inputs of the buttons connected to it and feeds this information into the Arduino in form of a byte array. For example, one 74HC165 shift register supports up to 8 buttons connected to a single pin on your base board. What is even cooler, shift registers can form a chain.
![Shift register project](https://github.com/gordonhch/mmjoy_en/blob/master/img/Hardware%20connection/Shift%20register%20project.jpg)<br>
You can find this and other designs in the MMjoy2/PCB folder in the archive or in the [repo](https://github.com/gordonhch/mmjoy_en/tree/master/PCB).
Connection of a shift register to the board depends on its type. MMjoy2 software supports 74HC165 and 4021 shift registers.

Here is an example of shift register 74HC165 soldered to the PCB:
![Shift register1](https://github.com/gordonhch/mmjoy_en/blob/master/img/Hardware%20connection/Shift%20register%20photo.jpg)

The shift registers take in only signal wires from your buttons. The ground pin is common for all your buttons. This makes shift registers much more compact than button matrix, as you need only 1 wire to the board. On the other hand, button matrix is a bit simpler to understand and a bit easier to implement in terms of materials. But it becomes messy very quickly, so if you have more than 10 buttons - go for switch registers.  

# MMjoy2 basic software setup
To let the board know what kind of input to expect, you will have to setup the software and write your config to the board. In the following section I will describe the possible configuration options.

## Define input pins
On the [compatible boards page](https://github.com/gordonhch/mmjoy_en/wiki/Controllers-(compatible-base-boards)) you can see that each pin has an address assigned to it in square brackets (D0, F0 etc). For each of you inputs that you have connected you will have to set the appropriate pin, so please memorize them.

## Axis options
Axes are setup on the first screen of MMJoysetup program:
![axes overview](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/Axis%20overview.PNG)
Lets explore the options as they are listed in the software.

### Mandatory stuff
#### Source
In Source dropdown you have to select the type of axis input.  
**Virtual** - in this mode you will emulate axis changes by buttons. More on that later.  
**IntSensor** - a usual analogue source, like potentiometer.   
**MCP3201, MCP3201, MCP3204s/MCP3208s, MCP3204d/MCP3208d, KMZ60+MCP3202, KMZ60+MCP3208s, TLE5010/5011, S/C-TLE5010/5011** - if you have a digital signal source from a chip in this list, choose your option.

#### MCU port
For analogue source you have to define the pin, to which you have connected the signal pin (usually the center one) of the potentiometer. For digital source, you have to define the connection of CS pin.

#### Channel
In case you have multi-channel digital sensor, in this field you will have to choose the number of the pin you have connected your source to.

#### Value raw
If your axis was defined correctly, after you write the setting to device, in this field you will see the raw values received from the sensor

#### Values processed
Given that you see raw values already, this field will show the values applying the filter (will be mentioned later)

#### Assignment
In this field you will have to assign your hardware axis to the HID joystick axis for Windows. Please note that without assignment you will not be able to use the axis at all, and setup program will return you an error.

#### Precision
Here you define the precision of the sensor you use. If you don't know what it is, here is the rule of thumb: If you have Hall sensor, MagRez or just potentiometer connected directly to the board - set it to 10. If you connect these inputs using MCP3208 chip, set it to 12.

#### Filter
If your axis is "noisy" and you want to make its signal more consistent, you can select a value for filtering its fluctuations. You want to keep this as low as possible.

#### Auto-calibration and calibration min/center/max fields
In this dropdown you can select calibration options for your axis. It can be set to Auto, and the software will adjust the axis range automatically after you move it to its full range. Another option is set it to manual, and define top, center and bottom values in the following fields.
The options with center (w center) will be helpful if you have the axis with asymmetrical movement - e.g. pitch axis will be shorter for pitch down and longer for pitch up. When you choose this option the software will either calculate the center position of your stick automatically (auto w center) or read the calibration center value (saved w center).

### Optional stuff
Under this section I situated more advanced parameters and those that will allow you do correct the hardware faults.

#### Invertion
Yup, this inverts the axis. Welcome to Australia!

#### Decrease, increase, return to center and Step of change
This options are available if you have selected Virtual source. In the first three fields you can select the _hardware_ button that will change the Virtual axis value in accordance with its function. The step of change defines increments of axis increase or decrease

#### Special Functions
In this dropdown you are to select the profile of the axis, if you want to. The profiles are defined on the second screen, 
"Joystick axes special functions". 

#### DZ low, center, high and dynamical
These fields will define the range in which raw values change will not affect the filtered value at all. The dynamical deadzone is a nice one: the software listens to axis readings 1000 times per second or so. If the last 3 readings were the same (which means you stopped moving the handle) it applies the deadzone value to it. This is useful when you have shimmering axis input.

#### Link errors
Here you will see if the software has lost your sensor. Useful for debugging.

## Joystick axes (Spec. Functions)
On this screen you are able to define custom response curve for each function if you are into that kinky stuff. 

## Button options
In this section we will review galaxy of button assignment options.
![Buttons](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/Buttons%20overview.PNG)

### Choose your source
Remeber - there are two options for buttons. You can either make a button matrix or a shift register board. 
You can define your input for buttons in the following sections:
![BM](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/Button%20Matrix.PNG)
For button matrix, you have to define the pins to which rows and columns are connected.
![SR](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/Shift%20registers%20setup.PNG) 
For shift registers you will define its type, the number of chips, CS signal pin, and MISO pin (the pin which is connected to Data leg on shift register).

### Check hardware buttons responce
![hardware buttons](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/HW%20buttons.PNG)
If you have done your job right and saved sets to device, the hardware buttons section will respond to your buttons presses by lighting up in red:  
This will help you later in mapping hardware buttons to virtual buttons and functions.

### Timers and shifts
![timers and shifts](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/timer%20and%20shifts.PNG)
This menus will allow you to set up to 3 types of delay for your switches and encoders, and define the modificators (shifts) to bind several virtual buttons to 1 hardware button and a shift. Pay attention, class, more on that later!

## Button mapping
Now its time to assign your hardware buttons to the buttons on your virtual joystick in Windows.

### Virtual buttons and keyboard/mouse emulation
![button mapping](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/Button%20setup.PNG)
#### Modes
For different type of inputs you can employ diffent modes: <br>
**Switch mode** means the virtual button will be pressed when 1) the button is pressed and 2) the button is released. <br>
**Switch on mode**  activates virtual button only when the real button is pressed<br>
**Switch off mode**, on the contrary, activates virtual button only when the real button is released<br>
**Soft switch mode** will act as software button fixation: when you pressed the button for the first time the virtual <br>button will be activated, when you press it the second time - virtual button is deactivated.<br>
**Encoder mode** is activated automatically for encoders set in the designated section. In this mode the activation of encoder positions is stored, and you can spin the encoder with a drill - and the board will store them and feed into the PC gradually, according to the timers set (see below)<br>

#### Shifts
After defining shifts in the designated section of the MMjoySetup, you can assign different virtual buttons to the same hardware button+shift combination

#### Timers
You can set the duration of timers in the designated section of the configurator. **Timer on** sets the time for which your virtual button will be pressed. **Timer off** sets the time for the period when you will not be able to activate the virtual button again. 
Consider using an encoder for example. You can spin the handle really fast, and the PC will not be able to register the button presses properly. Setting the timers for encoder will let the PC receive stable length of virtual button presses.
The other case it may be useful for is a bad shimmering button - when holding it will give you multiple unwanted virtual button presses. This may be avoided by employing timers.

### Advanced functions: Axis to buttons, Hats and Encoders
![Superfunctions](https://github.com/gordonhch/mmjoy_en/blob/master/img/Software%20setup%20screenshots/Axis%20to%20buttons%20and%20hats.PNG)  

These menus will allow you to enable functions like axis increments (e.g. from 100% to 0% in one click), and recognition of your buttons as hats or encoders