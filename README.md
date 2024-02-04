This config allows you to linearly control the heating or cooling of a heater in Klipper.

The most common use case would be to control the temperature of the heated bed during cooling to prevent warping in materials such as ABS/ASA/etc.
The bed temperature can be slowly/linearly cooled over time allowing the material to release internal stresses and cool uniformly.

Macro Name: LINEAR_HEATER_CONTROL

Macro Arguements:

    HEATER: 
      Data Type: string
      Default Value: "heater_bed"
      Unit: n/a
      Description: The name of the heater you would like to control (ie. heater_bed or extruder).
      
    TARGET:
      Data Type: float
      Default Value: 0
      Unit: Degree Celsius
      Description: The desired final temperature. This is what the heater will be set to when the macro ends control.
      
    TRANSITION_RATE:
      Data Type: float
      Default Value: 1.3
      Unit: Degree Celsius/min
      Description: The desired rate of temperature change of the temperature (if achievable).

    COOLING_ABORT_DELTA:
      Data Type: float
      Default Value: 1.5
      Unit: Degree Celsius
      Description: The control will terminate early if TRANSITION_RATE is exceeds the natural cooling rate (measured temp - control temp > COOLING_ABORT_DELTA). Only during cooling.

    REFRESH_TIME:
      Data Type: float
      Default Value: 5
      Unit: Seconds
      Description: The frequency that the control is executed. 
