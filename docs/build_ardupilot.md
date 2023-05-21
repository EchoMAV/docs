## Building and Loading ArduPilot Firmware

As of ArduPilot 4.4, the EchoPilot AI hardware definition files are not yet pulled into the [ArduPilot repository](https://github.com/ArduPilot/ardupilot). Therefore, if you wish to use ArduPilot firmware on the EchoPilot AI, you will need to follow the steps below and build ArduPilot from source. Fortunately the process is straightforward:

### Prerequisites
These instructions were tested on Ubuntu 20.04 LTS. They are not guaranteed to work on any other flavor of Linux, within a virtual machine or under WSL 1 or 2. We recommend a **physical machine** running Ubuntu 20.04 LTS for the most pain-free experience.

### Download ArduPilot 
These instructions will install ArduPilot in ```~/ardupilot```. If you wish to use a different location, please adjust the directory below and throughout these instructions. If you are a novice, we recommend proceeding exactly as described below.
```
cd ~
git clone --recurse-submodules https://github.com/ArduPilot/ardupilot
cd ardupilot
```
### Setup the toolchain

```
Tools/environment_install/install-prereqs-ubuntu.sh -y
```
Now reload the path (log-out and log-in to make permanent)
```
. ~/.profile
```

### Checkout a release or tag
You can identify a version you wish to build by looking at the ArduPilot tags [https://github.com/ArduPilot/ardupilot/tags](https://github.com/ArduPilot/ardupilot/tags). In the example below, we will demonstrate checking out release ArduCopter-stable 

```
git checkout tags/ArduCopter-stable
git submodule update --init --recursive
```
!!! WARNING

    We have observed a failure to identify I2C compasses on ArduPilot 4.3 releases. If your design relies on the RM3100 compass onboard the EchoPilot AI, we recommend avoiding version 4.3/ This problem appears to have been fixed in 4.4+ releases. We recommend using version 4.2.4 or earlier, or 4.4+.

### Do a test build
Before we build firmware for the EchoPilot AI board, it is wise to first build a native target to verify that your toolchain and environment is setup and working. Build the sitl (software in the loop simulator) target first:
```
./waf configure --board sitl
./waf copter
```
If the build completes without errors, congrats! If there are errors, you will need to resolve them before proceeding.
### Build ArduPilot for the EchoPilot AI
First obtain the hardware board files from the [EchoPilot AI BSP](https://github.com/EchoMAV/echopilot_ai_bsp) repo and checkout the appropriate branch matching the hardware revision of your EchoPilot AI. The HW Revision is marked on the board silkscreen near the FAN connector:

```
git clone https://github.com/EchoMAV/echopilot_ai_bsp
cd echopilot_ai_bsp
git checkout board_revision_0
```
> Be sure you checked out the appropriate branch matching your EchoPilot AI hardware revision!

Install the ArduPilot board definition files into the correct folder using the provided `install_ardupilot.sh` script:
```
./install_ardupilot.sh ~/ardupilot
```
At this point, you should have the hardware files located in ```~/ardupilot/libraries/AP_HAL_ChibiOS/hwdef/EchoPilotAI/```. To build firmware targeting this board, use the command:
```
./waf configure --board EchoPilotAI
./waf copter
```
The example above builds copter, for other vehicle targets, see below:
```
./waf copter                            # All multirotor types
./waf heli                              # Helicopter types
./waf plane                             # Fixed wing airplanes including VTOL
./waf rover                             # Ground-based rovers and surface boats
./waf sub                               # ROV and other submarines
```

The .apj file will be located in the ```~/ardipilot/build//``` folder. The firmware is now ready to be loaded on the board.  
> **_NOTE:_** If the EchoPilot AI is plugged in to your host computer, unplug it before proceeding. The board should be totally powered off before proceeding.

```
./waf copter upload
```
When the build completes, the system will wait for a USB connection from the EchoPilot AI's bootloader. You should see a message indicating ```waiting for the bootloader...```. At this point, plug in a USB-A to USB-C cable between the host computer and the **FMU** USB connection on the EchoPilot AI. The board should be recognized and the firmware will be uploaded automatically.
> Optionally, you can use [QGroundControl](https://docs.qgroundcontrol.com/master/en/getting_started/download_and_install.html) to upload the ```~/ardupilot/build.....``` file created previously. This is especially useful if you wish to send a firmware update to a customer as they can do it without terminal access. Follow the steps here to upload **Custom Firmware** using QGroundControl: [https://docs.px4.io/main/en/config/firmware.html](https://docs.px4.io/main/en/config/firmware.html)