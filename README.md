# CUDA 10.2 Installation Guide

This repository contains the guide for installing CUDA 10.2 for Ubuntu 20.04 LTS. 
For more information, please see the [official CUDA Toolkit Installation Guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#system-requirements) by Nvidia

## Requirements

 - Ubuntu 20.04 LTS
 - CUDA Capable GPU

## Pre-Installation Steps

### GCC
To avoid future issues with gcc, it is recommended that we install multiple versions of gcc then switch depending on the requirement. 

*This section is taken from an article by [Lubos Rendek](https://linuxconfig.org/how-to-switch-between-multiple-gcc-and-g-compiler-versions-on-ubuntu-20-04-lts-focal-fossa). All credits goes to the author.* 


**Step 1. Install multiple C and C++ compiler versions:**

    sudo apt install build-essential
    sudo apt -y install gcc-7 g++-7 gcc-8 g++-8 gcc-9 g++-9

**Step 2. Use the `update-alternatives` tool to create list of multiple GCC and G++ compiler alternatives:**


    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-7 7
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-7 7
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-8 8
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-8 8
    sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-9 9
    sudo update-alternatives --install /usr/bin/g++ g++ /usr/bin/g++-9 9
    
   **Step 3. Check the available C and C++ compilers list on your [Ubuntu 20.04](https://linuxconfig.org/ubuntu-20-04-guide) system and select desired version by entering relevant selection number:**
   
	sudo update-alternatives --config gcc

	There are 3 choices for the alternative gcc (providing /usr/bin/gcc).

	  Selection    Path            Priority   Status
	------------------------------------------------------------
	  0            /usr/bin/gcc-9   9         auto mode
	  1            /usr/bin/gcc-7   7         manual mode
	* 2            /usr/bin/gcc-8   8         manual mode
	  3            /usr/bin/gcc-9   9         manual mode
	Press  to keep the current choice[*], or type selection number:
	
   ***For C++ compiler execute:***

	sudo update-alternatives --config g++
	
	There are 3 choices for the alternative g++ (providing /usr/bin/g++).

	  Selection    Path            Priority   Status
	------------------------------------------------------------
	* 0            /usr/bin/g++-9   9         auto mode
	  1            /usr/bin/g++-7   7         manual mode
	  2            /usr/bin/g++-8   8         manual mode
	  3            /usr/bin/g++-9   9         manual mode

	Press  to keep the current choice[*], or type selection number:

**Step 4. Each time after switch check your currently selected compiler version:**

	    $ gcc --version
	    $ g++ --version

***Choose gcc-9***


### Nvidia GPU

**Step 1. Add PPA repository**
	
	sudo add-apt-repository ppa:graphics-drivers/ppa
	
**Step 2. Install Nvidia Drivers.**
At the time of this writing, the latest Nvidia PPA driver is 460

	sudo apt install nvidia-driver-460
	
**Step 3. Reboot system**

	sudo reboot

**Step 4. Check installed drivers**

	nvidia-smi

	Mon Apr 19 12:43:22 2021       
	+-----------------------------------------------------------------------------+
	| NVIDIA-SMI 460.67       Driver Version: 460.67       CUDA Version: 11.2     |
	|-------------------------------+----------------------+----------------------+
	| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
	| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
	|                               |                      |               MIG M. |
	|===============================+======================+======================|
	|   0  GeForce RTX 2060    Off  | 00000000:01:00.0  On |                  N/A |
	| N/A   47C    P8     8W /  N/A |    379MiB /  5926MiB |      2%      Default |
	|                               |                      |                  N/A |
	+-------------------------------+----------------------+----------------------+

	+-----------------------------------------------------------------------------+
	| Processes:                                                                  |
	|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
	|        ID   ID                                                   Usage      |
	|=============================================================================|
	|    0   N/A  N/A       923      G   /usr/lib/xorg/Xorg                 53MiB |
	|    0   N/A  N/A      1650      G   /usr/lib/xorg/Xorg                126MiB |
	|    0   N/A  N/A      1778      G   /usr/bin/gnome-shell              107MiB |
	|    0   N/A  N/A      2487      G   ...AAAAAAAAA= --shared-files       80MiB |
	+-----------------------------------------------------------------------------+


