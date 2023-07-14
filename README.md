# Arm Embedded Debugger

## Overview

The complete [documentation](https://developer.arm.com/documentation/108029/latest/Extension-packs-and-extensions) for **Arm Embedded Debugger** and the other Keil Studio extensions is available on Arm Developer.

The **Arm Embedded Debugger** extension allows you to run and debug projects on Arm Cortex-M based microcontrollers, development boards and debug probes implementing the Microsoft Debug Adapter Protocol (DAP). It can be installed individually or together with other extensions contained in the packs available for Visual Studio Code Desktop and Visual Studio Code for the Web. 

We recommend installing the **Keil Studio Pack** for Visual Studio Code Desktop to quickly set up your environment and start working with an example.

The **Arm Embedded Debugger** extension can work in combination with the **Arm Device Manager** (Identifier: `arm.device-manager`) and **Arm CMSIS csolution** (Identifier: `arm.cmsis-csolution`) extensions.

## Intended use cases for the extensions

- **Embedded and IoT software development using CMSIS-Packs and csolution projects**: The "Common Microcontroller Software Interface Standard" (CMSIS) provides driver, peripheral and middleware support for thousands of MCUs and hundreds of development boards. Using the csolution project format, you can incorporate any CMSIS-Pack based device, board, and software component into your application. For more information about supported hardware for CMSIS projects, go to the [Boards](https://www.keil.arm.com/boards/) and [Devices](https://www.keil.arm.com/devices/) pages on keil.arm.com. For information about CMSIS-Packs, go to [open-cmsis-pack.org](https://www.open-cmsis-pack.org/index.html).

- **Enhancement of a pre-existing Visual Studio Code embedded software development workflow**: USB device management and embedded debug can be adapted to other project formats (for example CMake) and toolchains without additional overhead. This use case requires familiarity with Visual Studio Code to configure tasks. See the individual extensions for more details.

## Install the extension

1. In Visual Studio Code, go to the **Extensions** view.

1. Search for **Arm Embedded Debugger**.

1. Click the **Install** button for the extension.

    Visual Studio Code installs the extension. It is now available in the **Extensions** view.

## Submit feedback

To submit feedback, please [open a bug report or a feature request](https://github.com/Arm-Software/vscode-embedded-debug/issues/new/choose).