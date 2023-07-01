# FLOOB TOOOLE - Fluke 700013 Analog Switch Replacement
Several old Fluke multimeters (and potentially other equipment as well) use this custom chip made by Fluke called the 700013. It's just a quad SPST analog switch chip but the control lines are latched and also pass through an AND gate. There's no off-the-shelf equivalent chip, and these chips are known to be unreliable.

![FLOOB TOOOLE circuit board](https://github.com/schlae/TOOOLE/blob/main/TOOOLE.jpg)

So I cloned the chip using a simple circuit that fits on a tiny circuit board. The new design uses any off-the-shelf DG412 or equivalent (industry standard pinout). To implement a 4-bit transparent latch, the design uses a 74157 quad 2-input mux with one set of inputs connected to the data coming in and the other set of inputs connected to the *outputs* of the mux to recirculate the data and latch it.

I've tested the board in my Fluke 8840A as a replacement for two of the chips in the ohms section, and it seems to work fine. I have not tested it in any of the other sections.

By the way, since the DG412 footprint is industry standard, feel free to substite it with your favorite quad analog switch. If yours uses active low control inputs, you can swap U2 with a 74AHCT00.

Check out the [schematic](https://github.com/schlae/TOOOLE/blob/main/TOOOLE.pdf)

## Bill of Materials

| Des | Mouser part number | Description |
|-----|--------------------|-------------|
| U1  | 78-DG412DQ-T1-E3   | Quad analog switch, SPST |
| U2  | 771-AHCT08PW118    | Quad AND gate |
| U3  | 771-AHCT157PW118   | Quad 2-1 line multiplexer |
| C1  | (generic)          | 0.1uF 25V X5R 0603 ceramic capacitor |
| R1  | (generic)          | 1K ohm 5% 0603 carbon resistor |
| Q1  | 512-2N7002L        | n-channel MOSFET, SOT23 (can be subbed) |
| J1  | (generic)          | 20x DIP pins (flip pins or others) |

## Assembly Instructions

Build the board using your favorite board vendor. I'm in the United States so I just sent the KiCAD board file directly to [OSH Park](https://oshpark.com/). The grand total was $3.40 for 3 boards, including shipping.

Solder the surface mount components first, then install the Flip Pins (but you could also use wires soldered into a machine-pin DIP socket). Be sure to clean the board thoroughly with isopropyl alcohol, since any residue will increase the leakage current of the DG412.

You can test it on a breadboard first, which might be a good idea if you aren't sure about the quality of the solder joints. I'd recommend installing a socket in your Fluke instrument, and then plugging the board into the socket.
