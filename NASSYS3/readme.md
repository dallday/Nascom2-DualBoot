# Modify NASSYS3 

The VFC card either defaults to showing the Nascom video or the VFC video via the on-board analogue switch.
I was not able to “hard wire” this to change depending upon the position of the CPMSwitch on pin 7 of the backplane.
I decided that the idea used in NAS-SYS 3A for the Nascom 3 was a good way to go. This modified the NAS-SYS rom to output the port controls to switch over to the Nascom video just before it displays the “– NASSYS 3 –“ message. 

The MAP80 VFC card is set to display it's video output by default, and NASSYS will switch it over to the Nascom Video as needed.

The switch over is handled by reading from Port 0xEF, needing 2 bytes ( 0xdb 0xef ), so by shortening the actual message it is possible to get the 2 bytes needed to do the trick. 

So the original code
``` Z80 code
    0404 22 6b 0c		ld	(rsp),hl 
    0407 ef		rst	prs 
    0408 ..			defm	"-- NAS-SYS 3 --" 
    0417 0d 00		defb	cr,0 
```
becomes
``` Z80 code
    0404 22 6b 0c		ld	(rsp),hl 
    0407			; added extra instructions  
    0407 db ef		in	a,(vidprt) 
    0409			; end of added instructions 
    0409 ef		rst	prs 
    040a ..			defm	"- NAS-SYS 3 -" 
    0417 0d 00		defb	cr,0 
```

and then a reprogrammed monitor chip, using 28C16 EEPROM, and all is well. 
