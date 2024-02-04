# Linear Heater Control
This config allows you to linearly control the heating or cooling of a heater in Klipper.

The most common use case would be to control the temperature of the heated bed during cooling to prevent warping in materials such as ABS/ASA/etc.
The bed temperature can be slowly/linearly cooled over time allowing the material to release internal stresses and cool uniformly.

## Macro Information
### Macro Name: 
    LINEAR_HEATER_CONTROL

### Macro Arguments:

| Argument  | Unit | Data Type | Default Value | Description |
| --------  | :---: | :------: | :-----------: | ----------- |
| HEATER  | n/a | String | heater_bed | The name of the heater you would like to control (ie. heater_bed or extruder). |
| TARGET  | °C | float | 0 | The desired final temperature. This is what the heater will be set to when the macro ends control. |
| TRANSITION_RATE  | °C/min | float | 1.3 | The desired rate of temperature change of the heater (if achievable). |
| COOLING_ABORT_DELTA  | °C | float | 1.5 | The control will terminate early if TRANSITION_RATE exceeds the natural cooling rate (measured temp - control temp > COOLING_ABORT_DELTA). Only during cooling. |
| REFRESH_TIME  | sec. | float | 5 | Duration of time between control actions (ie. 5s --> 12Hz update freq.) |

## Examples:
Calling the macro with default parameters:

    LINEAR_HEATER_CONTROL

Calling the macro with a custom transition rate:

    LINEAR_HEATER_CONTROL TRANSITION_RATE=1.0

Calling the macro with a custom heater name and transition rate:

    LINEAR_HEATER_CONTROL HEATER="extruder2" TRANSITION_RATE=1.0

Using the macro in your END_GCODE (example):

    ...
    SET_HEATER_TEMPERATURE HEATER=extruder TARGET=0     ;Turn off the extruder heater
    LINEAR_HEATER_CONTROL                               ; Controlled Cooldown Bed
    M107                                                ; turn off fan
    G90                                                 ; absolute positioning
    G0 X5 F3600                                         ; park nozzle
    M84                                                 ; Turn off steppers
    ...

## Disclaimer

> [!WARNING]
> Use this macro responsibly.
> 
> YOU are responsible for ensuring the safety of your printer and the commanded temperatures.
> 
> Do not operate your printer un-attended.
