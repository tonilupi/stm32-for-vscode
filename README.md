# STM32 for VSCode

This is a supporting extension to setup STM32 projects generated from STM CubeMX. It automatically generates a makefile and starts the build process, it also adds debugging, build and flash configurations to the workspace.

It also supports using cpp files, however for this main.c has to ben manualy renamed to main.cpp for it to work.

To use the extension use the cmd/ctrl+shift+p shortcut to open the commands panel and run the Build STM project command. This will setup the project and start the building process.

This project depends on a few dependencies so make sure they are installed before using this extension.

## Prerequisites
There are a few command line tools that needs to be added to the PATH for this extension to work. On top of this the Cortex-Debug extension needs to be installed for debugging. Should any of the command line tools not be installed you will get a warning stating which one is missing. The requirements are stated below.


- [STM32 CubeMX](https://www.st.com/en/development-tools/stm32cubemx.html)
- [Cortex-Debug extension](https://github.com/Marus/cortex-debug)
- [ST-Link (Drivers and Utility)](https://www.st.com/en/development-tools/st-link-v2.html)
- [GNU Arm Embedded Toolchain](https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads)
- Make (platform dependent, [Windows](http://gnuwin32.sourceforge.net/packages/make.htm), OSX: install command line developer tools)
- OpenOCD: [Windows](https://gnutoolchains.com/arm-eabi/openocd/), [all platforms](https://xpack.github.io/openocd/install/)

## Configuring CubeMX
This extension assumes the project initialised with CubeMX and the option to create a Makefile project under Project Manager->Project->Toolchain/IDE.

Also please leave the default on Copy all used libraries into the project folder and generate separate .c and .h files for the peripherals. The advanced project structure is not supported, so please un check that box if checked.

## How to use
Use cmd/ctrl+shift+p to open the show all commands panel and issue the command: Build STM32 project. Please note that external libraries should be placed in the lib folder and source code should be place in the src and inc folders.

## Features
- Creating a makefile and building and STM32 project.
- Adding configurations for debugging, flashing and building in the workspace.
- Ability to compile it as a C++ project by adding a main.cpp file.
- Automatic configuration of intellisense.
- Detection of required tools and creating a warning.

## Disclaimer
This an extension created because I wanted a fast way to build, flash and debug STM32 on OSX in VSCode. This extension is used internally at Bureau Moeilijke Dingen for development. As this might be helpful to others I have allocated time to publish this extension. Should you find any bugs or have feature requests please open an issue on the [Github page](https://github.com/bmd-studio/stm32-for-vscode).

## Issues
### Cannot find arm-none-eabi-gcc or will not compile on OSX
Due to new access permissions on OSX sometimes when installing the extension has no access and execution rights for the arm compiler. To prevent this we advise using [xpm](https://xpack.github.io/xpm/install/) as an installer. Make sure you hae a version of [node](https://nodejs.org/en/) installed. You can then run the following command in the terminal to install the arm-none-eabi compiler: 

```$ npx xpm install --global @xpack-dev-tools/arm-none-eabi-gcc@latest```

(npx allows you to not install xpm as a global dependency and just run it).
After this the arm-non-eabi-gcc files can be found in the following folder where the text LATEST-VERSION-NUMBER should be replaced by the version number you downloaded: ~/Library/xPacks/@xpack-dev-tools/arm-none-eabi-gcc/LATEST-VERSION-NUMBER/.content/bin/arm-none-eabi-gcc

If you input this into you STM32 for VSCode configuration the compilation should work.