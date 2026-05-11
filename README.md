# CR-10 V3 Custom Marlin Firmware

Custom Marlin firmware configuration for my Creality CR-10 V3 upgraded with a BTT SKR Mini E3 V2.0 control board.

This repo documents the firmware configuration, hardware assumptions, and debugging work used to adapt Marlin to my specific printer setup.

## Hardware

- Creality CR-10 V3
- BTT SKR Mini E3 V2.0
- Stock CR-10 display
- Stock direct drive extruder
- Filament runout sensor

## Configuration Goals

- Enable reliable firmware support for the upgraded control board
- Configure the stock CR-10 display through the EXP3 connector
- Support manual mesh bed leveling
- Preserve EEPROM settings for repeatable calibration
- Support filament runout detection
- Document hardware/software decisions for future troubleshooting

## Key Configuration Areas

- Marlin 2.1.x configuration
- Board and pin mapping
- LCD support
- Manual mesh bed leveling
- EEPROM settings
- Filament runout sensor configuration
- Fan and thermal behavior validation

## What This Demonstrates

This project demonstrates practical firmware configuration, hardware/software debugging, device behavior validation, and configuration management for a customized physical system.

## Important Warning

This firmware configuration is specific to my printer hardware and wiring. Do not flash it to another printer without reviewing the configuration and validating compatibility.

## Attribution

This repo is based on the open-source Marlin firmware project.

Marlin is maintained by the Marlin Firmware community:
https://marlinfw.org

The original Marlin source and licensing terms remain the property of their respective authors and contributors.
