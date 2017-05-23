# DIY-Deep-Learning-Workstation
Build a deep learning workstation from scratch from hardware to software.

### Contents
1. [Build a GPU Workstation](#1-build-a-gpu-workstation)
2. [Install Ubuntu](#2-install-ubuntu)
3. [Install CUDA and cuDNN](#3-install-cuda-and-cudnn)
4. [Install TensorFlow](#4-install-tensorflow)
5. [Others](#5-others)

Disclaimer: This document records my own experience and lessons learnt in building a workstation for deep learning. However, there is no gurantee on saftey or success of the construction. It's your own responsibility to maintain safety during the process. Please refer to professional IT service when you have question or meet trouble.

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

### Install Ubuntu 16.04 LTS
Insert the disk to the machine's USB stick. Start the machine and it should automatically enter a window for Ubuntu installation. If your system has a preinstalled OS, you need to modify BIOS boot order to set USB stick as first priority. The installation process should be very fast (less than 10 minutes for my case) and simple.

## 3. Install CUDA and cuDNN
This step will require Internet connection.

###Preparation
``` bash
sudo apt-get install aptitude
sudo apt-get install \
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

## 4. Install TensorFlow
Follow TensorFlow official page for installation: https://www.tensorflow.org/install/
Or install whatever deep learning frameworks that you prefer :)

What I did to install TF1.1 with GPU and Python 3.5 was as follows:
```bash
export TF_BINARY_URL=https://storage.googleapis.com/tensorflow/linux/gpu/tensorflow_gpu-1.1.0-cp35-cp35m-linux_x86_64.whl
sudo pip install --upgrade $TF_BINARY_URL
```

## 5. Others
### Mount hard drive
### Set up SSH connection
