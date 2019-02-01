Gerbv Project with Gerbers for V1.1.2 of the PCB
================================================

The V1.1.3 PCB is very similar to V1.1.2, and BOTH have a design flaw in the FTDI VCC connection. 


The way that Creality has wired it is wrong at a number of levels. 

The following symptoms happen when main power is turned off.

1. The USB port will attempt to power the main +5V via DP2.
2. This can cause your hub to disable the USB port because too much power is being pulled from the port.
3. This will keep the LCD backlight on, which is obnoxious at night. My cat hates it.
4. This creates a high pitch whine. I haven't personally verified it, but other reports say this whine is the fan trying to start.

The FTDI part is the 28-pin SSOP at U1 (See Gerber)

Datasheet is here: https://www.ftdichip.com/Support/Documents/DataSheets/ICs/DS_FT232R.pdf

There are two fixes for this. 

1. Butcher a perfectly good USB cable and cut the +5V wire. This has the problem that when you turn the printer off, the USB port goes away.
2. Fix it properly, so the USB cable just powers the FTDI part and nothing else. 
  - The port will not disappear when main power is off.
  - The LCD backlight will remain off and that awful high-pitched whine will stay away.


The major steps for #2 above are:
  * Lift Pin 20 on U1 and wire it according to page 23 of the data sheet titled 'USB Bus Powered Configuration.
  * Remove DP2.

Option 2 details:

Page 7 of the datasheet has the pin out, and you are looking for VCC (Pin 20).

1. Since there is a ground plane very close to pin 20, scrape off the solder mask down to bare copper close to the pin (close enough to reach it with the ferrite bead soldered to pin 20.
2. Lift pin 20 on U1.
3. Pre-tin the ground plane you scrapped. It will take a bit of heat.
4. Solder the 10nF ceramic chip cap (i.e. 10,000pf,.01uF, usually marked 102) to ground where you scraped the solder mask off. 
5. Solder a wire to the via on the USB +5V on the connector labeled 'USB'. There is a via on this line that a 26 gauge solid wire fits through perfectly.
6. Solder the wire from +5 USB to the other end of the cap.
7. Solder the ferrite bead to pin 20 and the +5V USB.
8. Remove DP2 (or cut the trace that goes to the via in the middle of DP2 on the bottom of the board).

This is the primary complaint I have with my Ender 3. Other than this, it is a very, very nice 3D printer. Let us hope V1.1.4 has this fix.

