# Change Log

## 1.2.1
- Fixed RPC messages which were causing DAPLink flash to fail

## 1.2.0
- Updated underlying USB package and switched to libusb v1.0.27
- Stopped using workers when run in vscode-server

## 1.1.2
- Fixed empty Registers view in version 1.1.1
- Fixed breakpoint management on Windows in version 1.1.1
- Updates `programs` debug and run configuration option to accept a string with a comma-separated list of file paths

## 1.1.1
- Refactored device access to support debugging in SSH remotes and WSL
- Added support for the [Eclipse CDT Cloud Peripheral Inspector](https://github.com/eclipse-cdt-cloud/vscode-peripheral-inspector)
- Included Memory Inspector and Peripheral Inspector views by default
- Split Arm Debugger for VS Code support into [Arm Debugger extension](https://marketplace.visualstudio.com/items?itemName=Arm.arm-debugger)
- Support pre-filling DeviceName and ProcessorName from CMSIS Solution extension
- Warn user when using HID devices

## 1.0.13
- Fixed issue with checking program paths before flashing on Windows

## 1.0.12
- Fixed WebAssembly loading in VS Code Server

## 1.0.11
- Changed pack asset service to use cmsis.io
- Fixed broken documentation link
- Various dependency package updates

## 1.0.10
- Fixed broken flashing after VS Code update

## 1.0.9
- Improved flash progress display for Arm Debugger
- Fixed device vendor resolution for Arm Debugger

## 1.0.8
- Fixed paths for browser-based debug

## 1.0.6
- Ensured default tasks exist for flash and debug
- Removed default debug config labels

## 1.0.5
- Better extension tracking for skipping flashing
- Changes to build execution

## 1.0.4
- Fixed pack loading issue with run and debug

## 1.0.3
- Fixed some issues with windows paths in the embedded debugger
- Initial support for Arm Debugger flashing

## 1.0.2
- Fixed detection for NXP devices

## 1.0.1
- Added intelligent flashing to skip when firmware is up to date.
- Added device and processor picker enhancements.

## 1.0.0
- Non-preview release.
- Added option to open serial output after flash.
- Added file completion for flash tasks.

## 0.11.3
- Removed scheme from path before canonicalization.

## 0.11.2
- Added additional logging.

## 0.11.1
- No longer parse path as file.

## 0.11.0
- `Add to Watch` command added.
