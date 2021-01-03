# Robo3D-Laser


## WARNING!!! 
* ### Working with lasers can be dangerous.  Wear proper eye protection! 
* ### Using high power lasers to engrave or cut will create smoke and fumes. Use in a well ventilated area.
* ### This guide is provided without any guarantees or warranties.  I am not responsible for any property damage or injuries.
* ### I am not a laser expert. Please read up on safety guidelines for Class IIIb lasers.




<br>
<br>
This is a guide to attaching the Creality (or Comgrow) laser head kit to the Robo 3D R1.  The laser head was designed to be able to quicky be mounted and removed via the magnets on it.  The R1 does not have a place to quickly mount this laser head kit.  What I have done is remove the extruder assembly from the printer and replace it with a laser module.

The laser module can be purchased here (affiliate link, would appreciate ordering from this link especially if you found this guide helpful).
https://amzn.to/3hBcbAK

Before removing your extruder, make sure you are able to print this mount for the laser module: https://github.com/mak0t0san/Robo3D-Laser/blob/main/3D%20Models/Robo3D%20Laser%20Mount.stl


<dl>
  <dt><h2>Extruder Removal</h2></dt>
  <dd>Disconnect all the wires going to the extruder assembly. This includes the cable for the stepper motor, thermistor, and heater cartrdige. You can also remove the part cooling fan and the heatsink fan as these won't be needed.  Then, unscrew the two bolts holding the extruder plate on.  You can use a small Phillips screwdriver from the bottom of the extruder plate. You might need some pliers to hold the nuts on the top in place.</dd>
  <dt><h2>Laser assembly</h2></dt>
  <dd>
  <ul>
  <li>
  Attach the laser module to the mount that you downloaded and printed.  You'll need a couple of short M3 screws.  I've found that only 2 screws are needed to hold it securely but you're welcome to use 4. </li>
  <li>Then place the mount into the R1 where the extruder was. You'll be able to attach this with the 2 nuts and bolts that were holding the extruder in place before. 
  </li>
  <li>
  Remove the bottom cover from the R1. We'll need to get to the board. The R1 has a modified version of the RAMPS 1.4 board (which is mounted to an Arduino). Once you have the bottom cover off, locate the fan wire.  It's a plug towards the top-right (if you laid your R1 on the left side) of the board and is labeled "FAN". Disconnect the fan from here and then plug in the laser module.  The connector on the laser module is not the same as the fan plug but it will fit in place as the pin size and spacing is the same. Make sure to match up the polarity correctly (Red +, Black -).
  </li>
  </ul>
  See this image: ![Fan connector](https://raw.githubusercontent.com/mak0t0san/Robo3D-Laser/main/assets/fan-connector.png "Fan connector")
  </dd>
  <dt><h2>Usage</h2></dt>
  <dd>
  This laser module was designed to be able to be added and removed quickly by swapping out the fan for the laser.  At this point, you should be good to go to use the laser, just make sure that the software that you're using uses <code>M106</code> and <code>M107</code> to turn on and off the laser instead of <code>M3</code> and <code>M5</code>. However, using this setup without updating your firmware will limit you quite a bit.  The default firmware doesn't support arc commands (<code>G2</code> or <code>G3</code>) and also doesn't support inline laser power.  You'll be limited to what you can use the laser for.  <br>
  I have created a configuration for Marlin that will allow your R1 to act like a proper laser engraver.
  <br><br>
  There are a couple of important features that have been enabled. Mainly, support for G2 and G3 arc commands, and <code>LASER_POWER_INLINE</code>.  This allows <code>G1</code> commands to specify laser power via the <code>S</code> parameter. This enables the planner to change the laser output and continue to move smoothly.
  </dd>
</dl>