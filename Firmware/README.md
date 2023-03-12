# How to Flash the OpenEVSE Firmware (in Windows with a USBasp)

- Download Zadig http://zadig.akeo.ie/
- Plug in your USBasp
- Run Zadig
  - USBasp should be detected and appear in the dropdown box
    - If it does not show up, select **Options** and **List All Devices**
  - **Make sure USBasp is selected** (You don't want to accidentally flash something on your PC)
  - Install the **libusbK** driver; if it doesn't work, use the **libusb-win32** driver instead
- Download and install WinAVR http://sourceforge.net/projects/winavr/files/latest/download
  - Select BOTH:
    - **[x] Install Files**
    - **[x] Add Directories to PATH (Recommended)**
- Connect the USBasp cable to the OpenEVSE then plug the USBasp into a USB port on the PC
- Download a pre-compiled HEX, BIN, and BAT files from the OpenEVSE Sources https://github.com/OpenEVSE/open_evse/releases and put them into the same directory
- Run the flash.bat

</br>

> ***NOTE:*** ``` error: cannot set sck period; please check for usbasp firmware update ``` is normal with older firmware and can be ignored
> To fix this error you need to update your USBasp firmware

</br>
SAMPLE batch file (flash.bat):

```
@echo off
avrdude -c USBasp -p m328p -U lfuse:w:0xFF:m -U hfuse:w:0xDF:m -U efuse:w:0x05:m
avrdude -V -c USBasp -p m328p -U flash:w:openevse.hex
avrdude -V -c USBasp -p m328p -U eeprom:w:eeprom_24.bin
@echo
echo Last Flash Performed at:
time /T
pause
flash.bat
```

</br></br>

## Flashing Tips:

When using a USBasp to flash OpenEVSE via ISP
- Open the BAT file and make sure the HEX and BIN names match the files you downloaded
- Make sure the voltage is set to 5v
- Pin 1 is MISO

| OpenEVSE v5.5 | USBasp ISP Connector |
| :---: | :---: |
| Ground ○ ___ ○ Reset | GND ○ ___ ○ RST |
| MOSI ○ ___ ○ SCK | MOSI ○ ___ ○ SCK |
| +5v DC ○ ___ ◙ MISO | VCC ○ ___ ◙ MISO |

</br></br>

## Troubleshooting:

If you receive error:</br>
  ```
  avrdude: error: could not find USB device with...
  ```
- Install the libusb-win32 driver

If you receive error:</br>
  ```
  avrdude: error: program enable: target doesn't answer. 1
  avrdude: initialization failed, rc=-1
  ```
- Most likely you're plugged in 180° out (i.e., Pin-1 is on GND vs MISO)

</br></br>

# ADVANCED - How to Flash the USBasp Firmware (in Windows with a USBasp)

Download the latest version of USBasp firmware from: http://www.fischl.de/usbasp/ or to make your USBasp WCID compliant use the firmware in the [USBasp-Firmware](https://github.com/RealCarvedArt/Tesla-OpenEVSE/tree/main/Firmware/USBasp-Firmware) directory
- Extract the firmware from the bin\firmware\ directory in the tar.gz file (You can use 7-Zip to extract)
- Put the firmware into an empty directory

Create a batch file named USBaspFirmware.bat and put in in the same directory

SAMPLE batch file using the original firmware (USBaspFirmware.bat):

```
@echo on
avrdude -v -c usbasp -p m8 -U flash:w:usbasp.atmega8.2011-05-28.hex:i
pause
```

SAMPLE batch file using the WCID compliant firmware (USBaspWCIDFirmware.bat):

```
@echo on
avrdude -v -c usbasp -p m8 -U flash:w:usbasp.atmega8.2022-07-16.hex:i
pause
```


![USBasp](https://user-images.githubusercontent.com/78761379/224510732-716f17e0-a90b-48ee-967d-2a24b4380dba.png)

- Plug in your USBasp
- Identify what type of USBasp you have (Look at what’s printed on the chip: ATMega8, ATMega88, or an ATMega48)
  - To determine the version of avrdude currently installed run the following code at the command prompt:
    - avrdude -v (verbose) -c \<programmer\> -p \<partno\> (You can use ```avrdude -?``` to view the options for avrdude)
    - For example, if you're using a USBasp with an ATmega8 chip you would use:
    
    ```
    avrdude -v -c usbasp -p m8
    ```

    SAMPLE results:

    ```
    avrdude: Version 5.10, compiled on Jan 19 2010 at 10:45:23
             Copyright (c) 2000-2005 Brian Dean, http://www.bdmicro.com/
             Copyright (c) 2007-2009 Joerg Wunsch
    ```

    \- or - (You can simply copy the [latest avrdude files](https://github.com/avrdudes/avrdude/releases/) into the C:\WinAVR-20100110\bin\ directory to update)

    ```
    avrdude: Version 7.1
             Copyright the AVRDUDE authors;
             see https://github.com/avrdudes/avrdude/blob/main/AUTHORS
    ```


On the USBasp that you want to update the firmware on:
- If the 2-pin header is missing, solder a 2-pin jumper on the board next to the 3-pin "Supply Target" header (boards are often labeled either JP1 or JP2)
  > You could jump it with a paperclip in a pinch
- Apply a jumper across the "Self Program" pins
- Connect a second USBasp via the 10-pin cable (The USBasp to be flashed must have a jumper on the "Self Program" pins and the flashing USBasp must be open)
- Then plug the second USBasp into a USB port on the PC (The one without the jumper)
- Run the USBaspFirmware.bat -or- USBaspWCIDFirmware.bat

![USBasp2USBasp](https://user-images.githubusercontent.com/78761379/224511002-757b1bc3-0bab-4c77-8501-935081e989cc.png)

A successful flash of an ATmega8 using the WCID firmware looks like this:

```

C:\Users\RealCarvedArt\Desktop\USBasp>avrdude -v -c usbasp -p m8 -U flash:w:usbasp.atmega8.2022-07-16.hex:i

avrdude: Version 7.1
         Copyright the AVRDUDE authors;
         see https://github.com/avrdudes/avrdude/blob/main/AUTHORS

         System wide configuration file is C:\WinAVR-20100110\bin\avrdude.conf

         Using Port                    : usb
         Using Programmer              : usbasp
         AVR Part                      : ATmega8
         Chip Erase delay              : 10000 us
         PAGEL                         : PD7
         BS2                           : PC2
         RESET disposition             : possible i/o
         RETRY pulse                   : SCK
         Serial program mode           : yes
         Parallel program mode         : yes
         Timeout                       : 200
         StabDelay                     : 100
         CmdexeDelay                   : 25
         SyncLoops                     : 32
         PollIndex                     : 3
         PollValue                     : 0x53
         Memory Detail                 :

                                           Block Poll               Page                       Polled
           Memory Type Alias    Mode Delay Size  Indx Paged  Size   Size #Pages MinW  MaxW   ReadBack
           ----------- -------- ---- ----- ----- ---- ------ ------ ---- ------ ----- ----- ---------
           eeprom                  4    20   128    0 no        512    4      0  9000  9000 0xff 0xff
           flash                  33    10    64    0 yes      8192   64    128  4500  4500 0xff 0x00
           lfuse                   0     0     0    0 no          1    1      0  2000  2000 0x00 0x00
           hfuse                   0     0     0    0 no          1    1      0  2000  2000 0x00 0x00
           lock                    0     0     0    0 no          1    1      0  2000  2000 0x00 0x00
           signature               0     0     0    0 no          3    1      0     0     0 0x00 0x00
           calibration             0     0     0    0 no          4    1      0     0     0 0x00 0x00

         Programmer Type : usbasp
         Description     : USBasp, http://www.fischl.de/usbasp/

avrdude: auto set sck period (because given equals null)
avrdude usbasp_spi_set_sck_period() error: cannot set sck period; please check for usbasp firmware update
avrdude: AVR device initialized and ready to accept instructions
avrdude: device signature = 0x1e9307 (probably m8)
avrdude: Note: flash memory has been specified, an erase cycle will be performed.
         To disable this feature, specify the -D option.
avrdude: erasing chip
avrdude: auto set sck period (because given equals null)
avrdude usbasp_spi_set_sck_period() error: cannot set sck period; please check for usbasp firmware update
avrdude: reading input file usbasp.atmega8.2022-07-16.hex for flash
         with 5670 bytes in 1 section within [0, 0x1625]
         using 89 pages and 26 pad bytes
avrdude: writing 5670 bytes flash ...

Writing | ################################################## | 100% 6.77 s

avrdude: 5670 bytes of flash written
avrdude: verifying flash memory against usbasp.atmega8.2022-07-16.hex

Reading | ################################################## | 100% 5.61 s

avrdude: 5670 bytes of flash verified

avrdude done.  Thank you.

```
