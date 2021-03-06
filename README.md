I orginally wrote this code for my bachelor project, so I might not currently work with micro-manager but for questions, feel free to ask under the "Issue section" of this repository.

# Arduino32bitBoards device adapter
This git contains a new Micro-Manager device adapter for Arduino 32-bits boards.
This device adapter contains extra features compared to the regular arduino device adapter.

Currently the Teensy 3.5 is the recommended board to be used with this device adapter, bur there is also firmware available for the teensy 3.2, ESP32 and feather M4.

Differences compared to regular Arduino Device Adapter:
* Two extra output channels to a total of 8
* Added Pulse-width modulation (PWM) control
* Unified DAC and PWM
* Unified digital-out channels and DAC/PWM channels, this allows DAC/PWM blanking on all 8 channels
* Changed unit of DAC/ PWM from "Volt" to "Power %" and the default scale to 0-100
* In the Firmware: Channels 1 - 2 are by default DAC channels, channels 3-8 are by default PWM

## Contents
  - [Advantages and Disadvantages of Arduino 32 Bit-boards in general](advantages-and-disadvantages-of-Arduino-32-bit-boards-in-general)
  - [Arduino boards information](#arduino-boards-information) contains settings and pinouts
  - [Installation](#installation)
  - [Drivers](#drivers)
  - [Known bugs](#bugs)
  
## Advantages and Disadvantages of Arduino 32 Bit-boards in general
### Advantages
* Much faster, because of higher clock speed and more is done per clockcycle.
* Baudrate increased to 500 000, nearly 9 times the transferspeed between Arduino and Micro-Manager (there are some exceptions). This can be even increased to 2 000 000
* Most 32-bit Arduinos have a buildin DAC (max 3.3V output)
* Higher PWM frequencies and PWM bitresolutions
* More flexibility with pins used

### Disadvantages
* Most are not 5V tolerant, this means you'll need voltage level converter when using the triggerpin. It is recommended to use Teensy 3.5 since this board does have 5V tolerant inputs. When using a not 5V tolerant board it is recommended to use a voltage level converter like this one [link](https://www.adafruit.com/product/757) or this one [link](https://www.sparkfun.com/products/12009)
* Library support might not always be great


## Arduino boards information:
### ESP32
- Baudrate: 115200
- ADC not implemented
- Able to set PWM frequency and Resolution
- Low cost boards available
- KEEP IN MIND: NOT 5V TOLERANT!!
- Pins Used
  - Trigger: Pin 5
  - Channel 1: Pin 25  (DAC)
  - Channel 2: Pin 26  (DAC)
  - Channel 3: Pin 27  (PWM)
  - Channel 4: Pin 15  (PWM)
  - Channel 5: Pin 14  (PWM)
  - Channel 6: Pin 4   (PWM)
  - Channel 7: Pin 23  (PWM)
  - Channel 8: Pin 19  (PWM)

### Featherboards M4
- Baudrate 500 000
- The ADC does not work at the moment because of DAC implementation
- 12 bit PWM
- KEEP IN MIND: NOT 5V TOLERANT!!
- Pins Used
  - Trigger: Pin 5
  - Channel 1: Pin A0  (DAC)
  - Channel 2: Pin A1  (DAC)
  - Channel 3: Pin 6   (PWM)
  - Channel 4: Pin 9   (PWM)
  - Channel 5: Pin 10  (PWM)
  - Channel 6: Pin 11  (PWM)
  - Channel 7: Pin 12  (PWM)
  - Channel 8: Pin 13  (PWM)
 
### Metro M4 Express
- Traditional form factor
- Baudrate 500 000
- The ADC does not work at the moment because of DAC implementation
- 12 bit PWM
- KEEP IN MIND: NOT 5V TOLERANT!!
- Pins Used
  - Trigger: Pin 5
  - Channel 1: Pin A0  (DAC)
  - Channel 2: Pin A1  (DAC)
  - Channel 3: Pin 8   (PWM)
  - Channel 4: Pin 9   (PWM)
  - Channel 5: Pin 10  (PWM)
  - Channel 6: Pin 11  (PWM)
  - Channel 7: Pin 12  (PWM)
  - Channel 8: Pin 13  (PWM)

### Teensy 3.x and 4.0 Boards
* All 3.x boards
  - Able to set PWM frequency and Resolution, for more information [link](https://www.pjrc.com/teensy/td_pulse.html)
  - handy: Pinouts page [https://www.pjrc.com/teensy/pinout.html]
  - Baudrate 500 000
 
* Teensy 3.1 & 3.2 (Please use 96Mhz)
  - All currently used pins in the sketch are 5V tolerant
  - Has one DAC on pin A14
  - Current PWM frequency: 11718.75 Hz
  - Pins Used
    - Trigger: Pin 2
    - Channel 1: Pin A14 (DAC)
    - Channel 2: Pin 20  (PWM)
    - Channel 3: Pin 3   (PWM)
    - Channel 4: Pin 4   (PWM)
    - Channel 5: Pin 5   (PWM)
    - Channel 6: Pin 6   (PWM)
    - Channel 7: Pin 21  (PWM)
    - Channel 8: Pin 22  (PWM)

* Teensy 3.5 **_(recommended)_** & Teensy 3.6
  - Currently used pins are 5V tolerant for Teensy 3.5
  - KEEP IN MIND: Teensy 3.6 is not 5V tolerant!!
  - Current PWM frequency: 14648.437 Hz
  - Pins used:
    - Trigger: Pin 2
    - Channel 1: Pin A21 (DAC)
    - Channel 2: Pin A22 (DAC)
    - Channel 3: Pin 3   (PWM)
    - Channel 4: Pin 4   (PWM)
    - Channel 5: Pin 5   (PWM)
    - Channel 6: Pin 6   (PWM)
    - Channel 7: Pin 7   (PWM)
    - Channel 8: Pin 8   (PWM)
 
* Teensy 4.0
  - KEEP IN MIND: not 5V tolerant!!
  - Very fast
  - Does not have a DAC
  - Current PWM frequency: 468750 Hz (At 7-bits)
  - Pins used:
    - Trigger: Pin 8
    - Channel 1: Pin 23  (PWM)
    - Channel 2: Pin 15  (PWM)
    - Channel 3: Pin 3   (PWM)
    - Channel 4: Pin 4   (PWM)
    - Channel 5: Pin 10  (PWM)
    - Channel 6: Pin 9   (PWM)
    - Channel 7: Pin 6   (PWM)
    - Channel 8: Pin 5   (PWM)
  - Sketch has weird pinout because the firmware was written to be used with a Feather 3.x adapter board
  

## Installation
This page is an overview of the installation links for Arduino and the respective boards

### Arduino (Required)
Arduino offers two solutions, an online editor and a local Integrated development environment (IDE) program.
It is recommended to use the local IDE software.
The page for the software can be found [here](https://www.arduino.cc/en/Main/Software)

### Adafruit
Adafruit makes two programming environments to use on their 32-bit boards. One is circuit python and Arduino. Circuitpython currently doesn't work with micro-manager.
Guide for installing the Adafruit Feather M4 board can be found [here](https://learn.adafruit.com/adafruit-feather-m4-express-atsamd51/setup)

### Esp32
ESP32 arduino core installation link can be found [here](https://github.com/espressif/arduino-esp32/blob/master/docs/arduino-ide/boards_manager.md)
Also when using an windows version older than Windows 10 driver installation might be needed. There are two types of usb to serial chips used with each their own driver. If you are not sure what IC is used just install both drivers.

These two are the most common type of drivers:
* [SiLabs cp210x](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)
* [CH340] (https://cdn.sparkfun.com/assets/learn_tutorials/8/4/4/CH341SER.EXE)

### Teensy boards
Teensy requires its own installation software that can be downloaded [here](https://www.pjrc.com/teensy/td_download.html)

## Drivers
On windows 10 the Arduino-compatible board drivers are automatically installed, but this is not the case for windows 7 and below.

There are two ways to install the Arduino-compatible board drivers, the first is to install the Arduino IDE and than to install the board under boards-manager. The second way is to install the standalone driver packages. The standalone drivers are listed below.

### Adafruit Serial Drivers:
* Most general driver package
* Includes drivers for FTDI
* Includes SiLabs CP210x drivers

[Adafruit Drivers](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/latest)

[Source Drivers](https://learn.adafruit.com/adafruit-arduino-ide-setup/windows-driver-installation)

### CH340G:
* Used on a lot of Arduino-compatible boards from China

[Windows Drivers](https://cdn.sparkfun.com/assets/learn_tutorials/8/4/4/CH341SER.EXE)

[Source Drivers](https://www.sparkfun.com/products/14050)

### FTDI Drivers
* Used on a lot of arduino-compatible boards (also included in the Adafruit Serial Driver package)
(Drivers)[https://www.ftdichip.com/Drivers/VCP.htm]

### SiLabs Drivers
* Used on a lot of arduino-compatible boards (also included in the Adafruit Serial Driver package)

(Drivers) [https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers]

### Teensy Serial Drivers:
[Windows Serial Installer](https://www.pjrc.com/teensy/serial_install.exe)

[Source Drivers](https://www.pjrc.com/teensy/td_download.html)

## Bugs
When a bug isn't listed here, please report it under 'Issues' above.

* Using different exposure times in multi-dimensional acquisition can lead to problems. It is not yet known if this is caused by Arduino or the Andor camera

* The Arduino will behave slow and sporadic under multi-dimensional acquisition if not a channel has been selected first under 'Configuration settings' in the main micro-manager window.

