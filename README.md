<p align="center">
 <img width="300px" src="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/assets/39442130/21806232-1546-4bf5-936c-5a5a34e05c76" align="center" alt="ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)" />
 <h2 align="center">ROG-Zephyrus-G14-GA401-Hackintosh(2020-2021)</h2>
 <p align="center">OpenCore Config for Asus ROG-Zephyrus-G14-GA401(2020-2021) with AMD Ryzen.</p>
  <p align="center">
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/graphs/contributors">
      <img alt="GitHub Contributors" src="https://img.shields.io/github/contributors/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh" />
    </a>
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/issues">
      <img alt="Issues" src="https://img.shields.io/github/issues/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh?color=0088ff" />
    </a>
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/pulls">
      <img alt="GitHub pull requests" src="https://img.shields.io/github/issues-pr/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh?color=0088ff" />
    </a>
  </p>
  <p align="center">
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh">View Demo</a>
    ·
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/issues">Report Bug</a>
    ·
    <a href="https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/issues">Request Feature</a>
  </p>
  <p align="center">
    <a href="README_cn.md">简体中文</a>
    ·
    <a href="README.md">English</a>
  </p>



![Screenshot](https://github.com/PIut02/ROG-Zephyrus-G14-GA401-Hackintosh/assets/39442130/11d858f8-de53-4e87-a39c-329be14903ad)

## Description

- Available version of this repository: Sonoma
- The model information has been removed, please generate and replace it yourself.
  - The machine model must be one of the following: `MacbookPro16,3`, `iMac20,1`, `iMacPro1,1`.
- OpenCore version: 0.9.7
- BIOS settings:
  - Suggest using [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) tool to increase VRAM, Go to Device Manager > AMD CBS > NBIO Common Options > GFX Configuration and adjust the `IGPU Configuration` to `UMA_SPECIFIED`. Then, set the `UMA Frame buffer Size` to at least 1G and recommend 2G.
  - To prevent installation freezing, you can either enable the `Above 4G Decoding` or add the `ncpi=0x2000` to the boot-args.
  Use [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) tool to enable `Above 4G decoding` in the [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) tool by going to Device Manager > PCI Subsystem Settings.
  - Turn off `Secure Boot` and `Fast Boot`
- This repository does not include `NootedRed`, please go to [NootedRed](https://github.com/ChefKissInc/NootedRed) to download and add it yourself.
- Updating EFI may require clearing NVRAM to take full effect.

> [!Warning]
> When installing or updating the system, be sure to disable the `NootedRed` driver in `config.plist`, otherwise the installation process will get stuck at the progress bar and cannot be installed normally.
>
> `BFixup.kext` must be loaded before `NootedRed`, meaning the loading order should be adjusted to Lilu > BFixup > NootedRed.

## Configuration

| Component            | Model (2020/2021)         |
| :------------------- | :------------------------ |
| CPU                  | AMD Ryzen 7 4800HS/5800HS |
| Integrated GPU       | AMD Radeon Vega 8         |
| Dedicated GPU        | NVIDIA                    |
| Network/Bluetooth    | Intel AX200               |
| SSD                  | WD SN570 SSD              |
| Keyboard/Trackpad    | IC2 HID                   |
| Audio/Headphone jack | ALC289/285                |

## Overview

### Working

- CPU / IGPU
  - Use [AMDPowerGadget](https://github.com/trulyspinach/SMCAMDProcessor) for CPU power management and temperature monitoring.
  - Use [RadeonSensor](https://github.com/NootInc/RadeonSensor) to monitor GPU temperature.
- WIFI/Bluetooth
- Apple ID & iMessages & iCloud
- Interrupt mode touchpad and keyboard input
- 1440p 60hz HiDPI display
- Built-in speakers and 3.5mm headphone audio output / Built-in microphone
- All USB ports / NVME SSD
- Brightness, sound shortcut keys, and keyboard backlight control
  - Use [ROG-HID](https://github.com/black-dragon74/ROG-HID) to control, and to use this software, you need to turn off `SIP`.
- S3 Sleep
  - Use [UMAF](https://github.com/DavidS95/Smokeless_UMAF/) tool to enable `S3 Sleep`
  - Might need to enter the following commands in the terminal:
    ```
    sudo pmset autopoweroff 0
    sudo pmset powernap 0
    sudo pmset standby 0
    sudo pmset proximitywake 0
    sudo pmset tcpkeepalive 0
    ```

### Not working and current issues

- HDMI audio output / 3.5mm headphone input
- NVIDIA graphics card
- Some Fn shortcut keys
- After using Windows and restarting to macOS, there is no sound from the headphones. A forced shutdown and reboot will make it work normally again.
- VCN (video/image hardware encoding/decoding) still has some problems, can be used but not guaranteed, turned off by default, to turn on, please add `-ChefKissInternal` to `boot-args`. For details, please go to the NootedRed page to see the latest progress.

### Tips

- You can control the temperature within a suitable range by turning off `CPS (core performance boost)`, but this will lose some performance. You can use the UMAF tool to turn off `CPS` in the BIOS, but it will affect the performance of other systems such as Windows, so it is recommended to use AMD Power Gadget to turn it off after each boot into the system, at least for now.
- The `BFixup.kext` downgrades the OpenGL version to prevent system freezing, allowing certain applications like Chrome to work normally. However, it may also cause some applications to not work. If you encounter any problems, please disable the `BFixup.kext`.

## Know Your EFI

### ACPI

SSDT | Function
:---------|:---------
SSDT-PLUG-ALT | Used for MacOS to recognize CPU, must-have
SSDT-EC | Fakes an EC for MacOS, must-have
SSDT-HPET | Solves IRQ conflicts, must-have
SSDT-USBX | USB power management, must-have
SSDT-XOSI | ACPI function of MAC and WIN, dual systems must-have.
SSDT-ALS0 | Provided by NootedRed, used for screen brightness adjustment
SSDT-PNLF | Provided by NootedRed, used for screen brightness adjustment
SSDT-NoHybGfx | Turn off the discrete graphics card
SSDT-RMNE | Used in combination with the built-in Ethernet card in NullEthernet.kext to implement Apple ID login

### Kexts

Kext | Function
:---------|:---------
AirportItlwm | Intel wireless card driver, note that different systems have different kexts
AMDRyzenCPUPowerManagement | AMD CPU power management
AppleALC | Audio driver
AppleMCEReporterDisabler | Turn off AppleIntelMCEReporter to avoid errors on AMD CPU devices
BFixup | Downgrading the OpenGL version.
BlueToolFixup | Bluetooth repair patch
BrightnessKeys | Brightness adjustment keys
CPUTscSync | To mitigate certain issues, it is advisable to synchronize the CPU's TSC (Time Stamp Counter).
ECEnabler | Battery reading
FeatureUnlock | Unlock features on unsupported models
HoRNDIS | Support Android device USB shared network
IntelBTPatcher | Bluetooth driver
IntelBluetoothFirmware | Bluetooth driver
Lilu | Essential
NullEthernet | Allows devices without Ethernet ports to log in to iCloud on MacOS
NVMeFix | NVMe hard drive power management
RestrictEvents | [Lilu](https://github.com/acidanthera/Lilu) Kernel extension for blocking unwanted processes causing compatibility issues on different hardware and unlocking the support for certain features restricted to other hardware
RadeonSensor | Get AMD graphics card temperature information
SMCAMDProcessor | Subsidiary of AMDRyzenCPUPowerManagement
SMCProcessorAMD | Enable the system to read the temperature and power consumption of the CPU
SMCBatteryManager | Battery management
SMCLightSensor | For ambient light sensors on laptops
SMCRadeonGPU.kext | Get AMD graphics card temperature information
USBToolBox | USB Map
USBMap | USB Map
VirtualSMC | Essential
VoodooI2C | Touchpad or touch screen driver
VoodooI2CHID | Touchpad or touch screen driver

## Credit

- [Apple](https://www.apple.com) for macOS.
- [ChefKissInc](https://github.com/ChefKissInc/) for [NootedRed](https://github.com/ChefKissInc/NootedRed) and VoodooI2C, their hard work has made this project possible.
- [zabdottler](https://github.com/zabdottler/Lenovo-Yoga-16S-hackintosh), [AlphaNecron](https://github.com/AlphaNecron/Zephyrus-G14-GA401QH-EFI), [b00t0x](https://github.com/b00t0x/ROG-Zephyrus-G14-GA402-Hackintosh) for let me to know this work is possible.
- [DavidS95](https://github.com/DavidS95/) for [UMAF](https://github.com/DavidS95/Smokeless_UMAF/), allow me to conveniently modify the hidden BIOS settings.