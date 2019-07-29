# Arduino32bitBoards device adapter
This git contains a new Micro-Manager device adapter for Arduino 32-bits boards.
This device adapter contains extra futures compared to the regular arduino device adapter.

Changes:
* Added PWM control
* Unified DAC and PWM
* Changed unit of DAC/ PWM from "Volt" to "Power %" and the default scale to 0-100
* Added three extra output channels to a total of 8
