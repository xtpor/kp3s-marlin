
# kp3s-marlin

This repository contains the Marlin firmware built for the Kingroon KP3S printer with the BLTouch upgrade, the files are built using the Auto Build Marlin vscode extension.

The configuration profile is based on https://github.com/bdwilson/KP3S with minor modifications, namely:

1. The BLTouch is connected to the Z-Max port on the motherboard
2. The BLTouch is only used for the ABL (Auto Bed Leveling) process while the Z-endstop is still being used for homing the Z axis

## How to use

1. Install the BLTouch/3DTouch on your printer following the instruction from the official Kingroon website.

https://kingroon.com/blogs/downloads/kingroon-kp3s-bltouch-installation

2. Power on the printer 

3. Grab a SD card formatted in FAT32, copy the file `Robin_nano.bin` into the SD card and insert it into printer.

4. Power on the printer, you should see the message "TFT Updating" appear on the lcd screen.

5. You might need to modify your slicer to output gcode in the "marlin2" flavour

6. You might need to modify your printer's start gcode to put `M420 S` after `G28` to enable ABL after homing 

## Additional Information

After installing the new firmware you should recalibrate the Z offset, E-steps, PID tuning, and auto level the bed, these are settings for my printer you may need to do your own calibration.

XYZ offset for the BLTouch probe

```
M851 X41 Y0 Z-2.8
```

Steps for the stepper motors

```
M92 X160 Y160 Z800 E910
```

PID Tuning

```
M303 E0 C8 S210 ; Start PID tuning for extruder #1 with temp 210c
M304 P13.63 I0.95 D48.78 ; Set the PID values (replace with your own value)
```

ABL

```
G29
```

Finally remember to store the settings to the printer's EEPROM

```
M500
```

