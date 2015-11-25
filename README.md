# QuadCopter Project
This project is for our Embedded systems course. Our plan is to build a QuadCopter that would be able to stabilize indoors using a camera on board that it will use an object as reference points.



##Hardware
* ArduCopter (APM 1.4)
* ESC AC30-1.0 (Jdrones 30A)
* Motors 
* GPS
* Compass (Magnetometer)
* IMU Shield/ oilpan (JD-APMIMU H V1.1A)
* Lipo Batter 4s 5000mAh 14.8v
* RC Controller (Spektrum dx8)
* RC Transmitter (AR6210)
* Xbee Pro

##Software
* Mission PLanner
* KKmulticopter Flashing tool

##Setup

###Configuration
Usually you can configure the quad in one of the following configurations:

1. The "+" configurations (one arm forward)
2. The "x" configurations (two arms at 45 degrees on either side of the direction)  

We chose to use the "x" configuration as it will make it easier for us to calibrate.

The way to select which mode you want is with the DIP switch on the IMU board:
![IMU DIP switches for configuration](./images/Flight_Mode_Selection.jpg)

###Connections
</br><img src="./images/DiagramRC_APM14.jpg" alt="APM connections" height="400" width="600">

###Motor Setup
Configuring the motor directions:

1. The ESCs have three blue output connections, connect all of them the same way.
2. Observed the direction they turn in. 
3. Switch any two of the wires to reverse the direction of the motors to much the diagram below. 

</br><img src="./images/Motor_Dir.jpg" alt="Motor direction" height="400" width="700">

###RC Setup
The remote control and transceiver need to be binded as follows:

1. Attach the binding jumber cable to the transceiver, the light should start blinking.
2. Turn off power controller.
3. Power on the controller while pressing the Training button on top of the controller until the light on the transceiver turns solid. 

##Modification

###ESC
The ESC is usually sold with a firmware that limits its refresh speed to  8khz. We decided to flash it with SimonK firmware that allows the refresh speed to reach 400khz which allows more control on the motors.

How it's done:

1. Identify ESC and its ISP connections 
</br><img src="./images/DYS30AMP.jpg" alt="ESC Model" height="400" width="600">
2. Remove Cover just enough to access the SPI pads ![ESC power]()
</br><img src="./images/ESC_cut.jpg" alt="ESC power" height="400" width="600">
3. Modified the connection from an avrisp mkii programmer to be able to connect to the ESC (MISO, MOSI, REST, VCC, GND) 
</br><img src="./images/AVRISP.jpg" alt="avrisp mkii" height="400"width="500">
</br><img src="./images/avrispmkII-pin.jpg" alt="AVR" height="400"width="600">
</br><img src="./images/Connection.jpg" alt="Modified Connection" height="400"width="500">
4. Connect ESC to power (6-16v)
</br><img src="./images/ESC_power.jpg" alt="ESC power" height="400"width="600">
5. Attach connection to the pads in the correct position
</br><img src="./images/ESC_Flashing.jpg" alt="ESC Connect" height="400"width="600">
6. Using KKmulticopter Flashing tool, flash with the latest SimonK firmware TYG version 
</br><img src="./images/ESC_DONE.jpg" alt="ESC Flashed" height="400"width="600">

###Communication

Initially the arducopter was only setup to recieve telemetry while connected through the usb connector. We soldered telemetry pins on board in order to connect an Xbee pro on board for two-way communication between our laptop and Apm.
</br><img src="./images/xbeeCommunication.jpg" alt="Xbee Connection" height="400"width="600">


###Parameter changes
Changes to the default parameter in Arducopter can be written using the mission planner.
* Changed RC pins for Throttle, Yaw, Pitch and Roll to correspond with RC transciever. (channel 7, 6, 5 and 4)


##Issues and Failures
1. Initially we thought that since the ESCs we have are similar to the DYS designs that they should be flashed with SimonK's DYS N-FET bu that was a mistake, because these ESC's are quite different.


##References
1. APM archived manual- https://code.google.com/p/ardupirates/wiki/RC 
2. Drivers for AVRISP- http://zadig.akeo.ie/
3. ESC Flashing- http://www.rchacker.com/diy/simonk-esc-firmware-flashing
4. Xbee 2-way communication- http://www.ardupilot.co.uk/guide/ardupilot-mega-telemetry-kit-2-way-communications-with-your-uav
5. ESC firmware Database- https://docs.google.com/spreadsheet/ccc?key=0AhR02IDNb7_MdEhfVjk3MkRHVzhKdjU1YzdBQkZZRlE#gid=0

