# EchoPilot AI Documentation

## Overview

The EchoPilot AI is a highly integrated vehicle control and edge computing system designed to power next-generation uncrewed systems. The EchoPilot AI supports computer vision, machine learning, autonomy, artificial intelligence and other advanced edge computing needs. The EchoPilot AI leverages the popular Ardupilot and PX4 projects, and uses Pixhawk open-hardware standards. The power of  an advanced autopilot is seamlessly combined with high-performance computing, IP networking, cloud connectivity and flexible low-latency hardware accelerated video encoding.

![EchoPilot AI](assets/echopilot_ai_stack.jpg)

The hardware is configured into a two board stack. The upper board is the EchoPilot AI board, and it contains the flight management unit, peripherals, sensors and Nvidia Jetson interface. The lower board is the Carrier Board, and it handles power regulation and connectors. Two high-density FX23L-80S-0.5SV 80-pin board-to-board connectors are used between the two boards.

This design philosophy achieves multiple goals:

1. For integrated vehicle solutions, it is often desired to design a custom carrier board to add additional components, minimize cables/wiring, integrate power distribution. In this case, our design allows you to design a carrier board (using the provided Carrier Board as a reference design) and in production products use only the EchoPilot AI board.
2. A stacked solution minimizes X-Y size in exchance for moving into the Z axis, which is an acceptable compromise for most uncrewed vehicles.
3. Moving the switching power regulators to the Carrier board reduced noise near the sensitive sensors on EchoPilot AI board.
4. A stacked design is more future proof, as periperals can often be added to the Carrier Board without a re-design of the EchoPilot AI main board.

## Quickstart Guide

These instructions assume you have a Jetson module that is already flashed. If you have a new Jetson module that is not flashed, please see [Flashing a Jetson](#flashing-a-jetson-module-using-the-echopilot-ai) instructions.

1. Assemble the EchoPilot AI board with a Carrier Board, using 8mm standoffs between the two boards.
2. If a Jetson Module is not already installed in the EchoPilot AI, install the module now.
3. Attached a USB cable between your host computer and J7 (Console) on the Carrier Board
4. Power the Carrier Board with 7-56VDC source capable of supplying up to 4A.
5. Once the Jetson Module boots
 
## Board Components EchoPilot AI

### Top Side

![Top Side Components](assets/top-side-labels.png)

### Bottom Side

![Bottom Side Components](assets/bottom-side-labels.png)

## Pinouts

#### Debug Power In 
This connector is **not normally used**. It exists only to power the EchoPilot AI without a carrier board attached.

Connector: J8, Part Number: B2B-XH-A(LF)(SN)  
Mating Connector: XHP-2

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
PIN 1        | Pwr            | GND           | Ground
PIN 2        | Pwr            | +5.2V          | Debug Power Input

#### FMU Debug
This connector is **not normally used** by the customer. It is primarily used during board setup to load bootloader firmware on the FMU. It is however possible to use the UART7 lines for other purposes.

Connector: J12, Part Number: SM06B-SRSS-TB(LF)(SN)  
Mating Connector: SHR-06V-S-B

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
PIN 1        | Pwr            | +3.3V           | 3.3V Power
PIN 2        | O            | +3.3V          | FMU UART7 TX
PIN 3        | I            | +3.3V          | FMU UART7 RX
PIN 4        | IO            | +3.3V         | FMU SWDIO
PIN 5        | O            | +3.3V          | FMU SWCLK
PIN 6        | Pwr           | GND          | Gnd

#### IO Debug
This connector is **not normally used** by the customer. It is used during board setup to load bootloader firmware on the IOMCU.

Connector: J13, Part Number: SM06B-SRSS-TB(LF)(SN)  
Mating Connector: SHR-06V-S-B

Pin Number   | Direction     | Voltage       | Pin Description
------------ | ------------- | ------------  | ------------
PIN 1        | Pwr            | +3.3V           | 3.3V Power
PIN 2        | O            | +3.3V          | IOMCU UART1 TX
PIN 3        | I            | +3.3V          | IOMCU UART1 RX
PIN 4        | IO            | +3.3V         | IOMCU SWDIO
PIN 5        | O            | +3.3V          | IOMCU SWCLK
PIN 6        | Pwr           | GND          | Gnd

## Mechanical

TBD Step Files
TBD Location of Screw Holes

## Notes on Vibration Isolation

TBD

## Building Code for the FMU

TBD 

### ArduPilot

```
TBD
```

### PX4

```
TBD
```

## Flashing a Jetson Module using the EchoPilot AI

TBD