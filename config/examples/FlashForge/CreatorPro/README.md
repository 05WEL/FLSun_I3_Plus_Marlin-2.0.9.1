# NOTE ON FLASHING THE FIRMWARE:

The firmware for the Atmel chip used for USB on the Mighty Board is the same as the Arduino Mega's, but it doesn't do an automatic reset. If you want the printer to reset on DTR you will need to flash it with the firmware for the Arduino Mega.

### Use with all nozzle settings

- Build plate shape: Rectangular
- Origin at center
- Heated bed
- G-code flavor: Marlin

### Right Nozzle

- Number of Extruders: 1
- X (Width) 227
- Y (Depth) 148
- Z (Heigth) 150

## Extruder 1
- Nozzle size: 0.4
- Compatible material diameter: 1.75
- Nozzle offset X: 0
- Nozzle offset Y: 0
- Cooling Fan Number:0

```gcode
;START G-CODE;
M104 T0 S{material_print_temperature}
M140 S{material_bed_temperature}
G28
T0
G1 X150 Y-70 Z30 F4800 ; move to wait position left hand side of the table
M190 S{material_bed_temperature}
M109 T0 S{material_print_temperature}
G92 E0
G1 Z0.4 F1800
G1 X110 Y-70 E20 F300 ; purge nozzle
G1 X120 Y-70 Z0.15 F1200 ; slow wipe
G1 X110 Y-70 Z0.5 F1200 ; lift
G92 E0
;START G-CODE;

;END G-CODE;
G1 X150 Y75 Z150 F1000 ; send Z axis to bottom of machine
M140 S0; cool down HBP
M104 T0 S0 ; cool down right extruder
M104 T1 S0 ; cool down left extruder
M127 ; stop blower fan
M18 ; disable stepper
;END G-CODE;
```

## Left Nozzle
Number of Extruders: 1
X (Width) 227
Y (Depth) 148
Z (Heigth) 150

Extruder 1 -
    Nozzle size: 0.4
    Compatible material diameter: 1.75
    Nozzle offset X: -34
    Nozzle offset Y: 0
    Cooling Fan Number:0

```gcode
;START G-CODE;
M104 S{material_print_temperature}
M140 S{material_bed_temperature}
G28
T1
G1 X-110 Y-70 Z30 F4800 ; move to wait position left hand side of the table
M104 S{material_print_temperature}
M190 S{material_bed_temperature}
M109 S{material_print_temperature}
G92 E0
G1 Z0.4 F1800
G1 E10 F300 ; purge nozzle
G1 X-67 Y-70 E25 F300 ; purge nozzle
G1 X-77 Y-70 Z0.15 F1200 ; slow wipe
G1 X-67 Y-70 Z0.5 F1200 ; lift
G92 E0
;START G-CODE;

;END G-CODE;
G1 X150 Y75 Z150 F1000 ; send Z axis to bottom of machine
M140 S0; cool down HBP
M104 T0 S0 ; cool down right extruder
M104 T1 S0 ; cool down left extruder
M127 ; stop blower fan
M18 ; disable stepper
;END G-CODE;
```

## Both Nozzles
Number of Extruders: 2
X (Width) 295 <---- bed width + 2 x nozzle offset
Y (Depth) 148
Z (Heigth) 150

Extruder 1 -
    Nozzle size: 0.4
    Compatible material diameter: 1.75
    Nozzle offset X: 0
    Nozzle offset Y: 0
    Cooling Fan Number:0
    ;Extruder End G-code;
    G1 X150 Y70 F9000;move away from print in case extrusion cool down speed modifier too low
    ;Extruder End G-code;

Extruder 2 -
    Nozzle size: 0.4
    Compatible material diameter: 1.75
    Nozzle offset X: -34
    Nozzle offset Y: 0
    Cooling Fan Number:0
    ;Extruder End G-code;
    G1 X150 Y70 F9000;move away from print in case extrusion cool down speed modifier too low
    ;Extruder End G-code;

```gcode
;START G-CODE;
M104 T0 S{material_print_temperature, 0}
M104 T1 S{material_print_temperature, 1}
M140 S{material_bed_temperature}
G28
;purge right
T0
G1 X155 Y-70 Z30 F4800
M190 S{material_bed_temperature}
M109 T0 S{material_print_temperature, 0}
M104 T0 S{material_standby_temperature, 0}
G92 E0
G1 Z0.4 F1800
G1 X110 Y-70 E20 F300 ; purge nozzle
G1 X120 Y-70 Z0.15 F1200 ; slow wipe
G1 E17 F2400
G1 X110 Y-70 Z0.5 F1200 ; lift
G92 E0
;purge left
T1
;M104 T0 S{material_standby_temperature, 0}
M104 T1 S{material_print_temperature, 1}
G1 X-110 Y-70 Z30 F4800
M109 T1 S{material_print_temperature, 1}
G92 E0
G1 Z0.4 F1800
G1 X-67 Y-70 E25 F300 ; purge nozzle
G1 X-77 Y-70 Z0.15 F1200 ; slow wipe
G1 E22 F3600
G1 X-67 Y-70 Z0.5 F1200 ; lift
G92 E0
;START G-CODE;
;END G-CODE;
G1 X150 Y75 Z150 F1000 ; send Z axis to bottom of machine
M140 S0; cool down HBP
M104 T0 S0 ; cool down right extruder
M104 T1 S0 ; cool down left extruder
M127 ; stop blower fan
M18 ; disable stepper
;END G-CODE;
```
