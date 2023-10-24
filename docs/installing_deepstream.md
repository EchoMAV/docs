# Installing DeepStream and CUDA for the Jetson

NVIDIA® DeepStream Software Development Kit (SDK) is an accelerated AI framework to build intelligent video analytics (IVA) pipelines. DeepStream runs on NVIDIA® Jetson NX™, NVIDIA® Jetson Orin™ NX, NVIDIA® Jetson Orin™ Nano in conjunction with the EchoPilot AI. 

The CUDA Toolkit provides a development environment for creating high-performance GPU-accelerated applications.

The instructions below show how to install both. These instructions were developed using a Jetson Orin NX with a 256 GB SSD, running L4T 35.4.1. In most cases, you will not be able to install this software without significant available storage space. E.g., an Xavier NX with only a 16 GB eMMC will not have enough storage space. We recommend adding a NVMe SSD before proceeding. 
!!! note
    The instructions below assume that the EchoPilot AI has internet access and you are logged in to the console. Since EchoPilotAI Jetson hardware is provided with a static IP address, it is often simpler to enable DHCP and let the Jetson get internet through your LAN's router. To do this, you can use the nmcli commands to change the static-eth0 connection profile to auto/hdcp.
    ```
    sudo nmcli con mod static-eth0 ipv4.method auto
    sudo nmcli con down static-eth0
    sudo nmcli con up static-eth0
    ```
    When you are done and would like to return the IP config to static, use:
    ```
    sudo nmcli con mod static-eth0 ipv4.addresses "10.223.44.55/16"   # For example
    sudo nmcli con down static-eth0
    sudo nmcli con up static-eth0
    ```

### Install DeepStream

Start by doing an apt update
```
sudo apt-get update
```
### Install dependencies
```
sudo apt install \
build_essential \
libssl1.1 \
libgstreamer1.0-0 \
gstreamer1.0-tools \
gstreamer1.0-plugins-good \
gstreamer1.0-plugins-bad \
gstreamer1.0-plugins-ugly \
gstreamer1.0-libav \
libgstreamer-plugins-base1.0-dev \
libgstrtspserver-1.0-0 \
libjansson4 \
libyaml-cpp-dev
```
### Install librdkafka 

1. Clone the repo
```
git clone https://github.com/edenhill/librdkafka.git
```
2. Configure, build and install
```
cd librdkafka
git reset --hard 7101c2310341ab3f4675fc565f64f0967e135a6a
./configure
make
sudo make install
```
3. Copy the generated files to the deepstream directory.
```
sudo mkdir -p /opt/nvidia/deepstream/deepstream-6.3/lib
sudo cp /usr/local/lib/librdkafka* /opt/nvidia/deepstream/deepstream-6.3/lib
```
### Get and install the Deepstream SDK
```
wget --content-disposition 'https://api.ngc.nvidia.com/v2/resources/org/nvidia/deepstream/6.3/files?redirect=true&path=deepstream-6.3_6.3.0-1_arm64.deb' -O deepstream-6.3_6.3.0-1_arm64.deb
sudo apt-get install ./deepstream-6.3_6.3.0-1_arm64.deb
```
### Install CUDA
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/sbsa/cuda-keyring_1.1-1_all.deb
sudo dpkg -i cuda-keyring_1.1-1_all.deb
sudo apt-get update
sudo apt-get -y install cuda-toolkit-12-3
```
### Install Cuda driver
```
sudo apt-get install -y cuda-drivers
```

### Boost the clocks
```
sudo nvpmodel -m 8
$ sudo jetson_clocks
```
Now *Reboot* the system.

### Verify functionality

At this point, deepstream-app should run without errors:
```
deepstream-app --help
```
### Explore Sample Code

Browse and Run precompiled sample applications in `sources/apps/sample_apps`
Follow the directory’s README file to run the application.