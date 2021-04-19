# CUDA 10.2 & cuDNN 7.6.5 Installation Guide

This repository contains the guide for installing CUDA 10.2 and cuDNN 7.6.5 for Ubuntu 20.04 LTS. 

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




## CUDA 10.2 Installation

The following information is taken from the [official CUDA Toolkit Installation Guide](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#system-requirements) by Nvidia


### Step 1. Download CUDA 10.2
	wget https://developer.download.nvidia.com/compute/cuda/10.2/Prod/local_installers/cuda_10.2.89_440.33.01_linux.run
	
	sudo sh cuda_10.2.89_440.33.01_linux.run
### Step 2. If an prompt appears, type continue then accept the EULA

### Step 3. Uncheck Nvidia Drivers

### Step 4. Install

### Step 5. Download Patches
Go to [CUDA Toolkit 10.2 archive](https://developer.nvidia.com/cuda-10.2-download-archive) > Linux > x86_64 > Ubuntu > 18.04 > runfile (local)

 - Patch 1 (Released Aug 26, 2020)
 - Patch 2 (Released Nov 17, 2020)

### Step 6. Install all patches
	sudo sh filename.run

### Step 7. Edit ~/.bashrc

	sudo gedit ~/.bashrc
### Step 8. Add the following to the end of the file:

	export PATH=/usr/local/cuda/bin:$PATH  
	export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
	
### Step 9. Reboot System
	sudo reboot

### Step 10. Check CUDA Version
	nvcc --version
export PATH=/usr/local/cuda/bin:$PATH  
	export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
	
## CUDNN v7.6.5 Installation
The following information is taken from the [Official cuDNN Documentation](https://docs.nvidia.com/deeplearning/cudnn/developer-guide/index.html) by NVIDIA

### Step 1. Go to the latest [cuDNN 7.6.5](https://docs.nvidia.com/deeplearning/cudnn/install-guide/index.html) for CUDA 10.2 archive

### Step 2. Download the following files

1. cuDNN Runtime Library for Ubuntu18.04 (Deb)
2. cuDNN Developer Library for Ubuntu18.04 (Deb)
3. cuDNN Code Samples and User Guide for Ubuntu18.04 (Deb)


### Step 3. Install the downloaded files
Install the Runtime library first, then developer, then lastly the code samples

	sudo dpkg -i filename.deb

### Step 4. Verify installation

1. Copy the cuDNN samples to a writable path.

		cp -r /usr/src/cudnn_samples_v7/ $HOME

2. Go to the writable path.

		cd  $HOME/cudnn_samples_v7/mnistCUDNN

3. Compile the  mnistCUDNN  sample.

		make clean && make

4. Run the mnistCUDNN sample

		./mnistCUDNN

If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:

	Test passed!
