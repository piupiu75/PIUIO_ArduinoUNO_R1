# Arduino Uno PIUIO

Emulates a Pump it Up IO board (a.k.a. MK6 PIUIO) using an Arduino Uno.

The code and instructions are slightly modified to support Arduino Uno R1 with button or custom pad input.

This fork was tested with Pump it Up Prime 2015 and IO2KEY utility.

## Install
First:
1. Upload ArduinoPIUAux_Lights onto your Arduino Uno (as you would a regular Arduino sketch)

In linux ([WSL works too if you're on Windows 8/10](https://www.microsoft.com/en-us/p/debian/9msvkqc78pk6?activetab=pivot:overviewtab)):
1. `sudo apt-get install build-essential git gcc-avr avr-libc`
2. `git clone https://github.com/48productions/PIUIO_Arduino`
3. cd to the cloned folder, delete the lufa folder
4. `git clone https://github.com/abcminiuser/lufa`
5. `make`
6. Move PIUIO.hex,elf,bin,eep,lss,map,sym into ATmega8u2Code/HexFiles

Then reboot into windows...
1. Install FLIP https://www.microchip.com/developmenttools/ProductDetails/flip
2. Plug in the Arduino UNO
3. Put the UNO into DFU mode:

- Solder or just push a 10 kOhm resistor to two points on the back of the Uno board. Note: If you have soldered a resistor to enable dfu mode, you need to solder it off before uploading new sketches.

![Uno-back-DFU-resistor](https://user-images.githubusercontent.com/116333562/197133659-ab4bbe4a-3936-41e4-8763-04ba4ceaf051.jpg)

- With the Uno oriented with the USB port to the left, briefly bridge the left two pins on the 2x3 header near the USB port.

4. Install the device by going into device manager, finding the port you noted down earlier, then selecting from a list of drivers, have disk, naviate to "Program Files (x86)/Atmel/Flip 3.4.7/usb/" and then double click the inf
5. After the drivers are set up correctly, run TurnIntoAPIUIO.bat. Congrats, your Arduino is now a PIUIO!
6. Connect the buttons to the corresponding connectors and GND pin according to the scheme below:

- Clear: A0
- Test: A1
- Service: A2
- Coin: 12

Player 1 pad:

- DL: 3
- UL: 2
- C: 4
- UR: 6
- DR: 5

Player 2 pad:
- DL: 8
- UL: 11
- C: 9
- UR: 10
- DR: 7

Note that you can't upload new sketches to your Arduino when it's acting as a PIUIO. If you ever need to change your Arduino back into an Arduino to upload new code:
1. Navigate to C:\Program Files (x86)\Arduino\hardware\arduino\avr\firmwares\atmegaxxu2\arduino-usbserial
2. Copy Arduino-usbserial-uno.hex into HexFiles
3. Put your arduino into DFU mode and run the batch script. Once this above file is copied, you just need to put the arduino in DFU mode and run the appropriate batch file to change between Arduino/PIUIO modes.
