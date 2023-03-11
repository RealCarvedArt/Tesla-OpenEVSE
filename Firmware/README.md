# How to Flash the OpenEVSE Firmware (in Windows with a USBasp)

- Download Zadig (http://zadig.akeo.ie/)
- Plug in your USBasp
- Run Zadig
  - USBasp should be detcted and appear in the dropdown box
    - If it does not show up, select **Options** and **List All Devices**
  - **Make sure USBasp is selected** (You don't want to accidentally flash something on your PC)
  - Install the **libusbK** driver; if it doesn't work, use the **libusb-win32** driver instead
- Download and install WinAVR (http://sourceforge.net/projects/winavr/files/latest/download)
  - Select BOTH:
    - **[x] Install Files**
    - **[x] Add Directories to PATH (Recommended)**
- Connect the USBasp cable to the OpenEVSE then plug the USBasp into a USB port on the PC
- Download a pre-compiled HEX, BIN, and BAT files from the OpenEVSE Sources (https://github.com/OpenEVSE/open_evse/releases) and put them into the same directory
- Run the flash.bat

</br>

***NOTE:*** ```Warning can not set SCK period``` is normal with older firmware and can be ignored

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

| OpenEVSE v5.5 | USBasp ISP conncetor |
| :---: | :---: |
| Ground ○ ___ ○ Reset | GND ○ ___ ○ RST |
| MOSI ○ ___ ○ SCK | MOSI ○ ___ ○ SCK |
| +5v DC ○ ___ ◙ MISO | VCC ○ ___ ◙ MISO |

</br></br>

## Troubleshooting:

If you recieve error:</br>
  ```
  avrdude: error: could not find USB device with...
  ```
- Install the libusb-win32 driver

If you recieve error:</br>
  ```
  avrdude: error: program enable: target doesn't answer. 1
  avrdude: initialization failed, rc=-1
  ```
- Most likely you're plugged in 180° out (i.e., Pin-1 is on GND vs MISO)

</br></br>

# How to Flash the USBasp Firmware (in Windows with a USBasp)

Download the latest version of USBasp firmware from:  (http://www.fischl.de/usbasp/)
- Extract the firmware from the bin\firmware\ directory in the tar.gz file (You can use 7-Zip to extract)
- Put the firmware into an empty directory

Create a batch file named USBaspFirmware.bat and put in in the same directory

SAMPLE batch file (USBaspFirmware.bat):

```
@echo off
avrdude -v -c usbasp -p m8 -U flash:w:usbasp.atmega8.2011-05-28.hex:i
@echo   
echo Last Flash Performed at:
time /T
pause
```

![USBasp](https://user-images.githubusercontent.com/78761379/224510732-716f17e0-a90b-48ee-967d-2a24b4380dba.png)

- Plug in your USBasp
- Identify what type of USBasp you have (Look at what’s printed on the chip: ATMega8, ATMega88, or an ATMega48)
  - To determine the version of firmware currently installed the USBasp run the following code in a command window:
    - avrdude -v (verbose) -c \<programmer\> -p \<partno\> (You can use ```avrdude -?``` to view the options for avrdude)
    - For example if you're using a USBasp with an ATmega8 chip you would use: ```avrdude -v -c usbasp -p m8```
SAMPLE result:

```
avrdude: Version 5.10, compiled on Jan 19 2010 at 10:45:23
         Copyright (c) 2000-2005 Brian Dean, http://www.bdmicro.com/
         Copyright (c) 2007-2009 Joerg Wunsch
```


On the USBasp that you want to update the firmware on:
- If the 2-pin header is missing, solder a 2-pin jumper on the board next to the 3-pin "Supply Target" header (boards are often labeled either JP1 or JP2)
- Apply a jumper across the "Self Program" pins
- Connect a second USBasp via the 10-pin cable (The USBasp to be flashed must have a jumper on the "Self Program" pins and the flashing USBasp must be open)
- Then plug the second USBasp into a USB port on the PC (The one without the jumper)
- Run the USBaspFirmware.bat

![USBasp2USBasp](https://user-images.githubusercontent.com/78761379/224511002-757b1bc3-0bab-4c77-8501-935081e989cc.png)

