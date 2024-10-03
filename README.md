# Ender 3 Custom G-code

This repository contains custom G-code scripts for the Ender 3 3D printer. These scripts are designed to optimize the start and stop sequences of your prints, ensuring better print quality and machine longevity.

## Files

- **Start G-code**: This script prepares the printer for a new print job.
- **Stop G-code**: This script safely shuts down the printer after a print job is completed.

## Start G-code

```gcode
; Ender 3 Custom Start G-code
G92 E0 ; Reset Extruder
G28 ; Home all axes
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X0.1 Y20 Z0.3 F5000.0 ; Move to start position
G1 X0.1 Y200.0 Z0.3 F1500.0 E15 ; Draw the first line
G1 X0.4 Y200.0 Z0.3 F5000.0 ; Move to side a little
G1 X0.4 Y20 Z0.3 F1500.0 E30 ; Draw the second line
G92 E0 ; Reset Extruder
G1 Z2.0 F3000 ; Move Z Axis up little to prevent scratching of Heat Bed
G1 X5 Y20 Z0.3 F5000.0 ; Move over to prevent blob squish
```

### Description

- **G92 E0**: Resets the extruder position.
- **G28**: Homes all axes.
- **G1 Z2.0 F3000**: Moves the Z axis up slightly to prevent bed scratching.
- **G1 X0.1 Y20 Z0.3 F5000.0**: Moves to the start position.
- **G1 X0.1 Y200.0 Z0.3 F1500.0 E15**: Draws the first line.
- **G1 X0.4 Y200.0 Z0.3 F5000.0**: Moves to the side slightly.
- **G1 X0.4 Y20 Z0.3 F1500.0 E30**: Draws the second line.
- **G92 E0**: Resets the extruder position again.
- **G1 Z2.0 F3000**: Moves the Z axis up slightly to prevent bed scratching.
- **G1 X5 Y20 Z0.3 F5000.0**: Moves over to prevent blob squish.

## Stop G-code

```gcode
G91 ;Relative positioning
G1 E-2 F2700 ;Retract a bit
G1 E-2 Z0.2 F2400 ;Retract and raise Z
G1 X5 Y5 F3000 ;Wipe out
G1 Z10 ;Raise Z more
G90 ;Absolute positioning

G1 X0 Y{machine_depth} ;Present print
M106 S0 ;Turn-off fan
M104 S0 ;Turn-off hotend
M140 S0 ;Turn-off bed

M84 X Y E ;Disable all steppers but Z
```

### Description

- **G91**: Sets relative positioning.
- **G1 E-2 F2700**: Retracts the filament slightly.
- **G1 E-2 Z0.2 F2400**: Retracts the filament and raises the Z axis.
- **G1 X5 Y5 F3000**: Wipes the nozzle.
- **G1 Z10**: Raises the Z axis further.
- **G90**: Sets absolute positioning.
- **G1 X0 Y{machine_depth}**: Moves the print bed to the front for easy print removal.
- **M106 S0**: Turns off the fan.
- **M104 S0**: Turns off the hotend.
- **M140 S0**: Turns off the heated bed.
- **M84 X Y E**: Disables all steppers except for the Z axis.

## Usage

1. Copy the start G-code into your slicer's start G-code section.
2. Copy the stop G-code into your slicer's end G-code section.
3. Adjust `{machine_depth}` in the stop G-code to match your printer's bed depth.
