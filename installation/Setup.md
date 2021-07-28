OctoDash will start with an installation wizard when you first start it. The wizard will ask for some basic information and will establish the connection with your OctoPrint installation. If you're unsure about any values during setup - just leave them at their default value. You can change everything in the settings later.

## Setup without Keyboard

With the latest version there is no keyboard required to complete the initial installation. If you do want to adjust for example the printer name and don't have a keyboard connected to your Raspberry Pi you can use xdotool.

### Send Keyboard input to Pi via SSH

You can use [xdotool](https://www.semicomplete.com/projects/xdotool/) to send keyboard input to the Pi via SSH. This is the recommended method, as your config will be validated by OctoDash and tested if the connection works.

#### xdotools commands

- send text input: `xdotool type "<text>"`
- click somewhere: `xdotool mousemove <x> <y> click 1`

#### Click locations

Here are all the locations of the different buttons & checkboxes. You can use those to do the whole setup via xdotools: `xdotool mousemove x,y click 1`, just replace x and y with the values for your screen size.
Below are listed the click locations for 800x480 (first) and 480x320 (second), if you're using a different screen size adjust them accordingly.

- next: `660,40 | 395,25`
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

_You need to know what you are doing if you face any errors please delete your config and try setting it up with xdotools_

Copy the JSON from [here](https://github.com/UnchartedBull/OctoDash/blob/master/src/app/config/config.default.ts) (just copy the JSON part) to `.config/octodash/config.json` and then adjust the values to your needs. Most of the parameters should be pretty safe explanatory. If you have questions about variable types please have a look at [this file](https://github.com/UnchartedBull/OctoDash/blob/master/src/app/config/config.model.ts). After a restart, OctoDash should pick up to new config file.
