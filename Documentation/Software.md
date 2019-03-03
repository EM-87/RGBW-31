# Software Instrucctions

This its a brief revision of the serial commands and other input methods

## Serial commands:

#### help:
```
__________________________________________________
|                - RGBW v4.0 -                   |
|________________________________________________|
|Commands:                                       |
|    onoff   allon            alloff             |
|    data    cycle            resetsettings      |
|    help    savecolor[1-8]   callcolor[1-8]     |
|    wt      levelw[0-100]    lramp[0-10000]     |
|    rt      levelr[0-100]    lcramp[0-10000]    |
|    gt      levelg[0-100]    lstay[0-30000]     |
|    bt      levelb[0-100]    ldimm[0-99]        |
|                                                |
|Tuners:                                         |
|      r+         g+          b+         w+      |
|      r-         g-          b-         w-      |
|     stay+      ramp+      cramp+      rgb+     |
|     stay-      ramp-      cramp-      rgb-     |
|                                                |
|Colors:                                         |
|  red   ltgreen  green   magenta  cyan  white   |
|  blue  ltblue   orange  rgbwhite gold  violet  |
|________________________________________________|
```
Provides this help frame with all the commands.

#### onoff:
Turn off fast and turn on to the last color.

#### allon:
All colors on to the higest level.

#### alloff:
All colors off.

#### data:
```
__________________________________________________
| Data:                                          |
|   White    |    Red    |   Green   |   Blue    |
|     0      |     255   |     0     |    255    |
|     0%     |     100%  |     0%    |    100%   |
|  - - - - - - - - - - - - - - - - - - - - - -   |
|     Ramp      |   Cycle Ramp   |  Cycle Stay   |
|     300       |      1500      |     2000      |
|________________________________________________|
```
Show this data frame.
#### cycle:
Start/Stop the cycle mode. It change the color from the 8 memory colors. It gives this frame:
```
__________________________________________________
|                   Cycle Mode                   |
|                       On                       |
|________________________________________________|
```

#### resetsettings:
:warning: This reset all setings to the factory settings.

#### savecolor:
Save the current color to the desired position:
```
savecolor 4
```

#### callcolor:
Call the selected color:
```
callcolor 4
```

#### wt, rt, gt, bt:
Color toogle, it switch the selected channel.

#### levelw, levelr, levelg, levelb:
Level input, use to set a desired level in %:
```
levelw 74
```
It gives the next frame:
```
__________________________________________________
|              White Level:74%                   |
|________________________________________________|
```
Can be setted from 0 to 100.

#### lramp:
Level ramp, use to set a desired time in ms:
```
lramp 300
```
It gives the data frame updated. Can be setted from 0 to 10000.

#### lcramp:
Level cycle ramp, use to set a desired time in ms:
```
lcramp 300
```
It gives the data frame updated. Can be setted from 0 to 10000.

#### lstay:
Level cycle stay, use to set a desired time in ms:
```
lstay 300
```
It gives the data frame updated. Can be setted from 0 to 30000.

#### ldimm:
Level dimmer, use to set a desired level in %, it gives the data frame updated. 
On cycle mode it gives this data frame:
```
__________________________________________________
| Data:                                          |
|   White    |    Red    |   Green   |   Blue    |
|     0      |     200   |     0     |    200    |
|     0%     |     78%   |     0%    |    78%    |
|  - - - - - - - - - - - - - - - - - - - - - -   |
|     Ramp      |   Cycle Ramp   |  Cycle Stay   |
|     300       |      1500      |     2000      |
|  - - - - - - - - - - - - - - - - - - - - - -   |
|                   Cycle On                     |
|                   Dimm:50%                     |
|________________________________________________|
```


#### w+/- r+/- g+/- b+/-:

Increment/decrement the selected color

#### stay+/-:

Increment/decrement cycle stay time.

#### ramp+/-:

Increment/decrement ramp time.

#### cramp+/-:

Increment/decrement cycle ramp time.

#### rgb+/-:

Increment/decrement all colors.

#### red:

Set red color (r100%)

#### blue:

Set blue color (b100%)

#### green:

Set green color (g100%)

#### cyan:

Set cyan color (g100% b100%)

#### magenta:

Set magenta color (r100% b100%)

#### gold:

Set yellow color (g100% g100%)

#### orange:

Set orange color (g100% g14%)

#### violet:

Set violet color (r65% b100%)

#### ltgreen:

Set ltgreen color (g100% b9%)

#### ltblue:

Set ltblue color (g74% b100%)

#### white:

Set white color (w100%)

#### rgbwhite:

Set rgb white color (r100% g100% b100%)

## Buttons:

Buttons have two push modes, short and long press:
Button 1 on short press use the `onoff` comand, showing the next frame
```
__________________________________________________
|                       On                       |
|________________________________________________|
```
On long press use the `wt` comand, showing the next frame
```
__________________________________________________
|                   White toggle                 |
|                       On                       |
|________________________________________________|
```
Button 2 on short press change trougth the seven color mode, showing the next frame:
```
__________________________________________________
|                    Mode:1                      |
|________________________________________________|
```
On long press use the `cycle` comand, showing the next frame
```
__________________________________________________
|                   Cycle Mode                   |
|                       On                       |
|________________________________________________|
```

## IR Remote
When a signal is recived this frame appears:
```
__________________________________________________
|               IR Signal recived                |
|________________________________________________|

```
The IR functions are limited to the folowing commands:
* w+/- / r+/- / g+/- / b+/-
* wt / rt / gt / bt
* alloff
* allon
* rgb+/-
* cycle
* cramp+/-
* stay+/-
* ramp+/-
* onoff
* red
* green
* blue
* cyan
* gold
* magenta
* violet
* ltgreen
* ltblue
* orange
* rgbwhite

## Code adaptation

### IR codes:
To set youre own IR controller add this code to the line 128:
```
Serial.println(F("__________________________________________________"));
Serial.println(F("| IR Signal detected:                            |"));
Serial.print(F("|           "));
Serial.print(results.value, HEX);
Serial.print(F(" | "));
Serial.println(remval);
Serial.println(F("|________________________________________________|"));
```
It gives a frame like this trougth serial:
```
__________________________________________________
| IR Signal detected:                            |
|           1CE3D02F | -12241                    |
|________________________________________________|

```
### Serial supresion:
Serial console uses 49% of the memory, so if you want to add mayor changes on an Atmega 328 without using USB functions supress it.

### EEPROM Maping:
* 1 hr
* 2 hg
* 3 hb
* 4 hw
* 5 onoff flag
* 6 cycledim
* 7 mode
* 8 cyclego
* 9 first use flag
* 10-13 color 1
* 14-17 color2
* 18-21 color3
* 22-25 color4
* 26-29 color5
* 30-33 color6
* 34-37 color7
* 38-41 color8
* 42-45 ramp
* 46-49 cycleramp
* 50-53 stay

| Sector |    Function    |
| :----: | :------------- |
|   1    |       hr       |
|   2    |       hg       |
|   3    |       hb       |
|   4    |       hw       |
|   5    |   onoff flag   |
|   6    |    cycledim    |
|   7    |      mode      |
|   8    |    cyclego     |
|   9    | first use flag |
| 10-13  |    color 1     |
| 14-17  |    color 2     |
| 18-21  |    color 3     |
| 22-25  |    color 4     |
| 26-29  |    color 5     |
| 30-33  |    color 6     |
| 34-37  |    color 7     |
| 38-41  |    color 8     |
| 42-45  |      ramp      |
| 46-49  |   cycleramp    |
| 50-53  |      stay      |


## Built With

* [EEPROM](https://github.com/Chris--A/EEPROM) - *EEPROM Memory Library* - [Christopher Andrews](https://github.com/Chris--A)
* [Adafruit_NeoPixel](https://github.com/adafruit/Adafruit_NeoPixel) - *WS2812 Library* - [James Fowkes](https://github.com/jamesfowkes)
* [IRremote](https://github.com/z3t0/Arduino-IRremote) - *IR Library* - [Ken Shirriff](https://github.com/z3t0)


## Authors

* **Jeremy Saglimbeni** - *Initial work* - [jersagfast](https://github.com/jersagfast/)
* **Eduardo Martínez** - *Current version* - [EM-87](https://github.com/EM-87/)

## License

This project is licensed under ©Copyright License. Ask for permisions.

[:back: Back to Readme](https://github.com/EM-87/RGBW-Analog-Digital-LED-Controller)
