# Linear Heater Control
This config allows you to linearly control the heating or cooling of a heater in Klipper.

The most common use case would be to control the temperature of the heated bed during cooling to prevent warping in materials such as ABS/ASA/etc.
The bed temperature can be slowly/linearly cooled over time allowing the material to release internal stresses and cool uniformly.

## Macro Information
### Macro Name: 
    LINEAR_HEATER_CONTROL

### Macro Arguements:
    HEATER:
        Description: The name of the heater you would like to control (ie. heater_bed or extruder).
        Data Type: string
        Default Value: "heater_bed"
        Unit: n/a
        
    TARGET:
        Description: The desired final temperature. This is what the heater will be set to when the macro ends control.
        Data Type: float
        Default Value: 0
        Unit: Degree Celsius

    TRANSITION_RATE:
        Description: The desired rate of temperature change of the heater (if achievable).
        Data Type: float
        Default Value: 1.3
        Unit: Degree Celsius/min

    COOLING_ABORT_DELTA:
        Description: The control will terminate early if TRANSITION_RATE exceeds the natural cooling rate (measured temp - control temp > COOLING_ABORT_DELTA). Only during cooling.
        Data Type: float
        Default Value: 1.5
        Unit: Degree Celsius

    REFRESH_TIME:
        Description: The frequency that the control is executed.
        Data Type: float
        Default Value: 5
        Unit: Seconds

### Examples:
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
