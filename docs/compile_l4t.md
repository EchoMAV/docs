# Compiling L4T for the Xavier NX on the EchoPilot AI

## Instructions for customizing the device tree and compiling the kernel for the Xavier NX on EchoPilot AI

When a Jetson Xavier NX module is included with an EchoPilot AI purchase, it is flashed with a custom Linux for Tegra (L4T) image which includes support for the hardware and pin configuration of the EchoPilot AI. If you wish to build/update the kernel for use with the EchoPilot AI, the instructions below will provide the information and files you need to ensure your custom image remains fully compatible with the EchoPilot AI hardware. When compared to a standard Nvidia development carrier board, the primary differences in the EchoPilot AI hardware are:

1. The EchoPilot AI does not have an I2C HDMI controller
2. The EchoPilot AI has an SD Card (SDMMC3)

To minimize console errors due to (1) and to enable the SD card on SDMMC3, the kernel must be compiled from source and flashed to the Xavier NX using the Debug USB port and recovery mode. It is not possible to update only the dtb files because the pinmux changes require a full flash. The following instructions will walk you through the process.

!!! WARNING
    
    These instructions were developed and tested on Ubuntu 20.04 LTS (with a Windows machine used for the Excel pinmux change). We recommend using a *physical* machine running Ubuntu 20.04 LTS.

    These instructions assume you are using a _Production_ Jetson SOM. These instructions will not work with the SOM included with a Jetson developer kit. 
    
What you will doing:

1. Download and setup the necessary files
2. Replace .dtb and .cfg files, and create a extlinux.conf file
3. Generate the image and flash the device

So buckle up and let's get started.

> _These instructions are adapted from the the excellent document by Hao Ye availabe on [medium.com](https://medium.com/@haoye94/editing-device-tree-and-compiling-kernel-for-nvidia-jetson-xavier-nx-11a1df20939c) along with documentation pulled from Nvidia's forums. Some minor changes are include from Hao Ye's document, most likely as it was created for an older L4T release (32.6.1)._

### Download and Setup Necessary Files

Note that you will need to create an NVIDIA developer account and login to download, so if you do not have a developer account please [set that up](https://developer.nvidia.com/login) before proceeding. 
Next you will need to download three packages from Nvidia: [Driver Package (BSP), Sample Root Filesystem and Driver Package (BSP) Sources](https://developer.nvidia.com/embedded/jetson-linux). 

> These instructions were developed using Jetson Linux 35.3.1. These instructions _may_ continue to work for future releases,   but proceed with caution.

The files to download are highlighted in blue below:
![l4t_downloads](assets/l4t_downloads.png)

The instructions below assume that the downloaded files are downloaded to the `~/Downloads/` folder.  

#### Extract Driver Package (BSP)
> Note: the filename below will be different if you download a different version.

```
mkdir -p ~/XavierNX
tar -xf ~/Downloads/Jetson_Linux_R35.3.1_aarch64.tbz2 -C ~/XavierNX
```
#### Extract kernel sources (Driver Package (BSP) Sources)
In the public_sources.tbz2 (BSP sources) zip file, there will be many other zipped files inside, but we are only interested in kernel_src.tbz2. Extract this file into a folder to named `source` within the `Linux_for_Tegra` folder. The steps are:
```
mkdir ~/Downloads/temp
tar -xf ~/Downloads/public_sources.tbz2 -C ~/Downloads/temp
mkdir ~/XavierNX/Linux_for_Tegra/source && tar -xf ~/Downloads/temp/Linux_for_Tegra/source/public/kernel_src.tbz2 -C ~/XavierNX/Linux_for_Tegra/source
```
#### Extract sample Root File System  (Sample Root Filesystem)
Extract contents into Linux_for_Tegra/rootfs/. Note the filename below will be different if you downloaded a different version.
```
mkdir ~/XavierNX/Linux_for_Tegra/rootfs
tar -xf ~/Downloads/Tegra_Linux_Sample-Root-Filesystem_R35.3.1_aarch64.tbz2 -C ~/XavierNX/Linux_for_Tegra/rootfs/
```

### Get the EchoPilot .dtb, .cfg and extlinux.conf files

The files you will need to replace include the device tree binary (.dtb), pinmux configuration (.cfg) and extlinux.conf files. These files can be obtained from the echopilot_dtb_pinmux repository [https://github.com/EchoMAV/echopilot_dtb_pinmux](https://github.com/EchoMAV/echopilot_dtb_pinmux). Use the steps below to clone and install these files:

Clone the files:
```
cd ~
git clone https://github.com/EchoMAV/echopilot_dtb_pinmux
cd echopilot_dtb_pinmux
```
Checkout the appropriate branch using the naming convention rev_[x]_[jetson_som]. For example, EchoPilot AI rev0 hardware and the Xavier NX SOM would be branch `rev_0_xavier_nx`.
```
git checkout rev_0_xavier_nx
```
Run the install script to copy the cfg, dtb and extlinux.conf files into your Linux_for_Tegra folder. The usage is `./install.sh [Path to Linux_for_Tegra]`, e.g.:
```
./install.sh ~/XavierNX
```
Ensure this script completes with no errors before proceeding with flashing.

### Flash device
1. Plug in a usb cable (this will require a JST-GH to micro usb female adapter for Rev0 boards) to the Jetson Debug port (J25) on the EchoPilot AI. Rev 0 is shown below to help you locate this connector. Note: future versions of hardware may use a USB micro connector for J25 rather than a JST-GH connector.
![Bottom Side Components](assets/bottom-side-labels.png)
2. Hold the recovery button down. (see image below for location of the recovery button).
![Top Side Components](assets/top-side-labels.png)
3. Apply power, and release recovery button after a few seconds.
4. Flash device:

```
cd ~/XavierNX/Linux_for_Tegra/
sudo ./flash.sh jetson-xavier-nx-devkit-emmc mmcblk0p1
```



