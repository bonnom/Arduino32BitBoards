# Arduino32bitBoards device adapter
This git contains a new Micro-Manager device adapter for Arduino 32-bits boards.
This device adapter contains extra futures compared to the regular arduino device adapter.

Changes:
* Added PWM control
* Unified DAC and PWM
* Can do DAC/PWM blanking on all 8 channels
* Changed unit of DAC/ PWM from "Volt" to "Power %" and the default scale to 0-100
* Three extra output channels to a total of 8
* Channels 1 and 2 are by default the DAC channels

## Advantages of 32 Bit-boards in general
* Much faster, because of higher clock speed and more is done per clockcycle.
* Baudrate increased to 500 000, nearly 9 times the transferspeed between Arduino and Micro-Manager (there are some exceptions). This can be even increased to 2 000 000
* Most 32-bit Arduinos have a buildin DAC (max 3.3V output)
* Higher PWM frequencies and PWM bitresolutions

## Working Arduino boards:
### ESP32
- Baudrate: 115200
- ADC not implemented
- Able to set PWM frequency and Resolution    
- KEEP IN MIND: NOT 5V TOLERANT!!
- Pins Used
  - Trigger: Pin 5
  - Channel 1: Pin 25 (DAC)
  - Channel 2: Pin 26 (DAC)
  - Channel 3: Pin 27
  - Channel 4: Pin 15
  - Channel 5: Pin 14
  - Channel 6: Pin 4
  - Channel 7: Pin 23
  - Channel 8: Pin 19
  
### Featherboards M4
- Baudrate 500 000
- The ADC does not work at the moment because of DAC implementation
- 12 bit PWM
- KEEP IN MIND: NOT 5V TOLERANT!!
- Pins Used
  - Trigger: Pin 5
  - Channel 1: Pin A0 (DAC)
  - Channel 2: Pin A1 (DAC)
  - Channel 3: Pin 6
  - Channel 4: Pin 9
  - Channel 5: Pin 10
  - Channel 6: Pin 11
  - Channel 7: Pin 12
  - Channel 8: Pin 13
 
 
### Teensy 3.x Boards
* All 3.x boards
  - Able to set PWM frequency and Resolution, for more information [link](https://www.pjrc.com/teensy/td_pulse.html)
  - handy: Pinouts page [https://www.pjrc.com/teensy/pinout.html]
  - Baudrate 500 000
 
* Teensy 3.1 & 3.2 (Please use 96Mhz)
  - All currently used pins in the sketch are 5V tolerant
  - Current PWM frequency: 11718.75 Hz
  - Pins Used
    - Trigger: Pin 2
    - Channel 1: Pin A14 (DAC)
    - Channel 2: Pin 20
    - Channel 3: Pin 3
    - Channel 4: Pin 4
    - Channel 5: Pin 5
    - Channel 6: Pin 6
    - Channel 7: Pin 21
    - Channel 8: Pin 22

* Teensy 3.5 (recommended) & Teensy 3.6
  - Current PWM frequency: 14648.437 Hz
  - Currently used pins are 5V tolerant for Teensy 3.5
  - KEEP IN MIND: Teensy 3.6 is not 5V tolerant!!
    - Trigger: Pin 2
    - Channel 1: Pin A21 (DAC)
    - Channel 2: Pin A22 (DAC)
    - Channel 3: Pin 3
    - Channel 4: Pin 4
    - Channel 5: Pin 5
    - Channel 6: Pin 6
    - Channel 7: Pin 7
    - Channel 8: Pin 8
