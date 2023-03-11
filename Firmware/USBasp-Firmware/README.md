# WCID compliant, HID UART support

This USBasp firmware is based on a [fork by Ralph Doncaster](https://github.com/nerdralph/usbasp). Original fork readme can be found at README_nerdralph.md.

## Features

- From version 1.07 a default SCK clock of 1.5Mhz and automatic SCK slowing if target does not respond. PORTD is left as input, so this firmware also works with [USBISP modules](https://www.sciencetronics.com/greenphotons/?p=938). ( nerdralph )

- From version 1.08 the firmware is [WCID](https://github.com/pbatard/libwdi/wiki/WCID-Devices) compliant, meaning it should work on Windows without any driver or .inf install.

- From version 1.09 a ( reliable at 9600 Baud, with 120ms - 160ms intervals for higher speeds see note at UART HID protocol ) UART HID implementation is added for debugging purposes. USBasp will appear as a composite device with a WINUSB interface and a HID interface.

- From version 1.10 USBasp WCID switch to Microsoft OS 2.0 Descriptors. It seems that it play better with USB 3.0 ports.

> Note: A prebuilt hex file for the ATmega8 (usbasp.atmega8.2022-07-16.hex) and one for the ATmega88 (usbasp.atmega88.2022-07-16.hex) are in the USBasp-Firmware directory. Built with [MSYS2](https://www.msys2.org/) and [avr8-gnu-toolchain (3.6.2.17778)](https://www.microchip.com/en-us/tools-resources/develop/microchip-studio/gcc-compilers) from Microchip, on a Windows 10 box.


### Visit the original repo [dioannidis/usbasp](https://github.com/dioannidis/usbasp) for HID UART use and original content
