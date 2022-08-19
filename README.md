# Arm Embedded Debugger

## Overview

This extension allows you to do flashing and debugging on Arm Cortex-M based microcontrollers, development boards and debug probes implementing the Microsoft Debug Adapter Protocol (DAP).

## Useful resources

The **Arm Embedded Debugger** extension works in combination with the **Arm Device Manager** (Identifier: `arm.device-manager`) and **Arm CMSIS csolution** (Identifier: `arm.cmsis-csolution`) extensions to flash csolution projects to a device and do debugging.

## Submit feedback

To submit feedback, please [create an issue](https://github.com/ARM-software/vscode-embedded-debug/issues/new/choose).

## Flash your project to your device

### Configure a task

You must first configure a task to be able to flash a project to your device.

Procedure:

1. In Visual Studio Code, go to **Terminal** > **Configure Default Built Task...**.

1. In the drop-down list that opens at the top of the window, select **embedded-debug.flash:Flash Device**.

    A `tasks.json` file opens with some default configuration.


            ``{
                "type": "embedded-debug.flash",
                "serialNumber": "${command:device-manager.getSerialNumber}",
                "program": "${command:embedded-debug.getBinaryFile}",
                "cmsisPack": "<path or URL of CMSIS Pack for your device>",
                "problemMatcher": [],
                "label": "embedded-debug.flash: Flash Device",
                "group": {
                    "kind": "build",
                    "isDefault": true
                  }
               }``

1. Replace the default configuration by your own configuration. See [Flash configuration options](#flash-configuration-options) for more details.

    For example:

                ``{
                    "type": "embedded-debug.flash",
                    "serialNumber": "${command:device-manager.getSerialNumber}",
                    "program": "${command:embedded-debug.getBinaryFile}",
                    "cmsisPack": "https://mcuxpresso.nxp.com/cmsis_pack/repo/NXP.K32L3A60_DFP.13.1.0.pack",
                    "label": "embedded-debug.flash: Flash Device",
                    "processorName": "cm4",
                    "group": {
                        "kind": "build",
                        "isDefault": true
                      }
                  }``

1. Save the `tasks.json` file.

### Flash configuration options

|    Configuration option     |                                      Description                                      |
|-----------------------------|---------------------------------------------------------------------------------------|
| `"serialNumber"`            | Serial number of the connected USB device to use.                                     |
| `"program"` or `"programs"` | Path(s) (file or url) to the project(s) to use.                                       |
| `"cmsisPack"`               | Path (file or url) to a DFP (Device Family Pack) CMSIS pack for your device.          |
| `"pdsc"`                    | Path (file or url) to a pdsc file.                                                    |
| `"vendorName"`              | CMSIS pack vendor name.                                                               |
| `"deviceName"`              | CMSIS pack device name.                                                               |
| `"processorName"`           | CMSIS pack processor name for multi-core devices.                                     |
| `"sdf"`                     | Path (file or url) to an sdf file.                                                    |
| `"dbgconf"`                 | Path (file or url) to a dbgconf file.                                                 |
| `"resetAfterConnect"`       | Resets the device after having acquired control of the CPU. Default: true.            |
| `"flm"` or `"flms"`         | Path(s) (file or url) to an flm file or flm files.                                    |
| `"programFlash"`            | Program code into flash. Default: true.                                               |
| `"verifyFlash"`             | Verify the contents downloaded to flash. Default: true.                               |
| `"resetRun"`                | Issue a hardware reset at end of flash download. Default: true.                       |
| `"connectMode"`             | Connection mode. Possible values: haltOnConnect (halts for any reset before running), underReset (holds external NRST line asserted), preReset (pre-reset using NRST), running (connects to running target without altering state). Default: haltOnConnect.|
| `"resetMode"`               | Type of reset to use. Possible values: auto (debugger decides), system (use ResetSystem sequence), hardware (use ResetHardware sequence), processor (use ResetProcessor sequence). Default: auto.|
| `"eraseMode"`               | Type of flash erase to use. Possible values: sectors (erase only sectors to be programmed), full (erase full chip), none (skip flash erase). Default: sectors.|

### Flash your project

Procedure:

1. Check that your device is connected to your computer.

1. Select **Terminal** > **Run Build Task...** to flash the project to your device.

1. Check the **Terminal** tab to verify that the project has been flashed correctly.

## Debug your project

### Add configuration

As for flashing, you must first add some configuration to be able to do debugging.

Procedure:

1. In Visual Studio Code, go to **Run** > **Add Configuration...**.

1. In the drop-down list that opens at the top of the window, select **Arm Embedded Debug**.

    A `launch.json` file opens with some default configuration.

        ``{
            // Use IntelliSense to learn about possible attributes.
            // Hover to view descriptions of existing attributes.
            // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
            "version": "0.2.0",
            "configurations": [
                {
                    "name": "Arm Embedded Debug",
                    "type": "embedded-debug",
                    "request": "launch",
                    "serialNumber": "${command:device-manager.getSerialNumber}",
                    "program": "${command:embedded-debug.getBinaryFile}",
                    "cmsisPack": "<path or URL of CMSIS Pack for your device>"
                }
            ]
        }``

1. Replace the default configuration by your own configuration. See [Debug configuration options](#debug-configurattion-options) for more details.

    For example:

        ``{
        // Use IntelliSense to learn about possible attributes.
        // Hover to view descriptions of existing attributes.
        // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
        "version": "0.2.0",
        "configurations": [
            {
                "name": "FRDM-K32L3A6 (CM0P)",
                "type": "embedded-debug",
                "request": "launch",
                "serialNumber": "${command:device-manager.getSerialNumber}",
                "deviceName": "K32L3A60VPJ1A",
                "processorName": "cm4",
                "program": "${command:embedded-debug.getBinaryFile}",
                "cmsisPack": "https://mcuxpresso.nxp.com/cmsis_pack/repo/NXP.K32L3A60_DFP.13.1.0.pack"
            }
        ]
    }``

1. Save the `launch.json` file.

### Debug configuration options

|    Configuration option     |                                      Description                                      |
|-----------------------------|---------------------------------------------------------------------------------------|
| `"serialNumber"`            | Serial number of the connected USB device to use.                                     |
| `"program"` or `"programs"` | Path(s) (file or url) to the project(s) to use.                                       |
| `"cmsisPack"`               | Path (file or url) to a DFP (Device Family Pack) CMSIS pack for your device.          |
| `"pdsc"`                    | Path (file or url) to a pdsc file.                                                    |
| `"vendorName"`              | CMSIS pack vendor name.                                                               |
| `"deviceName"`              | CMSIS pack device name.                                                               |
| `"processorName"`           | CMSIS pack processor name for multi-core devices.                                     |
| `"sdf"`                     | Path (file or url) to an sdf file.                                                    |
| `"dbgconf"`                 | Path (file or url) to a dbgconf file.                                                 |
| `"resetAfterConnect"`       | Resets the device after having acquired control of the CPU. Default: true.            |
| `"svd"` or `"svdPath"`      | Path (file or url) to an svd file.                                                    |
| `"debugFrom"`               | The symbol the debugger will run to before debugging. Default: `"main"`.              |
| `"programNames"`            | Filename(s) of the programs to be used. Only used for labelling.                      |
| `"verifyApplication"`       | Verify application against target memory for each application load operation in debug session. Default: true.|
| `"connectMode"`             | Connection mode. Possible values: haltOnConnect (halts for any reset before running), underReset (holds external NRST line asserted), preReset (pre-reset using NRST), running (connects to running target without altering state). Default: haltOnConnect. |
| `"resetMode"`               | Type of reset to use. Possible values: auto (debugger decides), system (use ResetSystem sequence), hardware (use ResetHardware sequence), processor (use ResetProcessor sequence). Default: auto. |
| `"pathSubstitutions"`       | Path substitutions to use. Example: "pathSubstitutions": [{"find": "the string to find", "replace": "the string to replace"}]|

### Debug

Procedure:

1. Check that your device is connected to your computer.

1. Select **Run** > **Start Debugging**.

   The **Run and Debug** view displays and the debug session starts. The debugger stops at the function "main" of your project.

1. Check the **Debug Console** to see the debugging output.

Look at the [Visual Studio Code documentation](https://code.visualstudio.com/docs/editor/debugging#_debug-actions) to learn more about the debugging features available in Visual Studio Code.

### Known limitations

* Support for the DWARF debugging standard limited to version 4. Please make sure that your application is built with the appropriate settings.
* Variables and registers are read-only.
* Stack trace limited if the debugger is halted in assembler source files.
* Watches are not supported.
