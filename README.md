# Nascom2-DualBoot

This details how I setup my Nascom2 computer to be able to boot into either NAS-SYS3 or CP/M disk system.
The NASSYS3 system used the Monitor Rom and VWRAM on the main Nascom2 baord, it also had optional Rom chips in BANKA and BANKB of the main board. These could be optional selected when in NASSYS3 mode but not when in CP/M mode.
The CP/M system used a boot rom on the MAP80-VFC card plus the MAP80-VFC video output, and a MAP80 256k Ram card.

The changes involved a number of separate parts.

1. Adding switches to the main system and connecting them to lines on the back plane.
2. Adding a "daughter" board the the Nascom 2 main board to control the links on the LKS1 socket.
3. Adapting the MAP80 VFC card so that link 4 would be pull high by a resistor and pull low by the switch line.
4. As I was using the MAP80 VFC video switch modifying the NASSYS3 rom to switch over the the Nascom display.

## 1.Adding switches
 This was done by using a wooden front panel for the switches with a IDC cable attaching it to the back plane.
 The lines on the backplane I used were
 Pin 7 - main CPM/NASSYS3 switch
 Pin 66 - activate BankA Roms
 Pin 65 - activate BankB Roms.
 The switches either allow the lines to float or pull them to 0v. Pull up resistors on the various cards handle the pulling the lines high.
 
 ## 2. CPMSwitch "daughter" board
 I created a PCB using KiCad to control the links in socket LKS1. It sits in the LKS1 socket and has 5 flying leads to provide power and connections to the 3 lines on the back plane. The board does not sit quite how I wanted it due to a slight mistake in the PCB layout but it does sit ok on my system.
 
 ## 3. MAP80 VFC modifications
 Link 4 on the VFC card selects if the Boot Rom is enabled or not at the start. The connection b on the link feeds the input of a logic gate and connection "a" grounds that feed and connection "c" connects it to 5v. I used a 10k resistor between connectors "b" and "c" so the normal state is disabled. I connected Pin 7 on the backplane to connection "b" so that when pulled low by the switch it would be enabled.
 
 The major issue here was that the VFC card did not have any edge connectors for pin 7. I used some narrow sticky back copper strip, normally sold as a slug deterant, and created an edge connector. To give some assurance that the connector was working I added an Resistor+LED between the 5v on the board and connection "b". The LED lights up when the CP/M mode is selected.
 
 ## 4. Modifying NASSYS3
 Taking an idea from the monitor for NASCOM3 I was able to add the required code to the normal startup process by shortening the actual startup -- NASSYS 3 -- message. I programmed a new 28C16 EEPROM chip for the Monitor ROM. These chips are easy to program as they only use the standard 5v lines. See my other project on programming the 28c16.

## Finally 
Hopefully there is enough information here to allow you to understand what I did but if you have any questions please let me know.

If anybody wants one of the PCB board then let me know - I had to get 10 done for the first batch. Otherwise you can checkout the Kicad version in this project.

Happy hacking David Allday
 
