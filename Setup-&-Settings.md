If you have successfully installed OctoDash and need help during the initial setup or don't know what that one setting is. There are also instructions on how to setup OctoDash without a Keyboard are at the [bottom](#setup-without-keyboard).

## Restarting OctoDash without restarting the Raspberry Pi
If you want to quickly restart OctoDash you can just execute the following commands to do exactly that without the need to restart the whole Raspberry Pi:
- `service getty@tty1 stop`
- `service getty@tty1 start`

## Inputs & Settings explained
All the settings - briefly explained. Settings marked with *no-ui* cannot be changed via the UI, thus need to be edited by modifying `.config/octodash/config.json`.

#### OctoPrint URL
The URL or IP where your OctoPrint installation is located. If you've installed OctoDash on the same device as OctoPrint you should use `localhost` or `127.0.0.1` here.

default: `localhost`

#### OctoPrint Port
The port of your OctoPrint API. If you're using `localhost` or `127.0.0.1` you should use `5000` here. If you use the OctoPi image and have a different URL use `80`. Otherwise use the port of your forward proxy.

default: `5000`

#### API KEY
The API Key for the OctoPrint API. Maybe also called Application Key or Access Token. Learn how to get one [here](https://octoclient.zendesk.com/hc/en-us/articles/360007208474-Where-to-Find-the-API-Key). **ONLY use the API Key here and nowhere else. If you share your config please remove the Access Token**

*no-ui*

default: ` `

#### Printer Name
The name of your printer, which will be displayed in the bottom left corner. Leave empty if you don't want to show a name.

default: ` `

#### Printer XY-Speed
The speed in mm/s which will be used by OctoDash to move the X and Y-Axis in the control screen.

default: `150`

#### Printer Z-Speed
The speed in mm/s which will be used by OctoDash to move the Z-Axis in the control screen.

default: `5`

#### Default Hotend Temperature
The temperature in °C that will be used as the default for heating up the nozzle for changing the filament and if you click on the nozzle, while the printer is idling.

default: `200`

#### Default Heatbed Temperature
The temperature in °C that will be used as the default if you click on the heatbed, while the printer is idling.

default: `60`

#### Default Fanspeed
Fan speed in % that will be used as the default if you click on the fan, while the printer is idling.

default: `100`

#### Use M600 to change Filament
When this is enabled OctoDash won't extrude any Filament, but rather will send the M600 command to the printer after heating up the nozzle. This then allows to use the printers filament change process.

default: `false`

#### Purge Distance
The amount of filament that should be pushed through the nozzle to clean out the old filament.

default: `30`
#### Feed Length
The distance the filament needs to travel between the Extruder and the Hotend. This will be used for the Filament Change Process. Make sure to set this fairly accurate (± 10mm). For a standard Ender-3 Pro this 440mm works great. This value should be fairly short for direct drive extruders. If you're unsure about your measurement, it is better to start with a smaller than measured value and slowly increase until enough filament is retracted / extruded.

default: `0`
default: `470`

#### Feed Speed
The speed that should be used to unload, and load the first 75% of the Filament. Make sure to also set a higher or equal max axis speed in OctoPrint, as otherwise OctoPrint might slow down the Extruder Movement.

default: `30`

#### Feed Speed Slow
The speed that should be used to load the last 20% of the Filament.

default: `3`

#### Filament Thickness
The thickness of the filament you're using in mm. Should be `1.75` or `3` in most cases. Will be used to calculate the filament amount.

default: `1.75`

#### Filament Density
The average density of the filaments you're printing in g/cm³. Will be used to calculate the filament amount.

default: `1.25`

#### Z-Step G-CODE
The command that is used to for babystepping Z. The value will be appended to the end of the command - so `M290 Z` will result in `M290 Z0.01`.

*no-ui*
default: 'M290 Z'

#### Value Refresh Interval
The interval which OctoDash waits between asking OctoPrint for new information in ms. Shouldn't be too short (< 1000ms) to prevent unnecessary load.

*no-ui*
default: `2000`

#### Touchscreen
Whether you're using a touchscreen or not. Based on this selection different screens will be loaded.

*no-ui*
default: `true`

#### Turn Screen Off While Sleeping
Turn the screen off after 5 minutes, if OctoDash is sleeping. Only working for displays that support dpms (i.e. official Raspberry Pi Display). The screen will turn back on, once touched.

default: `false`

#### Sort Files by
The default attribute to sort files by (can always be temporarily changed in the file view, by clicking sort in the top right corner).

default: `name`

#### Sort Files order
Whether to sort ascending or descending.

default: `asc`

#### Custom Actions
Define up to 6 Custom Actions more info [here](https://github.com/UnchartedBull/OctoDash/wiki/Custom-Actions)

#### Display Layer Progress enabled
*Can't be changed at the moment*
Whether the Display Layer Progress Plugin is installed and enabled.

default: `true`

#### Enclosure Plugin enabled
Whether the Enclosure Plugin is installed and enabled.

default: `false`

#### Enclosure Plugin Ambient Sensor
The id of the sensor, whose values should be used.

default: ` `

#### Filament Manager Plugin enabled
Whether the Filament Manager Plugin is installed and enabled.

default: `true`

#### Preheat Button Plugin enabled
Whether the Preheat Button Plugin is installed and enabled.

default: `true`

#### Print Time Genius Plugin enabled
Whether the Print Time Genius Plugin is installed and enabled.

default: `true`

#### PSU Control Plugin enabled
Whether the PSU Control Plugin is installed and enabled.

default: `false`

#### PSU Control Plugin Turn on PSU when exiting sleep
Whether to send an on-signal to the PSU Control Plugin when OctoDash is exiting sleep mode.

default: `false`

## Settings file
You can also edit these settings with your favorite code editor. The settings file is located at `~/.config/octodash/config.json`

## Setup without Keyboard

Don't have a keyboard connected to your Raspberry Pi? No problem.

### Send Keyboard input to Pi via SSH
You can use [xdotool](https://theembeddedlab.com/tutorials/simulate-keyboard-mouse-events-xdotool-raspberry-pi/) to send keyboard input to the Pi via SSH. This is the recommended method, as your config will be validated by OctoDash and tested if the connection works.

#### Click locations
Here are all the locations of the different buttons & checkboxes. You can use those to do the whole setup via xdotools: `xdotool mousemove x,y click 1`, just replace x and y with the values for your screen size.
Below are listed the click locations for 800x480 (first) and 480x320 (second), if you're using a different screen size adjust them accordingly.

- next: `660,40 | 395,25`
- back: `130,40 | 80,25`

- Printer Name: `530,230 | 320,150`
- Filament Diameter: `270,380 | 160,250`
- Filament Density: `620,380 | 370,250`
- Host: `400,230 | 240,150`
- Port: `690,230 | 410,150`
- API Key: `530,340 | 320,220`
- Touchscreen Checkbox: `245,175 | 150,115`
- Value Refresh Interval: `570,280 | 340,185`
- Display Layer Progress Checkbox: `80,170 | 50,110`
- Enclosure Checkbox: `530,170 | 320,110`
- Filament Manager Checkbox: `70,260 | 40,170`
- Preheat Button Checkbox: `450,260 | 270,170`
- Print Time Genius Checkbox: `100,350 | 60,230`
- PSU Control Checkbox: `480,350 | 290,230`
- done: `420,420 | 250,270`

### Creating the config manually
*You need to know what you are doing if you face any errors please delete your config and try setting it up with xdotools*

Copy the `sample.config.json` from this repo to `.config/octodash/config.json` and then adjust the values to your needs. Most of the parameters should be pretty safe explanatory. If you have questions about variable types please have a look at [this file](https://github.com/UnchartedBull/OctoDash/blob/master/src/app/config/config.service.ts#L155). After a restart, OctoDash should pick up to new config file.