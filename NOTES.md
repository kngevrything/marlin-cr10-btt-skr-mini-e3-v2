# Configuration Notes

These notes document the hardware assumptions, firmware configuration choices, and debugging decisions for my custom Marlin firmware build.

This firmware is specific to my Creality CR-10 V3 hardware configuration and should not be used on another printer without careful review.

## Printer Configuration

### Base Printer

- Creality CR-10 V3
- Stock direct drive extruder
- Stock display
- Manual bed leveling workflow

### Control Board

- BTT SKR Mini E3 V2.0
- Marlin 2.1.x firmware base
- Stock CR-10 display connected through EXP3

## Configuration Goals

The goal of this firmware configuration was to adapt Marlin to the upgraded control board while preserving the printer behavior I wanted for day-to-day use.

Primary goals:

- Support the BTT SKR Mini E3 V2.0 board
- Keep the stock CR-10 display working
- Enable manual mesh bed leveling
- Preserve EEPROM settings across restarts
- Restore leveling state after homing
- Configure filament runout detection
- Validate hotend and part cooling fan behavior
- Keep the configuration documented for future maintenance

## Key Marlin Features Enabled

### EEPROM Settings

EEPROM support is enabled so printer settings can be stored and reused across restarts.

Relevant behavior:

- Calibration values can be saved from the printer menu or terminal
- Mesh leveling data can persist after power cycles
- Configuration changes do not require constant reflashing when runtime values are adjustable

### Manual Mesh Bed Leveling

Manual mesh bed leveling is enabled instead of automatic probing.

Reason:

- The printer does not rely on an automatic bed probe
- Manual mesh leveling gives enough correction for this machine
- It keeps the hardware configuration simpler

Expected workflow:

1. Home the printer
2. Run the mesh leveling workflow
3. Save the mesh to EEPROM
4. Confirm the mesh is restored after future homing commands

### Restore Leveling After Homing

Leveling is restored after `G28` so the saved mesh remains active after homing.

Reason:

- Standard homing can disable leveling behavior
- Restoring leveling after homing makes print startup behavior more predictable
- It reduces the chance of accidentally printing without the saved mesh active

## Display Configuration

The stock CR-10 display is used with the upgraded control board.

Important notes:

- The stock display is connected through the EXP3 connector
- The single-cable EXP3 setup is expected for this configuration
- Display behavior should be validated after firmware changes

Validation steps:

- Confirm the screen powers on
- Confirm menu navigation works
- Confirm bed leveling menus are accessible
- Confirm EEPROM save/load options are available
- Confirm temperature and fan controls are visible and responsive

## Filament Runout Sensor

The filament runout sensor is configured through the board’s endstop-style input.

Important notes:

- The runout sensor is wired to the expected stop/input pin for this board configuration
- Pin behavior should be validated before relying on runout handling during long prints
- Sensor logic may need inversion depending on wiring and switch behavior

Validation steps:

1. Check printer state with filament inserted
2. Check printer state with filament removed
3. Confirm the firmware reports the expected triggered/open state
4. Confirm runout behavior does not falsely trigger during normal printing

## Fan and Thermal Behavior

Fan behavior should be validated any time board wiring or firmware pin configuration changes.

### Hotend Fan

The hotend fan should run as expected when the hotend reaches the configured temperature threshold, depending on wiring and firmware settings.

Validation steps:

- Heat the hotend to a normal operating temperature
- Confirm the hotend fan activates as expected
- Confirm the fan remains stable during heating

### Part Cooling Fan

The part cooling fan should respond to standard fan control commands.

Useful validation commands:

```gcode
M106 S255 ; full fan
M106 S128 ; half fan
M106 S0   ; fan off
