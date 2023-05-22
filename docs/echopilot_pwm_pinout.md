## EchoPilot PWM Breakout Board Pinout

![PWM Breakout](assets/echopilot_ai_6.png)
![PWM Breakout Board](assets/echopilot_pwm_breakout.JPG)

#### JST to EchoPilot Connector
This connector is used along with the provided cable to connect J20 on the Carrier Board.

Connector: J1, Part Number: SM14B-SRSS-TB(LF)(SN)  
Mating Connector: SHR-14V-S-B

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
PIN 1        | Pwr            | GND          | GND
PIN 2        | Pwr            | +5V          | +VServo Sense
PIN 3        | O            | +3.3V          | FMU PWM CH4
PIN 4        | O            | +3.3V         | FMU PWM CH3
PIN 5        | O            | +3.3V          | FMU PWM CH2
PIN 6        | O           | +3.3V          | FMU PWM CH1
PIN 7        | O            | +3.3V           | IO PWM CH8
PIN 8        | O            | +3.3V          | IO PWM CH7
PIN 9         | O            | +3.3V          | IO PWM CH6
PIN 10        | O            | +3.3V         | IO PWM CH5
PIN 11        | O            | +3.3V          | IO PWM CH4
PIN 12        | O           | +3.3V          | IO PWM CH3
PIN 13        | O            | +3.3V           | IO PWM CH2
PIN 14        | O            | +3.3V          | IO PWM CH1

#### Header PWM Outputs
This connector is used along with the provided cable to connect J20 on the Carrier Board.  

!!! warning

    The middle ("+") pin is bussed together, allowing you to distribute your VServo voltage using this connector. The EchoPilot AI does **NOT** provide VServo voltage, this must be supplied by an external regulator, BEC, etc. Typically this is provided by an Electronic Speed Controller (ESC) in the system.


Connector: J2, Part Number: TSW-112-08-G-T-RA_1  
Mating Connector: Standard 0.1" spacing servo/esc Futaba style

![PWM Breakout End View](assets/echopilot_pwm_endview.png)