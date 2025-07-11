# Design notes for TasBufo. 
This board began as an extension of the toads-di functionality to try and make it work with my Retevis RT-95 radio (which doesn't have a 'data' port but _does_ talk serial over the front RJ45 port to the embedded microcontroller in the standard microphone) and things just escalated from there.

## Hardware layout
Maintaining compatibility with the toads-di 2\*6 J2 header and the 24/34mm fixing centres was important to me. Everything else kinda grew off to the sides. Final size of PCB will depend on what paneling options work out cheapest at the PCB factory, and availability of boxes at the local Jaycar.

I'd also like to shout out to [Graham Sutherland's Blog posting](https://blog.poly.nomial.co.uk/2025-07-05-tips-for-getting-pcbs-made-with-jlcpcb.html) as this was my first interaction with JLCPCB.

## USB C upstream connection
I'm just using a 16 pin connecor wired for USB-2 compatibility. Sorry if you're expecting USB 3.x super-speed goodness, but nothing on this board require that extra complexity. Hoprfully both sides of the connector are wired so cable should be reversible.

## USB Hub 
The digirig board (which thanks to their open source licence, has been a significant help in designing this board) uses a 2 port USB hub (USB2412), which might have been enough, but for the sake of a few extra tracks I went with a 4 port version (Microchip USB2514B), breaking out the 'spare' connections to a header on the PCB for future use. For want of anything more standard, these come out to the 'motherboard' 9 pin design.

The 2 onboard (sound chip and uart) devices are marked as non-removable by pulling the appropriate strap pins. 

LEDs ???

## CM108B Sound Chip
Chosen for compatibility with AllStarLink asterisk drivers. The 3 GPIO pins are broken out to the Jx *FIXME* header in the same 2\*6 pin arrangement as toads-di, the idea being that you can use one of their daughteboards to connect directly to your radio with the various adjustment pots in place. 

The board design configures this chip as a headset (via pin 10 pulled low) to enable the microphone.

Pads are included for the optional 93C46 EEPROM, the addition of which would allow the user to set and save volume settings. Pads are designed around the Atmel AT93C46D device.


## CP2102N Serial Uart
There are lots of possible USB-Serial UART chips. FTDI is at risk of 'fake' chips then not being supported by the driver, so I've chosen the Silicon Labs CP2102N as a compromise. The 6 pin header uses the same pinout as the 'standard' FTDI header used by many breakout boards for programming microcontrollers and exposes GND, CTS, 3.3v VCC, TX, RX, and DTR. 

*FIXME* Possibility of a 3-pad cuttable jumper or 0-ohm resistor to switch from 3.3v to 5v if user requires?

*FIXME* RS232 - Digirig-mobile has a ADM3101E level converter? overkill? leave pads in v2?

# Datasheets
All datasheets I have used in this design are in the datasheets/ directory. They were the most recent I could find at the time of design. It is the users responsibility to check these are still current if adapting the board.

The TOADS-DI interface is NOT open source, but their [manual is available online](https://geni.us/toads-di)

# LICENCE
Given that digirig is GPL3. we may as well go open source. I've chosen the [CERN open hardware licence](https://cern-ohl.web.cern.ch/) mainly because I used to work there and they're supporting KiCad. 

