# lhoracek Kossel Plus Firmware (based on Marlin 2.0.x)

based on: [Knutwurst's](https://github.com/knutwurst/Marlin-2-0-x-Anycubic-Kossel-Linear-Plus)

# Readme - English

![Kossel Plus with 12864 LCD](images/kosselplus_lcd_full.jpg)

These configurations activate many of the new advanced features of the Marlin firmware:

 * Auto Calibration
 * S-Curve Acceleration
 * Babystepping while printing (double click on control knob)
 * Unified Bed Leveling (UBL)
 * Manual Mesh Edit via LCD
 * Full LCD 12864 Full Graphic Smart Controller Support
 * Progress Bar support for 2004 and 12864 LCD
 * Pause & Filament Change

...and Games! (click below)

[![Games on Anycubic Kossel Plus](https://img.youtube.com/vi/zc9mY9pi9JI/0.jpg)](https://www.youtube.com/watch?v=zc9mY9pi9JI)

**Important**: Before doing anything else after updating the firmware, go to `Configuration > Advanced Settings > Initialize EEPROM` to get rid of old configurations.

Please test the Z-height with a sheet of paper. At Z = 0.00 the nozzle should almost rest on the print bed. If not, set the Z-probe height again and change the value under `Configuration> Advanced Settings> Probe Z Offset`.

**Tutorial: Get the correct z probe offset**

1. Pace a sheet of paper on the heated bed.
2. Slide the nozzle onto the bed so that the sheet is just about to move. If you still have a gap between the nozzle and the sheet of paper even at 0.00, go back and deactivate the "Soft Endstops". The setting is dangerous however, because you can now go further down than actually possible and thus damage the nozzle and the bed. So be careful!
3. Write down the value on the display. (e.g. +0.20)
3. Run the Z-axis up a little and clamp the probe underneath.
4. Slowly drive back down (in 0.01mm steps) until you hear the click. Do not go further!
5. Write down the value on the display. (e.g. +16.40)
5. Subtract the value of point 5 from the value of point 3. -> 0.20 - 16.40 = -16.20
6. Enter the calculated value as a Z probe offset.
If the offset does NOT correspond to what the current default value is (-16.20), you MUST perform the auto calibration again afterwards.

After everything is checked, go to `Configuration> Delta Calibration> Auto Calibration` to perform the automatic calibration. The settings are saved automatically.

You should then execute `Motion> Unified Bed Leveling> Step by Step bed leveling` and save it with` Store Settings`.

**WARNING! DO NOT EDIT THE DELTA HEIGHT!**

It has been around on youtube for a while, but it is a highly outdated procedure, which was a workaroud for a non-working mesh leveling and a wrongly configured Z-Probe offset. So do yourself a favour and do not fiddle around with the Delta settings, which should have been calculated perfectly. Everything you need is a perfect Z-Probe offset (until you hear the clicking noise) and the UBL will do the rest for you.



# Select the Configuration

**Please select the correct values at the start of the Configuration.h file**

The Kossel comes in 3 versions:

 * Pulley
 * Linear
 * Linear Plus

Pulley and Linear use the same configuration, the Linear Plus is bigger and uses slightly different configurations.

Typically the probes for the Anycubic Delta Kossel printers come in two different versions.

  * Version 1: Z Probe Offset of -19.0mm

    ![Version 1 Probe](images/Version1Probe.jpg)

  * Version 2: Z Probe Offset of -16.2mm

    ![Version 2 Probe](images/Version2Probe.jpg)

If you select the `ANYCUBIC_PROBE_VERSION 0`: It's very important to follow the correct procedure to set it up after flashing the firmware, otherwise you might damage the printer by ramming the nozzle into the heatbed:

* `Configuration > Advanced Settings > Initialize EEPROM`
* `Motion > Move Axis > Soft Endstops` : `Off`
* Auto Home and slowly move the nozzle down until it barely touches the bed. (Do a paper-test: A normal sheet of paper should just feel the drag of the nozzle) and note this number.
* Subtract this number from the value in `Configuration > Delta Calibration > Delta Settings > Height`. (If it's negative, add it).
* Save and try the paper test again to verify your height.
* `Configuration > Store Settings`
* `Motion > Unified Bed Leveling (UBL) > Manual Mesh Bed Leveling`

# Download

You can download binary releases from the releases page, which can be found here: https://github.com/knutwurst/Marlin-2-0-x-Anycubic-Kossel-Linear-Plus/releases. Of course you can also build the firmware by yourself using PlatformIO or Arduino IDE.

In order to make it clear, the file names contain the individual features.

`_PLUS` stands for the Kossel Linear Plus with 240mm Ultrabase.

`_12864` stands for the full graphic display with 128x64 pixels.

`_TMC` stands for Trinamic TMC motor driver. The direction of rotation of the motors is also inverted.

`_BLTOUCH` stands for the BL-Touch version with autoleveling sensor.
