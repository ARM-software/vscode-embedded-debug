# Arm Embedded Debugger

## Overview

This extension allows you to flash, run and debug projects on Arm Cortex-M based microcontrollers, development boards and debug probes implementing the Microsoft Debug Adapter Protocol (DAP). It can be installed individually or together with other extensions contained in the **Keil Studio Pack** available for Visual Studio Code Desktop and Visual Studio Code for the Web. Check the extension pack Readme first if you want to install the extensions using the pack.

The **Arm Embedded Debugger** extension can work in combination with the **Arm Device Manager** (Identifier: `arm.device-manager`) and **Arm CMSIS csolution** (Identifier: `arm.cmsis-csolution`) extensions.

This Readme explains how to run a project on a device and how to start a debug session.

## Submit feedback

To submit feedback, please [create an issue](https://github.com/Arm-Software/vscode-embedded-debug/issues/new/choose).

## Run your project on your device

### Configure a task

You must first configure a flash task to be able to run a project on your device. The task transfers the binary into the appropriate memory locations on the device flash memory.

There are two flash tasks available:

- **embedded-debug.daplink-flash**: Use this task for DAPLink devices. The DAPLink firmware takes care of the flash download.
- **embedded-debug.flash:Flash Device**: Use this task for other CMSIS-DAP (such as Nu-Link2 and ULINKplus) and ST-Link devices. Flash algorithms contained in the CMSIS-Packs used in your project are deployed in the background to do the flash download.

Procedure:

1. In Visual Studio Code, go to **Terminal** > **Configure Tasks...**.

1. In the drop-down list that opens at the top of the window, select **embedded-debug.daplink-flash:Flash Device (DAPLink)** or **embedded-debug.flash:Flash Device**.

    A `tasks.json` file opens with some default configuration.

    Default configuration for **embedded-debug.daplink-flash:Flash Device (DAPLink)**:

    ```
            {
              "type": "embedded-debug.daplink-flash",
              "serialNumber": "${command:device-manager.getSerialNumber}",
              "program": "${command:embedded-debug.getBinaryFile}",
              "problemMatcher": [],
              "label": "embedded-debug.daplink-flash: Flash Device (DAPLink)"
            }
    ```

    Default configuration for **embedded-debug.flash:Flash Device**:

    ```
               {
                 "type": "embedded-debug.flash",
                 "serialNumber": "${command:device-manager.getSerialNumber}",
                 "program": "${command:embedded-debug.getApplicationFile}",
                 "cmsisPack": "${command:device-manager.getDevicePack}",
                 "problemMatcher": [],
                 "label": "embedded-debug.flash: Flash Device"
               }
    ```

1. You can override or extend the default configuration options as required. See the [Flash configuration options for DAPLink devices](#flash-configuration-options-for-daplink-devices) and for [other devices](#flash-configuration-options-for-other-devices) for more details.

    For example:

    ```
               {
                 "type": "embedded-debug.flash",
                 "serialNumber": "${command:device-manager.getSerialNumber}",
                 "program": "${command:embedded-debug.getApplicationFile}",
                 "cmsisPack": ""${command:device-manager.getDevicePack}",
                 "label": "embedded-debug.flash: Flash Device",
                 "processorName": "cm4"
               }
    ```

1. Save the `tasks.json` file.

### Flash configuration options for DAPLink devices

The task options below are the ones provided by the extension. Other Visual Studio Code options are also available. Use the **Trigger Suggestions** command (**Ctrl+Space**) to see what is available and check the [Visual Studio Code documentation on tasks](https://code.visualstudio.com/docs/editor/tasks), as well as the [Schema for tasks.json](https://code.visualstudio.com/docs/editor/tasks-appendix) page.

|    Configuration option     |                                      Description                                      |
|-----------------------------|---------------------------------------------------------------------------------------|
| `"program"`                 | Path(s) (file or url) to the project(s) to use.                                       |
| `"serialNumber"`            | Serial number of the connected USB device to use.                                     |


### Flash configuration options for other devices

The task options below are the ones provided by the extension. Other Visual Studio Code options are also available. Use the **Trigger Suggestions** command (**Ctrl+Space**) to see what is available and check the [Visual Studio Code documentation on tasks](https://code.visualstudio.com/docs/editor/tasks), as well as the [Schema for tasks.json](https://code.visualstudio.com/docs/editor/tasks-appendix) page.

|    Configuration option     |                                      Description                                      |
|-----------------------------|---------------------------------------------------------------------------------------|
| `"cmsisPack"`               | Path (file or url) to a DFP (Device Family Pack) CMSIS pack for your device.          |
| `"connectMode"`             | Connection mode. Possible values: auto (debugger decides), haltOnConnect (halts for any reset before running), underReset (holds external NRST line asserted), preReset (pre-reset using NRST), running (connects to running target without altering state). Default: auto.|
| `"dbgconf"`                 | Path (file or url) to a dbgconf file.                                                 |
| `"deviceName"`              | CMSIS pack device name.                                                               |
| `"eraseMode"`               | Type of flash erase to use. Possible values: sectors (erase only sectors to be programmed), full (erase full chip), none (skip flash erase). Default: sectors.|
| `"flm"` or `"flms"`         | Path(s) (file or url) to an flm file or flm files.                                    |
| `"pdsc"`                    | Path (file or url) to a pdsc file.                                                    |
| `"processorName"`           | CMSIS pack processor name for multi-core devices.                                     |
| `"program"` or `"programs"` | Path(s) (file or url) to the project(s) to use.                                       |
| `"programFlash"`            | Program code into flash. Default: true.                                               |
| `"programMode"`             | Mode to program an application to a target. Default: auto                             |
| `"resetAfterConnect"`       | Resets the device after having acquired control of the CPU. Default: true.            |
| `"resetMode"`               | Type of reset to use. Possible values: auto (debugger decides), system (use ResetSystem sequence), hardware (use ResetHardware sequence), processor (use ResetProcessor sequence). Default: auto.|
| `"resetRun"`                | Issue a hardware reset at end of flash download. Default: true.                       |
| `"sdf"`                     | Path (file or url) to an sdf file.                                                    |
| `"serialNumber"`            | Serial number of the connected USB device to use.                                     |
| `"targetAddress"`           | Synonymous with serialNumber.                                                         |
| `"vendorName"`              | CMSIS pack vendor name.                                                               |
| `"verifyFlash"`             | Verify the contents downloaded to flash. Default: true.                               |

### Run your project

Execute the binary on your device.

Procedure:

1. Check that your device is connected to your computer.

1. Select **Terminal** > **Run Task...** to run the project on your device.

1. In the drop-down list that opens at the top of the window, select the **embedded-debug.daplink-flash:Flash Device (DAPLink)** task or the **embedded-debug.flash:Flash Device** task.

1. In the drop-down list that opens at the top of the window, select your device.

1. Check the **Terminal** tab to verify that the project has run correctly.

## Debug your project

### Add configuration

As for running a project, you must first add some configuration to be able to do debugging.

Procedure:

1. In Visual Studio Code, go to **Run** > **Add Configuration...**.

    A `launch.json` file opens.

1. Select **Arm: Embedded Debug** in the IntelliSense suggestions widget that opens.

    Some default configuration is added.

```
         {
            "configurations": [
                {
                    "name": "Embedded Debug",
                    "type": "embedded-debug",
                    "request": "launch",
                    "serialNumber": "${command:device-manager.getSerialNumber}",
                    "program": "${command:embedded-debug.getApplicationFile}",
                    "cmsisPack": "${command:device-manager.getDevicePack}",
                    "debugFrom": "main"
                }
            ]
         }
```

1. You can override or extend the default configuration options as required. See [Debug configuration options](#debug-configurattion-options) for more details.

    For example:

```
         {
            "configurations": [
                {
                    "name": "FRDM-K32L3A6 (CM4)",
                    "type": "embedded-debug",
                    "request": "launch",
                    "serialNumber": "${command:device-manager.getSerialNumber}",
                    "deviceName": "K32L3A60VPJ1A",
                    "processorName": "cm4",
                    "program": "${command:embedded-debug.getApplicationFile}",
                    "cmsisPack": "${command:device-manager.getDevicePack}",
                    "debugFrom": "main"
                }
            ]
         }
```

1. Save the `launch.json` file.

### Debug configuration options

The task options below are the ones provided by the extension. Other Visual Studio Code options are also available. Use the **Trigger Suggestions** command (**Ctrl+Space**) to see what is available and check the [Visual Studio Code documentation on tasks](https://code.visualstudio.com/docs/editor/tasks).

|    Configuration option     |                                      Description                                      |
|-----------------------------|---------------------------------------------------------------------------------------|
| `"cmsisPack"`               | Path (file or url) to a DFP (Device Family Pack) CMSIS pack for your device.          |
| `"connectMode"`             | Connection mode. Possible values: auto (debugger decides), haltOnConnect (halts for any reset before running), underReset (holds external NRST line asserted), preReset (pre-reset using NRST), running (connects to running target without altering state). Default: auto. |
| `"dbgconf"`                 | Path (file or url) to a dbgconf file.                                                 |
| `"debugFrom"`               | The symbol the debugger will run to before debugging. Default: `"main"`.              |
| `"deviceName"`              | CMSIS pack device name.                                                               |
| `"pathMapping"`             | A mapping of remote paths to local paths to resolve source files.                     |
| `"pdsc"`                    | Path (file or url) to a pdsc file.                                                    |
| `"processorName"`           | CMSIS pack processor name for multi-core devices.                                     |
| `"program"` or `"programs"` | Path(s) (file or url) to the project(s) to use.                                       |
| `"programNames"`            | Filename or filenames of the projects to be used. Only used for labelling.            |
| `"resetAfterConnect"`       | Resets the device after having acquired control of the CPU. Default: true.            |
| `"resetMode"`               | Type of reset to use. Possible values: auto (debugger decides), system (use ResetSystem sequence), hardware (use ResetHardware sequence), processor (use ResetProcessor sequence). Default: auto. |
| `"sdf"`                     | Path (file or url) to an sdf file.                                                    |
| `"serialNumber"`            | Serial number of the connected USB device to use.                                     |
| `"svd"` or `"svdPath"`      | Path (file or url) to an svd file.                                                    |
| `"targetAddress"`           | Synonymous with serialNumber.                                                         |
| `"vendorName"`              | CMSIS pack vendor name.                                                               |
| `"verifyApplication"`       | Verify application against target memory for each application load operation in debug session. Default: true.|

### Debug

Procedure:

1. Check that your device is connected to your computer.

1. Select **Run** > **Start Debugging**.

1. If you are using a device with multiple cores, you must select the appropriate processor for your project in the **Select a processor** drop-down list that displays at the top of the window.

   The **Run and Debug** view displays and the debug session starts. The debugger stops at the function "main" of your project.

1. Check the **Debug Console** to see the debugging output.

Look at the [Visual Studio Code documentation](https://code.visualstudio.com/docs/editor/debugging#_debug-actions) to learn more about the debugging features available in Visual Studio Code.

### Supported debug probes

#### WebUSB-enabled CMSIS-DAP debug probes

The extension supports debug probes that implement the CMSIS-DAP protocol. See the [CMSIS-DAP](https://arm-software.github.io/CMSIS_5/DAP/html/index.html) documentation for general information.

Such implementations are for example:

- The DAPLink implementation: see the [ARMmbed/DAPLink](https://github.com/ARMmbed/DAPLink) repository.

- The Nu-Link2 implementation: see the [Nuvoton](https://github.com/OpenNuvoton/Nuvoton_Tools#comparison-of-nulink2fwbin-and-nulink2_daplinkbin) repository.

- The ULINKplus (firmware version 2) implementation: see the [Keil MDK](https://www2.keil.com/mdk5/ulink/ulinkplus) documentation.

#### ST-LINK debug probes

The extension supports ST-LINK/V2 probes and later, and the ST-LINK firmware available for these probes.

The recommended debug implementation versions of the ST-LINK firmware are:

- For ST-LINK/V2 and ST-LINK/V2-1 probes: J36 and later.
- For STLINK-V3 probes: J6 and later.

See "Firmware naming rules" in [Overview of ST-LINK derivatives](https://www.st.com/resource/en/technical_note/tn1235-overview-of-stlink-derivatives-stmicroelectronics.pdf) for more details on naming conventions.

### Known limitations

* Support for the DWARF debugging standard is limited to version 4. Please make sure that your application is built with the appropriate settings.
* Variables and registers are read-only.
* Stack trace is limited if the debugger is halted in assembler source files.
* Watches are not supported.
