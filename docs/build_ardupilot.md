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
You can identify a version you wish to build by looking at the ArduPilot tags [https://github.com/ArduPilot/ardupilot/tags](https://github.com/ArduPilot/ardupilot/tags). In the example below, we will demonstrate checking out release Copter-4.3.7 

```
git checkout Copter-4.4.1
git submodule update --init --recursive
```

### Do a test build
Before we build firmware for the EchoPilot AI board, it is wise to first build a native target to verify that your toolchain and environment is setup and working. Build the sitl (software in the loop simulator) target first:
```
./waf configure --board sitl
./waf copter
```
If the build completes without errors, congrats! If there are errors, you will need to resolve them before proceeding.
### Download and Install the Hardware Definition Files for ArduPilot
Obtain the hardware board files from the [EchoPilot AI BSP](https://github.com/EchoMAV/echopilot_ai_bsp) repo and checkout the appropriate branch matching the hardware revision of your EchoPilot AI using the commands below. The Hardware revision is marked on the board silkscreen near the FAN connector:

```
git clone https://github.com/EchoMAV/echopilot_ai_bsp
cd echopilot_ai_bsp
git checkout board_revision_1a     # Select the appropriate revision
```
!!! warning
    Be sure you checked out the appropriate branch matching your EchoPilot AI hardware revision!

Use the `install_ardupilot.sh` script to automatically copy the EchoPilot HW hardware definition files into the right place in the ardupilot directory structure. The first (and only) argument when using this script is the path to where you have the ardupilot repo installed on your system, e.g., `~/ardupilot`. For example:
```
./install_ardupilot.sh ~/ardupilot
```
### Build ArduPilot for the EchoPilot AI
At this point, you should have the EchoPilot AI hardware files located in ```~/ardupilot/libraries/AP_HAL_ChibiOS/hwdef/EchoPilotAI/```. To build firmware targeting EchoPilot AI, use the command:
```
cd ~/ardupilot
./waf configure --board EchoPilotAI
./waf copter    # or choose a different target per below
```
!!! tip

    The example above builds copter, for other vehicle targets, see below:
    ```
    ./waf copter                            # All multirotor types
    ./waf heli                              # Helicopter types
    ./waf plane                             # Fixed wing airplanes including VTOL
    ./waf rover                             # Ground-based rovers and surface boats
    ./waf sub                               # ROV and other submarines
    ```

The arducopter.apj and arducopter.bin file will be located in the ```~/ardupilot/build/EchoPilotAI/bin/``` folder. The firmware is now ready to be loaded on the board. This can be done by adding the upload argument as explained below, or using common ground control station software such as Mission Planner or QGroundControl to upload the ```apj``` file.

!!! info
    If the EchoPilot AI's FMU USB connection is plugged in to your host computer, unplug it before proceeding. Also ensure the board is fully powered down. The board should be totally powered off before proceeding. The FMU will get power via the USB cable in the step below.

#### Uploading using the WAF script
```
./waf copter --upload
```
When the build completes, the system will wait for a USB connection from the EchoPilot AI's bootloader. You should see a message indicating ```waiting for the bootloader...```. At this point, plug in a USB-A to USB-C cable between the host computer and the **FMU** USB connection on the EchoPilot AI. The board should be recognized and the firmware will be uploaded automatically.

#### Upload using QGroundControl 
Optionally, you can use [QGroundControl](https://docs.qgroundcontrol.com/master/en/getting_started/download_and_install.html) to upload the `~/ardupilot/build/EchoPilotAI/bin/arducopter.apj` file created previously. This is especially useful if you wish to send a firmware update to a customer as they can do it without terminal access. Follow the steps to upload **Custom Firmware** using QGroundControl: [https://docs.qgroundcontrol.com/master/en/SetupView/Firmware.html](https://docs.qgroundcontrol.com/master/en/SetupView/Firmware.html)