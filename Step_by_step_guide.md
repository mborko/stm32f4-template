# A step by step guide for the STM32F4-Template

## Introduction

The following document describes every step necessary to use the [STM32F4Discovery board](https://www.st.com/en/evaluation-tools/stm32f4discovery.html#sw-tools-scroll) with the template, which is provided in this GitHub repository.

This tutorial is limited to a Linux distribution (in our case [Ubuntu](https://ubuntu.com/)), so we are asking you to use Linux or a virtual instance of Linux.

#### Alternatives

If you don't wish to use the following templates, it is possible to use [STM Workbench](https://www.st.com/en/evaluation-tools/stm32f4discovery.html#sw-tools-scroll) as an alternative.

## "The guide"

### Step 1: Clone the repository

It's highly advised to use a directory, which is dedicated to repositories. One can create a directory with the `mkdir` command.

To clone the repository use the command `git clone https://github.com/mborko/stm32f4-template` after you've navigated to your created directory

Your terminal should look like this:

![alt text](https://i.gyazo.com/6a8e503540638f0e0a0c45e4f69d3085.png "terminal")

### Step 2: Download all necessary packages

To install all needed dependencies, simply run the following command:

```sh
apt install cmake libusb-dev libusb-1.0.0-dev build-essential autoconf\
     cutecom git binutils-arm-none-eabi gcc-arm-none-eabi
```

If an interface appears where you're asked if you want to restart relevant services, press *Yes*.

### Step 3: Install the STM32CubeF4 Library

#### Step 3.1 Create the ~/opt directory

To complete the following steps you need to have a *~/opt* directory. If the directory is missing just create it with the command `mkdir`like in a previous step.

#### Step 3.2 STM32CubeF4

Download the .zip archive directly form the [website](https://www.st.com/en/embedded-software/stm32cubef4.html#). 

![alt text](https://i.gyazo.com/1e8f3ba671040f60ab8f4cee1446c989.png "The Download")

Before you download the file you will be prompted to  enter some of your personal information. If you don't wish to do this, one can just enter their email address.

![img](https://i.gyazo.com/6d3343f34a63589a9976e51b6ec71aa8.png "The download prompt")

Now extract the contents of the zip into the *~/opt*-directory.

![Extract](https://i.imgur.com/bW57UEX.gif)

The last part of this step is to change the owner of the directory to avoid complications. This is done with the following command `chown -R username filename`.

![img](https://i.gyazo.com/b62af3522361138ea991102377fb3a16.png)

### Step 4: Install the flash-tool

The last tool you need is the flashing tool. Just enter the sequence of commands shown below into the console. Since a repository is being cloned, it's highly advised to change back to the directory dedicated for the repositories.

```shell
  git clone https://github.com/texane/stlink  
  cd stlink  
  make clean  
  make package  
  sudo dpkg -i build/Release/stlink-*-amd64.deb  
  sudo ldconfig # refresh library list for st-link  
```

### Step 5: Change Makefile

To avoid complications, you have to change the makefile, which is located in the STM32F4 template. Just open the Makefile and adjust the version. The Makefile states that we have version 21.0: this needs to be rewritten to 24.0.

![change Makefile](https://i.imgur.com/TrIyqRw.gif)

### Step 6: Test

To test if everything works, you can execute the command `make`. The output at first execution is something like this:

![Output](https://i.gyazo.com/30fb943113c6e4506b1f288ef14d2f36.png)

### (optional) Step 7: Set up Shared Folders in VMWare

If you're running a virtual machine and would prefer to use the C IDE outside of the abstraction layer, you can set up a Shared Folder, which is a folder that is present on both host and guest and can be used to transfer files between both systems.

In the Library, right click on your VM and open the Settings. 

![Shared_Folders_1](https://i.imgur.com/jRBMfXh.png)



Once there (as seen below),

- head to the *Options* tab,
- select the *Shared Folders* entry,
- enable folder sharing if it isn't enabled,
- and press the *Add...* button.

![Shared_Folders_2](https://i.imgur.com/YVhI5sY.png)



Now, a wizard should open. Click *Next*. Choose the path to the folder you want to share between host and guest and enter a name of your choosing if the automatically generated one doesn't fit your liking.

![Shared_Folders_3](https://i.imgur.com/IXs2YRY.png)



You can mark the folder as read-only to prevent the guest system from making changes to the folder contents or delete them.

![Shared_Folders_4](https://i.imgur.com/HnFkQYT.png)



The folder should now be ready for use between both systems.

## Makefile parameter

* `clean`: The previous compiled program is removed.
* `flash`: The compiled program is flashed on the microcontroller.
* `PROJ=`: Path to the project to be compiled.
