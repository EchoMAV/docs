The Carrier Board is open-source, please visit the [echopilot_ai_carrier](https://github.com/EchoMAV/echopilot_ai_carrier) repository. While you may refer to the pinout information below, also feel free to examine the [pdf schematic](https://github.com/EchoMAV/echopilot_ai_carrier/blob/master/echopilot_ai_carrier_schematic.pdf) or the [full design](https://github.com/EchoMAV/echopilot_ai_carrier) in Kicad 6.0+.  

### Carrier Board Schematic

A full schematic of the carrier board is available: [PDF schematic](https://github.com/EchoMAV/echopilot_ai_carrier/blob/master/echopilot_ai_carrier_schematic.pdf) 

### Top Side Carrier Board

![Top Side Components](assets/top-side-labels-carrier-board.png)

#### Iridium Rockblock 9603 (J10)

This connector is for connection to a [Rockblock Iridium 9603 modem](https://www.groundcontrol.com/us/product/rockblock-9603-compact-plug-and-play-satellite-transmitter/).

Connector: J10, Part Number: 0532617010  
Mating Connector:  0510211000

| Pin Number | Direction | Voltage | Pin Desription    |
|------------|-----------|---------|-------------------|
| 1          | Pwr         | GND    | GND |
| 2          | NA         | NA    | NC |
| 3          | Pwr       | +5V     | +5V              |
| 4          | O        | 3.3V    | Iridium On/Off         |
| 5          | I           |   3.3V      | TX (from modem's perspective)          |
| 6          | I          |   3.3V      | Iridium Ring                 |
| 7          | I          |   3.3V      | Iridium Network Available                 |
| 8          | NA          |   NA      | NC                  |
| 9          |  NA         |   NA      | NC                  |
| 10         |  O         |  3.3V       | RX (from modem's perspective)    

#### Ethernet 2 (J9)
This connector is used for Ethernet (100 Mbps to the Jetson).

Connector: J9, Part Number: SM04B-GHS-TB(LF)(SN)  
Mating Connector: GHR-04V-S

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
1        | IO            | Diff Signal          | Rx+
2        | IO            | Diff Signal          | Rx-
3        | IO            | Diff Signal          | Tx+
4        | IO            | Diff Signal         | Tx-       

#### Ethernet 1 (J15)
This connector is used for Ethernet (100 Mbps to the Jetson).

Connector: J15, Part Number: SM04B-GHS-TB(LF)(SN)  
Mating Connector: GHR-04V-S

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
1        | IO            | Diff Signal          | Rx+
2        | IO            | Diff Signal          | Rx-
3        | IO            | Diff Signal          | Tx+
4        | IO            | Diff Signal         | Tx-          |


#### Board to Board Jetson (J5)
This connector handles the Jetson-related board to board signals. It connects to the EchoPilot AI board.  

Connector: J5, Part Number: FX23L-80P-0.5SV8  
Mating Connector: FX23L-80S-0.5SV  

| Pin Number | Direction | Voltage | Pin Desription    |
|------------|-----------|---------|-------------------|
| 1          | I         | 3.3V    | Jetson Console RX |
| 2          | O         | 3.3V    | Jetson Console TX |
| 3          | Pwr       | GND     | GND              |
| 4          | IO        | 1.8V    | CAM0_SDA0         |
| 5          | IO           |   1.8V      | CAM0_SCL0          |
| 6          | IO          |   1.8V      | CAM0_MCLK                  |
| 7          | IO          |   1.8V      | CAM0_GPIO                  |
| 8          | Pwr          |   GND      | GND                  |
| 9          |  IO         |   Diff Signal      | CAM0_D1+                  |
| 10         |  IO         |  Diff Signal       | CAM0_D1-                   |
| 11         |  Pwr         |   GND      | GND                  |
| 12         |  IO         |    Diff Signal     |  CAM0_CLK+                 |
| 13         |  IO         |  Diff Signal       | CAM0_CLK-                  |
| 14         |  Pwr         |   GND      | GND                  |
| 15         |  IO         |   Diff Signal      | CAM0_D0+                  |
| 16         |  IO         |   Diff Signal      | CAM0_D0-                  |
| 17         |  Pwr         |   GND      | GND                  |
| 18         | IO        | 1.8V    | CAM1_SDA0         |
| 19         | IO           |   1.8V      | CAM1_SCL0          |
| 20         | IO          |    1.8V     | CAM1_MCLK                  |
| 21         | IO          |    1.8V     | CAM1_GPIO                  |
| 22         | Pwr          |    GND     | GND                  |
| 23         | IO          |   Diff Signal      | CAM1_D1+                  |
| 24         | IO          |  Diff Signal       | CAM1_D1-                   |
| 25         |  Pwr         |    GND     | GND                  |
| 26         |  IO         |    Diff Signal     |  CAM1_CLK+                 |
| 27         |  IO         |   Diff Signal      | CAM1_CLK-                  |
| 28         |  Pwr         |   GND      | GND                  |
| 29         |  IO         |  Diff Signal       | CAM1_D0+                  |
| 30         |  IO         |  Diff Signal       | CAM1_D0-                  |
| 31         |  Pwr         |   GND      | GND                  |
| 32         |  IO         |  1.8V       | I2S0_DOUT                |
| 33         |  IO         |  1.8V       | I2SO_DIN                  |
| 34         |  IO         |  1.8V       | I2SO_FS                  |
| 35         |  IO         |  1.8V       | I2SO_SCLK                  |
| 36         |  IO         |  1.8V       | AUDIO_MCLK                 |
| 36         |  IO         |  1.8V       | GPIO12                  |
| 38         | IO          |  1.8V       | GPIO10                  |
| 39         |   Pwr        |  GND       | GND                  |
| 40         |   O        |   3.3V      | IRIDIUM RX UART                  |
| 41         |   IO        |  Diff Signal       |  ETH0 TX-                 |
| 42         |   IO        |   Diff Signal      |  ETH0 TX+                 |
| 43         |   IO        |   Diff Signal      |  ETH0 RX-                 |
| 44         |   IO        |   Diff Signal      |  ETH0 RX+                 |
| 45         |   Pwr        |   GND      |  GND                 |
| 46         |   IO        |   Diff Signal      |  ETH2 RX+                 |
| 47         |   IO        |   Diff Signal      |  ETH2 RX-                 |
| 48         |   IO        |   Diff Signal      |  ETH2 TX+                 |
| 49         |   IO        |   Diff Signal      |  ETH2 TX-                 |
| 50         |    Pwr       |    GND     |  GND                 |
| 51         |    IO       |    3.3V     |  JETSON I2C1_SDA                 |
| 52         |    IO       |    3.3V     |  JETSON I2C1_SCL                 |
| 53         |   NA        |   NA      |  NC                |
| 54         |   NA        |   NA      |  NC                 |
| 55         |   NA        |   NA      |  NC                 |
| 56         |   Pwr        |   GND      |  GND                 |
| 57         |   Pwr        |   5V      |  VBUS5                 |
| 58         |    IO       |  Diff Signal       |  USB5 D+                 |
| 59         |   IO        |  Diff Signal       |  USB5 D-                 |
| 60         |   Pwr        |   GND      |  GND                 |
| 61         |   Pwr        |    5V     |  VBUS4                 |
| 62         |    IO       |   Diff Signal      |  USB4 D+                 |
| 63         |    IO       |   Diff Signal      |  USB4 D-                 |
| 64         |    Pwr       |    GND     |  GND                 |
| 65         |    Pwr       |     5V    |  VBUS3                 |
| 66         |    IO       |   Diff Signal      |  USB3 D+                 |
| 67         |    IO       |   Diff Signal      |  USB3 D-                 |
| 68         |    Pwr       |   GND      |  GND                 |
| 69         |    Pwr OUT       |   5V      |  VBUS2                 |
| 70         |    IO      |   Diff Signal      |  USB2 D+            |
| 71         |    IO       |  Diff Signal       |  USB2 D-                 |
| 72         |    Pwr       |   GND      |  GND                 |
| 73         |    I       |   3.3V      |  IRIDIUM NA                 |
| 74         |    I       |   3.3V      |  IRIDIUM RING                 |
| 75         |    I       |   3.3V      |  IRIDIUM TX UART                 |
| 76         |    O       |   3.3V      |   IRIDIUM ON/OFF                |
| 77         |   Pwr OUT        |   1.8      |   +1.8V OUT               |
| 78         |Pwr OUT        |   1.8      |   +1.8V OUT                |
| 79         |   Pwr OUT        |   3.3      |   +3.3V OUT                |
| 80         |   Pwr OUT        |   3.3      |   +3.3V OUT                |
| 81         |   Pwr IN        |   5.1      |   +5.1V                |
| 82         |    Pwr IN       |   5.1      |   +5.1V                |
| 83         |  Pwr         |   GND      |    GND               |
| 84         |  Pwr         |   GND      |    GND               |

#### PWM Output from FMU (J28)
This connector provides the PWM outputs from the FMU. The EchoPilot AI's autopilot hardware consist of a main processor (FMU) and an IO processor. The IO processor provides 8 PWM outputs (labeled IO CHX below) and the FMU provides 4 PWM outputs. An important distinction between the two is that **only the FMU outputs are D-Shot compatible**.  

The +VServo Sense input is optional and is used by the FMU to detect a drop in the VServo rail. This is an input only, the Carrier board does **not** provide power to the servo voltage rail. 

> The EchoPilot AI comes with a PWM Breakout board which allows users to use standard Futaba-style (3 pin, 0.1" spacing) servo connectors. The PWM Breakout Board is plugged into this connector with the supplied cable. 

Connector: J28, Part Number: SM14B-GHS-TB(LF)(SN)  
Mating Connector: GHR-14V-S

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
1        | O            | +3.3          | IO CH1
2        | O            | +3.3         | IO CH2
3        | O            | +3.3          | IO CH3
4        | O            | +3.3         | IO CH4      
5        | O            | +3.3          | IO CH5
6        | O            | +3.3          | IO CH6
7        | O            | +3.3          | IO CH7
8        | O            | +3.3         | IO CH8   
9        | O            | +3.3          | FMU CH1
10        | O            |+3.3          | FMU CH2
11       | O            | +3.3          | FMU CH3
12        | O            | +3.3        | FMU CH4   
13        | I            | +5V          | +VServo Sense (Optional)
14        | Pwr            | GND              | GND

#### Board to Board FMU (J6)
This connector handles the FMU-related board to board signals.  It connects to the EchoPilot AI board.  

Connector: J6, Part Number: FX23L-80P-0.5SV8  
Mating Connector: FX23L-80S-0.5SV   

| Pin Number | Direction | Voltage | Pin Desription    |
|------------|-----------|---------|-------------------|
| 1          | 0         | 3.3V    | FMW PWM CH6 |
| 2          | O         | 3.3V    | FMW PWM CH5 |
| 3          | O       | 3.3V     | FMW PWM CH4              |
| 4          | O        | 3.3V    | FMW PWM CH3        |
| 5          | O           |   3.3V      | FMW PWM CH2          |
| 6          | O          |   3.3V      | FMW PWM CH1                  |
| 7          | O          |   3.3V      | IO PWM CH1                  |
| 8          | O          |   3.3V      | IO PWM CH2                   |
| 9          |  O         |   3.3V      | IO PWM CH3                   |
| 10         |  O         |  3.3V       | IO PWM CH4                    |
| 11         |  O         |   3.3V      | IO PWM CH5                   |
| 12         |  O         |    3.3V     |  IO PWM CH6                 |
| 13         |  O         |  3.3V       | IO PWM CH7                   |
| 14         |  O         |   3.3V      | IO PWM CH8                   |
| 15         |  Pwr         |   GND      | GND                  |
| 16         |  Pwr         |   GND      | GND                  |
| 17         |  Pwr OUT         |   +5V      | +5V OUT  (PROTECTED)                |
| 18         | O        | 3.3V    | FMU I2C_2 SCL         |
| 19         | IO           |   3.3V      |    FMU I2C_2 SDA       |
| 20         | Pwr          |    GND     |    GND               |
| 21         | Pwr OUT         |    +5V     |   +5V OUT (PROTECTED)                |
| 22         | IO          |    Diff Signal     | CAN 2+                   |
| 23         | IO          |   Diff Signal      | CAN 2-                  |
| 24         | Pwr          |  GND       | GND                   |
| 25         |  Pwr OUT         |    +5V     | +5V OUT (PROTECTED)                 |
| 26         |  IO         |    Diff Signal     |  CAN 1+                 |
| 27         |  IO         |   Diff Signal      |  CAN 1-                  |
| 28         |  Pwr         |   GND      | GND                  |
| 29         |  Pwr OUT         |  +5V       | +5V OUT (PROTECTED)                  |
| 30         |  O         |  +3.3V       | TELEM1_RTS                  |
| 31         |  I         |   +3.3V      | TELEM1_CTS                 |
| 32         |  I         |  +3.3V      | TELEM1_RX                |
| 33         |  O         |  +3.3V       | TELEM1_TX                  |
| 34         |  Pwr         |  GND      | GND                  |
| 35         |  I         |  3.3V       | BATTERY CURRENT SENSE                  |
| 36         |  I         |  3.3V       | BATTERY VOLTAGE SENSE                 |
| 36         |  Pwr         |  GND      | GND                  
| 38         |  I          |  +3.3V       | +VSERVO SENSE                  |
| 39         |   Pwr        |  GND       | GND                  |
| 40         |   NA        |   NA      | NC   |
| 41         |   Pwr OUT        |  Pwr       |  +5V OUT (PROTECTED)                 |
| 42         |   O        |   +3.3V      |  SPI5 SCLK                 |
| 43         |   I        |   +3.3V     |  SPI5 MISO                 |
| 44         |   I        |   Diff Signal      |  SPI5_MOSI                |
| 45         |   O        |   +3.3V      |  SPI5 CS1  (PI4)               |
| 46         |   O        |   +3.3V      |  SPI5 CS2 (PI10)                |
| 47         |   Pwr        |   GND      |  GND                 |
| 48         |   Pwr OUT       |   +5V      |  +5V OUT (PROTECTED)                 |
| 49         |   O        |   +3.3V      |  GPS1 TX                 |
| 50         |    I       |    +3.3V     |  GPS1 RX                 |
| 51         |    O       |    3.3V     |  FMU I2C_1 SCL                 |
| 52         |    IO       |    3.3V     |  FMU I2C_1 SDA                 |
| 53         |   Pwr        |   GND      |  GND                |
| 54         |   I        |   +3.3V      |  SAFETY SWITCH IN                 |
| 55         |   O        |   +3.3V      |  SAFETY SWITCH LED OUT                 |
| 56         |   Pwr OUT       |   +3.3V      |  +3.3V OUT (SAFETY)                 |
| 57         |   O        |   +5V      |  BUZZER OUT                 |
| 58         |    Pwr       |  GND       |  GND                |
| 59         |   Pwr OUT        |  +5V       |  +5 VOUT (PROTECTED)                 |
| 60         |   I        |   +3.3V      |  RC INPUT                 |
| 61         |   Pwr        |   GND     |  GND                 |
| 62         |    Pwr IN      |   +5.4V      |  +5.4V IN FMU                 |
| 63         |    Pwr IN       |   +5.4V      |  +5.4V IN FMU                 |
| 64         |    Pwr IN       |    +5.4V     |  +5.4V IN FMU                 |
| 65         |    Pwr IN       |     +5.4V    |  +5.4V IN FMU                 |
| 66         |    Pwr       |   GND      |  GND                |
| 67         |    Pwr       |   GND      |  GND                 |
| 68         |    Pwr       |   GND      |  GND                 |
| 69         |    Pwr        |   GND      |  GND                 |
| 70         |    I      |   +3.3V      |  VDD POWER A VALID            |
| 71         |    I       |  +3.3V       |  VDD POWER B VALID                 |
| 72         |    O       |   +3.3V      |  SBUS OUTPUT                 |
| 73         |    O       |   3.3V      |  FMU UART4 TX                 |
| 74         |    I       |   3.3V      |  FMU UART4 RX                 |
| 75         |    Pwr       |   GND      |  GND                 |
| 76         |    NA       |   NA      |   NC                |
| 77         |   NA        |   NA      |   NC              |
| 78         |   NA        |   NA      |   NC                |
| 79         |   NA        |   NA     |   NC                |
| 80         |   NA        |   NA      |   NC               |
| 81         |   Pwr IN        |   +5.1V      |   +5.1V (JETSON POWER)     |
| 82         |    Pwr IN        |   +5.1V      |   +5.1V (JETSON POWER)     |
| 83         |  Pwr         |   GND      |    GND               |
| 84         |  Pwr         |   GND      |    GND               |

#### +5V Out

#### +VBattery

#### GPS/Compass

#### Radio In

#### Power In

### Bottom Side Carrier Board

![Bottom Side Components](assets/bottom-side-labels-carrier-board.png)

#### MIPI Cam 2

#### MIPI Cam 1

#### CAN 2 (FMU)

#### Telem1

#### I2C 2 (FMU)

#### V/I Sense

#### CAN 1 (FMU)

#### USB4

#### USB3

#### USB2

#### USB1