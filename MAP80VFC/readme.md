# Modification to the MAP80 VFC card.

Link 4 on the VFC card selects if the Boot Rom is enabled or not at the start. The connection b on the link feeds the input of a logic gate and connection "a" grounds that feed and connection "c" connects it to 5v. I used a 10k resistor between connectors "b" and "c" so the normal state is disabled. I connected Pin 7 on the backplane to connection "b" so that when pulled low by the switch it would be enabled.

The major issue here was that the VFC card did not have any edge connectors for pin 7. I used some narrow sticky back copper strip, normally sold as a slug deterant, and created an edge connector. To give some assurance that the connector was working I added an Resistor+LED between the 5v on the board and connection "b". The LED lights up when the CP/M mode is selected.
