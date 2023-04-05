# klipper-macros
Collection of useful macros for klipper


## Summary
This repo contains a collection of klipper macros I have found useful, mainly for tuning printers and new filaments. 
Some macros have come from other repos or have been inspired from various g-code generators. 
Each macro will be attributed to the original source where open source code has been used. If any attribution is incorrect please let me know so I can resolve.

## Disclaimer
While all of the macros included within this repo have caused no harm to any of my 3D printers, person and surroundings, I cannot gurantee you the same sucess. 
These macros all come with the warning that there is always the potential to damage your printer and/or surroundings and person.
Therefore by installing and executing any of the macros in this repro you take full responsibility for their actions.
In other words if any of these macros danamge your printer, cause a fire or injury I take no responsibility.

As always when running macros from the internet, you should asses the source code to check ther should be no issues with your particular setup.
Also make sure that when you run any macro that you closely monitor the printer and be prepared to shutdown the printer should any issues arise.


## Installation
Installation is fairly simple. 

1. ssh into your klipper host
2. `cd` to your klipper config directory (usually `~/printer_data/config` if kiauh was used to setup klipper)
3. create a new directory for these macros `mkdir klipper_macros`
4. `cd` into the new directory `cd klipper_macros`
5. clone this repo `git clone git@github.com:rosscon/klipper-macros.git . ` (dont forget to include the trailing '.')
6. add each macro you wish to use below to your printer.cfg `[include klipper_macros/<macro_filename>.cfg]` changing `<macro_filename>`



## Usage

### Retraction
Based on the gcode generator from [Teaching Tech](https://teachingtechyt.github.io/calibration.html#retraction) is a macro version from the gcode generated by the online tool.
The macro allows you to enter much of the same details as the online tool by defining values for each increment. 

To enable add `[include klipper_macros/tune_retraction.cfg]` to your printer.cfg

To use the macro you can either use the mainsail/fluid web gui or enter the below gcode into the console modifying the values for your particular test. Each value is fairly self explanitory as to which parameter is altered

```
TUNE_RETRACTION BED_START=60 BED=55 NOZZLE_START=220 NOZZLE=200 PA_START=1.0 A_DIST=1 B_DIST=1.5 C_DIST=2 D_DIST=2.5 E_DIST=3 F_DIST=3.5 A_SPEED=50.0 B_SPEED=50.0 C_SPEED=50.0 D_SPEED=50.0 E_SPEED=50.0 F_SPEED=50.0 A_SPEED_UNRETRACT=25.0 B_SPEED_UNRETRACT=25.0 C_SPEED_UNRETRACT=25.0 D_SPEED_UNRETRACT=25.0 E_SPEED_UNRETRACT=25.0 F_SPEED_UNRETRACT=25.0
```

#### Future plans
* Add a wrapper macro to allow defining start & increment values rather than individual values


### Pressure Advance (Tune)
A modified version of the pressure advance macro developed by [m0to](https://gist.github.com/m0to/d395d44fa412d9808e0130857ea74f0b). The version included here has been modified to work well for smaller 120x120mm build plates.

To enable add `[include klipper_macros/tune_pressure_advance.cfg]` to your printer.cfg

To use this macro you can either use the mainsail/fluid web gui or enter the below gcode into the console modifying the values for your particular test. Each value is fairly self explanitory as to which parameter is altered

```
TUNE_PRESSURE_ADV BED=70 NOZZLE=190 PA_START=0.5 PA_STOP=1.5 NZL=0.4
```

The macro will echo to the console will output instructions similar to below with instruction on how to calculate a pressure advance value based on which line has the best result. Note that the bottommost line is line 0.

```
Find best line and multiply it by (0.5 + (bestLine * 0.05) ) to find your PA setting.
```

### Pressure Advance (Set override)
An issue that can occur with klipper is in multiple extruder setups `SET_PRESSURE_ADVACE` may return an error due to being unable to infer which extruder queue to apply the advance value to. 
This can be particularly problematic for multi material prints where each filament used may need to set its own pressure advance value.

This macro simply overrides the klipper default `SET_PRESSURE_ADVACE` and executes the build in klipper command but with an `EXTRUDER` value defined.

To enable add `[include klipper_macros/set_pressure_advance.cfg]` to your printer.cfg and thats it!


### M600 Filament Change
TODO

### Timelapse
TODO


