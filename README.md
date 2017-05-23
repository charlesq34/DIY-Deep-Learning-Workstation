# DIY-Deep-Learning-Workstation
Build a deep learning workstation from scratch. While this document is written for Ubuntu 14.04 with TensorFlow, most steps should also apply to other Ubuntu versions and deep leanring frameworks.

Have fun DIY-ing!

### Contents
1. [Build a GPU Workstation](#1-build-a-gpu-workstation)
2. [Install Ubuntu](#2-install-ubuntu)
3. [Install CUDA and cuDNN](#3-install-cuda-and-cudnn)
4. [Install TensorFlow](#4-install-tensorflow)
5. [Others](#5-others)

**Disclaimer:** This document records my own experience and lessons learnt in building a workstation for deep learning. However, there is no gurantee on saftey or success of the construction. It's your own responsibility to maintain safety during the process. Please refer to professional IT service when you have question or meet trouble.

## 1. Build a GPU Workstation
Feel free to skip this section if you already have a GPU machine or plan to buy a pre-assembled one.

### Pick and purchase parts
In general, you need to have motherboard, CPU (including CPU fan), memory cards, power supply unit (PSU), hard drive (+SSD), case and graphics cards (GPUs). A good place to pick and compare computer parts is <a href="https://pcpartpicker.com" target="_blank">PC Part Picker</a>. The website will help you check compatibility of components and provides price comparisons from multiple providers, which is really helpful.

You can find my part list <a href="https://pcpartpicker.com/list/LbT7Fd" target="_blank">HERE</a>. The parts I bought are not completely the same as the list because, for convenience, I just bought all parts from <a href="http://www.frys.com" target="_blank">Frys</a> and choose parts depending on their availability. But at least you could get a sense of how much it costs and what parts are necessary. For my case it costs around $2.2k (May 2017) in total for a machine with two GTX 1080 GPUs, 32GB memory, 500GB SSD + 4TB hard drive with a quad-core i5 CPU and 850W power. Note that this spec is optimized for cost with strong constraint to preserve two GPUs. CPU, SSD and memory are versions that are far from the best.

### Assemble the machine
Read the instructions of motherboard, power and case *carefully* before installation. There are also plenty of videos online on how to assemble a machine, which might be helpful if you are doing it the first time.

A brief guideline on the assembling steps are as follows.
1. Install CPU on motherboard, install CPU fan, make sure the CPU fan stays solid, connect fan power cable to motherboard
2. Install memory card to motherboard
3. Connect cables to PSU, motherboard power (2 of them one for CPU, one for motherboard general, read the text on the cable, don’t misplace the PCI power cables!), harddrive power (one for HD, one for SSD), GPU power (2 cables), put PSU into the case
4. Install motherboard into the case, put the IO shield (the one for USB, ethernet etc.) before putting the motherboard
5. Connect power, reset, LED etc. jump cables to motherboard, connect case fan power cables to motherboard, connect motherboard power cables
6. Install HD and SSD, connect power cables
7. Install GPUs, connect power cables
8. Connect case cable to plug-in, start machine, enter the BIOS window to check if all HWs are detected and work normally :)

Tip:  if you find it extremely difficult to connect some cable, you are probably doing it in the wrong way!

## 2. Install Ubuntu
I assume at this step, you already have a functional machine connected to display, keyboard and mouse.

### Create a bootable USB stick on Ubuntu
Assuming you or your friend already have a computer, then you can prepare a USB stick for OS installation following this guideline: <a href="https://www.ubuntu.com/download/desktop/create-a-usb-stick-on-ubuntu" target="_blank">Create A USB Stick on Ubuntu</a> or equivalents for <a href="https://www.ubuntu.com/download/desktop/create-a-usb-stick-on-windows" target="_blank">Windows</a> and <a href="https://www.ubuntu.com/download/desktop/create-a-usb-stick-on-macos" target="_blank">macOS</a>.

The 14.04 ISO file (ubuntu-14.04.5-desktop-amd64.iso ) can be found here: http://releases.ubuntu.com/14.04/

### Install Ubuntu 14.04 LTS
Insert the disk to the machine's USB stick. Start the machine and it should automatically enter a window for Ubuntu installation. If your system has a preinstalled OS, you need to modify BIOS boot order to set USB stick as first priority. The installation process should be very fast (less than 10 minutes for my case) and simple.

## 3. Install CUDA and cuDNN
This and the following steps require Internet connection.

### Preparation

Install some useful packages in terminal:
``` bash
sudo apt-get update
sudo apt-get install \
  aptitude \
  freeglut3-dev \
  g++-4.8 \
  gcc-4.8 \
  libglu1-mesa-dev \
  libx11-dev \
  libxi-dev \
  libxmu-dev \
  nvidia-modprobe \
  python-dev \
  python-pip \
  python-virtualenv \
  vim
```


### Install CUDA

Download CUDA installation file: https://developer.nvidia.com/cuda-downloads

Choose Linux -> x86_64 -> Ubuntu -> 14.04 -> deb (local)  -> Download

Install CUDA in terminal (use the specific .deb file you've downloaded):
``` bash
cd ~/Downloads
sudo dpkg -i cuda-repo-ubuntu1404-8-0-local-ga2_8.0.61-1_amd64.deb
sudo apt-get update
sudo apt-get install cuda
```

Restart the computer to activate CUDA driver. Now your screen resolution should be automatically changed to highest resolution for the display!

### Install cuDNN

The NVIDIA CUDA® Deep Neural Network library (cuDNN) is aGPU-accelerated library of primitives for deep neural networks with optimizations for convolutions etc.

Register an (free) acount on NVIDIA website and login to download the latest cuDNN library: https://developer.nvidia.com/cudnn

Choose the specific version of cuDNN (denpending on support of your prefered deep learning framework)

Choose `Download cuDNN v5.1 (Jan 20, 2017), for CUDA 8.0` -> `cuDNN v5.1 Library for Linux`

Install cuDNN (by copying files :) in terminal:
```bash
cd ~/Downloads
tar xvf cudnn-8.0-linux-x64-v5.1.tgz
cd cuda
sudo cp lib64/* /usr/local/cuda/lib64/
sudo cp include/cudnn.h /usr/local/cuda/include/
sudo chmod a+r /usr/local/cuda/lib64/libcudnn*
```

### (Optional) Update your .bashrc

Add the following lines to your `~/.bashrc` file (you can open it by `gedit ~/.bashrc` in terminal)
```bash
export PATH=/usr/local/cuda/bin:$PATH
export MANPATH=/usr/local/cuda/man:$MANPATH
export LD_LIBRARY_PATH=/usr/local/cuda/lib64:$LD_LIBRARY_PATH
```

## 4. Install TensorFlow
Follow TensorFlow official page for installation: https://www.tensorflow.org/install/
Or install whatever deep learning frameworks that you prefer :)

For example to install TF1.1 with GPU and Python 2.7:
```bash
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.1.0-cp27-none-linux_x86_64.whl
sudo pip install --upgrade $TF_BINARY_URL
```

## 5. Others
### Mount hard drive
### Set up SSH connection
