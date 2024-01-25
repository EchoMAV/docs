## Building and Loading PX4 Firmware

As of PX4 1.13.3, the EchoPilot AI hardware definition files are not yet pulled into the [PX4 repository](https://github.com/PX4/PX4-Autopilot). Therefore, if you wish to use PX4 firmware on the EchoPilot AI, you will need to follow the steps below and build PX4 from source. Fortunately the process is straightforward:

### Prerequisites
These instructions were tested on Ubuntu 20.04 LTS. They are not guaranteed to work on any other flavor of Linux, within a virtual machine or under WSL 1 or 2. We recommend a **physical machine** running Ubuntu 20.04 LTS for the most pain-free experience.

### Download PX4 
These instructions will install PX4 in ```~/PX4-Autopilot```. If you wish to use a different location, please adjust the directory below and throughout these instructions. If you are a novice, we recommend proceeding exactly as described below.
```
cd ~
git clone https://github.com/PX4/PX4-Autopilot.git --recursive
cd PX4-Autopilot
```
### Setup the toolchain
Note if you have built PX4 before, you can likely skip this step. Also remove the ```--no-sim-tools``` option if you wish to install the simulation toolchain.
```
bash ./Tools/setup/ubuntu.sh --no-sim-tools
```
At this point, it is recommended to log out and back in to ensure the paths are loaded.
### Checkout a release
You can identify a version you wish to build by looking at the release history [https://github.com/PX4/PX4-Autopilot/releases](https://github.com/PX4/PX4-Autopilot/releases). In the example below, we will demonstrate checking out release 1.13.3  
!!! info
    You can reuse an existing repo rather than cloning a new one if this isn't your first PX4 rodeo. In this case, clean the build environment before proceeding:
    ```
    make clean
    make distclean
    ```

```
git fetch origin v1.13.3
git checkout v1.13.3
```
Update submodules:
```
make submodulesclean
```
### Do a test build
Before we build firmware for the EchoPilot AI board, it is wise to first build a native target to verify that your toolchain and environment is setup and working. Build the px4_sitl (software in the loop simulator) first:
```
make px4_sitl
```
If the build completes without errors, congrats! If there are errors, you will need to resolve them before proceeding.
### Build PX4 for the EchoPilot AI
First obtain the hardware board files from the [EchoPilot AI BSP](https://github.com/EchoMAV/echopilot_ai_bsp) repo and checkout the appropriate branch matching the hardware revision of you EchoPilot AI. The HW Revision is marked on the board silkscreen near the FAN connector:

```
git clone https://github.com/EchoMAV/echopilot_ai_bsp
cd echopilot_ai_bsp
git checkout board_revision_1b   # Change per your hardware
```
!!! warning
    Be sure you checked out the appropriate branch matching your EchoPilot AI hardware revision!

Use the provided install script `install_px4.sh` to place the PX4 board definition files into the correct folder. The first argument is the path to where you have the ardupilot repo on your system, e.g. `~/PX4-Autopilot`:
```
./install_px4.sh ~/PX4-Autopilot
```
At this point, you should have the hardware files located in ```~/PX4-Autopilot/boards/echomav/echopilot-ai/```. To build firmware targeting this board, use the command:
```
make echomav_echopilot-ai
```
The .px4 file will be located in the ```~/PX4-Autopilot/build/echomav_echopilot-ai_default/``` folder. The firmware is now ready to be loaded on the board.  

!!! info
    If the EchoPilot AI is plugged in to your host computer, unplug it before proceeding. Also ensure there is **no power** to the EchoPilot AI. The board should be totally powered off before proceeding. The FMU will get power via the USB cable in the step below.

```
make echomav_echopilot-ai upload
```
When the build completes, the system will wait for a USB connection from the EchoPilot AI's bootloader. You should see a message indicating ```waiting for the bootloader...```. At this point, plug in a USB-A to USB-C cable between the host computer and the **FMU** USB connection on the EchoPilot AI. The board should be recognized and the firmware will be uploaded automatically.
> Optionally, you can use [QGroundControl](https://docs.qgroundcontrol.com/master/en/getting_started/download_and_install.html) to upload the ```~/PX4-Autopilot/build/echomav_echopilot-ai_default/echomav_echopilot-ai_default.px4``` file created previously. This is especially useful if you wish to send a firmware update to a customer as they can do it without terminal access. Follow the steps here to upload **Custom Firmware** using QGroundControl: [https://docs.px4.io/main/en/config/firmware.html](https://docs.px4.io/main/en/config/firmware.html)