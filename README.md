# "Solar" PCB
--------------

Shared at oshpark:
https://oshpark.com/shared_projects/fC9XhvWo

This is a tiny PCB facilitating (atleast) two different circuits
that implement charging of a *protected* li-ion cell + night-light
functionality from a solar panel (usual suspect is one of those
6V 1W ones).

## Simpler ciruit - one N-fet ##
- Install the B- to S- diode
- Install the N-fet on the bottom (nearer to B+/B-) position
- bridge B+ to S+ (no diode, just a wire)
- bridge the S- to FET resistor position
- bridge the SMD solder jumper from the LOAD- to the 1st FET output

This circuit will activate the nightlight when Vpanel < (Vbattery - Vth),
that is you need almost the full battery voltage to turn off the load.

Effective schematic:
 S+ ---------------- B+ & L+
 
            /------- L-
     /----| Q
     |      |
 S- -*-|<---*------- B-


## Two-fet circuit ##
- Install the S+ to B+ diode
- install both N-fets
- install the pull-up resistor from B+ - eg. 470k
- bridge the S+ to FET resistor position
- bridge B- to S-

This ciruit will activate the nightlight when Vpanel < Vth, that is
it disables the load much earlier, at the cost of a few microamps
through the pull-up resistor during the off-time.

Effective schematic:
 S+ -*->|----*------ B+ & L+
     |       |
     |       R
     |       |    /- L-
     |    /--*--| Q
     \--| Q       |
          |       |
 S- ------*-------*- B- 


## Things and stuff ##

The PCB will facilitate either TO-92-style transistors where
the gate/base is the middle pin or SOT-23 with the GSD
pin order, eg. AO3400, IRLML2502, IRLML6344. 

For resistors there is a through-hole pattern and a
hand-soldering friendly 0805 SMD pattern (that you can
likely put a size up or down into too).

For diodes it will take basic through-hole ones (1N5817 or similar)
and SMD diodes from SMB to SOD-323 (and SMA and SOD-123 on the way).

I prefer FETs for this circuit (primarily because they need almost
no current to switch) but it should be workable with BJTs too,
just use a resistor instead of the link for the control line.

You could also play with resistors on both positions to adjust 
the light thresholds, etc... just look at the schematic
and have fun :P.

Another funky idea: put a BJT on the second transistor position
and set it up as a slightly more constant current source for
your LEDs...

Also, for funsies the entire schematic ASCIIfied:

 S+ -*->|----*--------- B+ & L+
     |       |
     R       R  /-J-*-- L-
     |       |  |   |
     |    /--*--*-| Q
     *--| Q         |
     |    |         |
     R    |         |
     |    |         |
 S- -*-|<-*---------*-- B-


