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

***NOTE:*** ```Warning can not set SCK period``` is normal and can be ignored
</br></br>

## Flashing Tips:

When using a USBasp to flash via ISP
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
