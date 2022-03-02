OctoDash will start with an installation wizard when you first start it. The wizard will ask for some basic information and will establish the connection with your OctoPrint installation. If you're unsure about any values during setup - just leave them at their default value. You can change everything in the settings later.

## Setup without Keyboard

With the latest version there is no keyboard required to complete the initial installation. If you do want to adjust for example the printer name and don't have a keyboard connected to your Raspberry Pi you can use xdotool.

### Send Keyboard input to Pi via SSH

You can use [xdotool](https://www.semicomplete.com/projects/xdotool/) to send keyboard input to the Pi via SSH. This is the recommended method, as your config will be validated by OctoDash and tested if the connection works.

#### xdotools commands

- send text input: `xdotool type "<text>"`
- click somewhere: `xdotool mousemove <x> <y> click 1`

### Creating the config manually

_You need to know what you are doing if you face any errors please delete your config and try setting it up with xdotools_

Copy the JSON from [here](https://github.com/UnchartedBull/OctoDash/blob/master/src/app/config/config.default.ts) (just copy the JSON part) to `.config/octodash/config.json` and then adjust the values to your needs. Most of the parameters should be pretty safe explanatory. If you have questions about variable types please have a look at [this file](https://github.com/UnchartedBull/OctoDash/blob/master/src/app/config/config.model.ts). After a restart, OctoDash should pick up to new config file.
