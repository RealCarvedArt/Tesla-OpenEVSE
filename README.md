# Tesla-OpenEVSE → Using a Tesla Wall Connector Gen 2 (HPWC) housing and a Tesla 24' whip

## Tesla Gen 2 HPWC Cable to OpenEVSE Kit (Pinouts & Identifications)

### Large Gauge
🔴	**RED** → AC Lead 1</br>
⚫	**BLACK** → AC Lead 2</br>
🟢/🟡	**GREEN/YELLOW** → Earth Ground</br>

### Small Gauge
🟣	**PURPLE** → Control Pilot → OpenEVSE Controller Pilot [PLT] connector</br>
🔵	**BLUE** → Charge port transmitter → 3.3v output on the WiFi Controller (Alternatively, to use an OpenEVSE 5v output add a few diodes in series to drop the voltage down a bit)</br>
⚫	**BLACK** → not used</br>
🟠	**ORANGE** → not used</br>
⚪	**WHITE** → not used</br></br>

## BUILD NOTES:
- Made a custom aluminum backplate to fit into the Tesla Gen 2 housing
- Reused the original Tesla Gen 2 relay mounting backplate/heatshield to mount the OpenEVSE relay
- Reused mounting screws and standoffs from the Tesla Gen 2 to mount the OpenEVSE Charging Station Controller
- Mounted the OpenEVSE WiFi Controller under the cable end socket so the status LEDs eluminate the original sight window on the Tesla Gen 2 housing cover
- Opted not to cut the Tesla Gen 2 housing or cover to mount the OpenEVSE LCD Screen to retain the watertight seal
- The original Tesla Gen 2 Reset Button could be utilized to actuate the optional button (Button Menu) on the OpenEVSE LCD Screen by adding a Jst 2.0 Ph 3 Pin pigtail
- Was able to retain all of the Tesla Gen 2 factory terminations on the cable by carefully bending the fork-type terminal ends to just push through the OpenEVSE AMP & GFCI Coils (Much patients & calculated alignment of each cable & terminal is required)</br>

## Some pics of how it fits...

![1](https://user-images.githubusercontent.com/78761379/220809885-8755c537-41ca-4bbf-84e0-f65cdb705790.jpg)

![2](https://user-images.githubusercontent.com/78761379/220809891-e8948dd8-8e3c-4fee-b2be-7fe258a3ec45.jpg)

![3](https://user-images.githubusercontent.com/78761379/220809914-df606c77-bd1f-4711-9326-fb588198e445.jpg)

![4](https://user-images.githubusercontent.com/78761379/220809925-77ddbbc0-af15-4abf-aa4a-81643d72ab00.jpg)

![5](https://user-images.githubusercontent.com/78761379/220809930-6aab4508-73e1-453d-9008-731c9a6a6cd8.jpg)

![6](https://user-images.githubusercontent.com/78761379/220809934-140cf16b-8b8a-4193-b984-307feeb4c8dd.jpg)

![7](https://user-images.githubusercontent.com/78761379/220809939-24bd9d5e-cab3-4de0-b68d-6f172daa7798.jpg)
