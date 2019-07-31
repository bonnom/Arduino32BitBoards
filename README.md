# Arduino32bitBoards device adapter
This git contains a new Micro-Manager device adapter for Arduino 32-bits boards.
This device adapter contains extra futures compared to the regular arduino device adapter.

Changes:
* Added PWM control
* Unified DAC and PWM
* Can do DAC/PWM blanking on all 8 channels
* Changed unit of DAC/ PWM from "Volt" to "Power %" and the default scale to 0-100
* Added three extra output channels to a total of 8

## Advantages of 32 Bit-boards in general
* Much faster, because of higher clock speed and more is done per clockcycle.
* Baudrate increased to 500 000, nearly 9 times the transferspeed between Arduino and Micro-Manager (there are some exceptions). This can be even increased to 2 000 000, with micro-manager 2
* Most 32-bit Arduinos have a buildin DAC (max 3.3V output)
* Higher PWM frequencies and PWM bitresolutions

## Working Arduino boards:
* ESP32
  - Baudrate: 115200
  - Trigger Pin: 5
  - DAC1 on pin 25 and DAC2 on pin 26
  - ADC not implemented
  - Able to set PWM frequency and Resolution
  - Low Price boards available       
  - KEEP IN MIND: NOT 5V TOLERANT!!
  
* Feather M4
  - The ADC does not work at the moment because of DAC implementation
  - Trigger Pin: 5
  - Channel 8 has become channel 7
  - KEEP IN MIND: NOT 5V TOLERANT!!
 
 
### Teensy 3.x Boards
* All 3.x boards
  - Able to set PWM frequency and Resolution, for more information [link](https://www.pjrc.com/teensy/td_pulse.html)
  - At least one DAC
  - Trigger Pin: 5
  - handy: Pinouts page [https://www.pjrc.com/teensy/pinout.html]
 
* Teensy 3.1 & 3.2
  - Seems to work fine, but more testing is needed
  - All currently used pins in the sketch are 5V tolerant
  - Only one DAC on pin A14
  - All other pins are the same as the original UNO firmware

* Teensy 3.5
  - Not yet tested
  - All currently used pins in the firmware are 5V tolerant
  - DAC1 on pin 21 and DAC2 on pin 22
  - Able to set PWM frequency and Resolution

* Teensy 3.6
  - Same pinouts as Teensy 3.5
  - Teensy 3.6: NOT 5V TOLERANT!!
  
## Not working boards:
  - Sipeed Maix boards

## To be tested:
 - Teensy LC
 - A SAMD21 board
 - Arduino Due

