# Template project for the STM32F4Discovery Board

This is a template repository for getting the main peripherals working on a [STM32F4Discovery](https://www.st.com/en/evaluation-tools/stm32f4discovery.html#sw-tools-scroll) board.

## Toolchain

To get all dependencies and be ready to flash the STM32F3 Board, install the following packages:

        apt install cmake libusb-dev libusb-1.0.0-dev build-essential autoconf\
         cutecom git binutils-arm-none-eabi gcc-arm-none-eabi

## Flash-Tool

The newest Flash-Tool for the STM-Boards can be found at [STLINK](https://github.com/texane/stlink). Clone it and make a debian package, which then can be installed via dpkg:

        git clone https://github.com/texane/stlink  
        cd stlink  
        make clean  
        make package  
        sudo dpkg -i build/Release/stlink-1.4.0-12-g95b6e03-amd64.deb  
        sudo ldconfig # refresh library list for st-link  

## Additional Resources

### STM32CubeF4
Download the [STM32Cube-F4](http://www.st.com/web/catalog/tools/FM147/CL1794/SC961/SS1743/PF259243#) Library and extract the Files to the ```~/opt``` Folder.

Further Documentation and the Manuals can be found here:  
* [Getting started with STM32CubeF4 firmware](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00107720.pdf)  
* [Discovery kit for STM32F407/417](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00039084.pdf)  
* [STM32F4xx HAL drivers](http://www.st.com/st-web-ui/static/active/en/resource/technical/document/user_manual/DM00105879.pdf)  
* [STM32F3 and STM32F4 Series Cortex®-M4 programming manual](http://www.st.com/web/en/resource/technical/document/programming_manual/DM00046982.pdf)  
* [STM32F405xx/07xx, STM32F415xx/17xx, STM32F42xxx and STM32F43xxx advanced ARM®-based 32-bit MCUs](http://www.st.com/web/en/resource/technical/document/reference_manual/DM00031020.pdf)  

## Credits
Thanks to Fabian Greif for his minimal example [repository](https://github.com/dergraaf/stm32f3_minimal) for the STM32F3-Discovery board.
I wish also to thank Matthew Blythe and 'mohammedari' for theier good startpoints:  
[Basic Template](https://github.com/mblythe86/stm32f3-discovery-basic-template)  
[Test Makefile](https://github.com/mohammedari/stm32f3discovery-test-c)  
[STM32CubeF4 Makefile Template Project](https://github.com/theotime/STM32CubeF4_makefile_template.git)  

