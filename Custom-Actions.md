OctoDash allows you to define custom actions, that can be executed from the control menu. You have full power over these buttons, OctoDash won't check, whether your commands make sense or if they might destroy your printer, it will send them to the printer, without any questions asked. So please be careful and do this at your own risk!

## Configuring Custom Actions
You can configure six actions from the settings UI. 

From v2.1.2 on OctoDash supports an unlimited amount of Custom Actions. Just add more by adding them to the `config.json` file (more info [here](https://github.com/UnchartedBull/OctoDash/wiki/Setup-&-Settings#manually-adjusting-the-settings)). 

If you have more than six actions defined the Custom Actions bar will be scrollable with the usual hold and drag functionality (there will be no scrollbar visible).

```
"customActions": 
[{
    "icon": string,
    "command": string,
    "color": string
},
...
```
You can change the [Icon](#icon), as well as the [Color](#color) of the box. Each icon can execute one or many [GCode](#gcode) commands or one of the [Predefined Actions](#predefined-actions). You can't combine Predefined Actions and GCode.

### GCode

If you want to execute GCode just put the commands inside the `command` attribute of the JSON. If you want to execute multiple GCode commands separate them with `; ` (the space at the end is important). Any GCode that your printer accepts will work here.

```
...
"command": "M140 S50; M104 S185",
...
```

### Predefined Actions

OctoDash supports a number of predefined actions, which aren't achievable with GCode. Please copy and paste the complete Action command attribute to prevent any spelling mistakes. The brackets and exclamation marks need to be copied as well. These commands will be executed even while you're printing and can cancel your print.

- `"command": "[!STOPDASHBOARD]"` - Stops OctoDash and closes the window
- `"command": "[!DISCONNECT]"` - Disconnects OctoPrint from the printer
- `"command": "[!RELOAD]"` - Restarts OctoPrint
- `"command": "[!SHUTDOWN]"` - Shuts down the Raspberry Pi
- `"command": "[!REBOOT]"` - Reboots the Raspberry Pi
- `"command": "[!KILL]"` - Nothing special yet, executes [!SHUTDOWN]
- `"command": "[!POWEROFF]"` - Turn off the PSU ([PSUControl](https://plugins.octoprint.org/plugins/psucontrol/) required)
- `"command": "[!POWERON]"` - Turn on the PSU ([PSUControl](https://plugins.octoprint.org/plugins/psucontrol/) required)
- `"command": "[!POWERTOGGLE]"` - Toggle the PSU ([PSUControl](https://plugins.octoprint.org/plugins/psucontrol/) required)
- `"command": "[!WEB]<website>"` - Opens the specified webpage in a fullscreen iFrame Window
- `"command": "[!NEOPIXEL]<identifier>,<red>,<green>,<blue>"` - Sets the LED strip to the specified color via the Enclosure Plugin. Make sure to include the `,`
- `"command": "[!OUTPUT]<identifier>,<status>"` - Sets the status of the specified output via the Enclosure Plugin (on / true turns output ON, off / false turns the output OFF). Make sure to include the `,`
- `"command": "[!OUTPUT_PWM]<identifier>,<duty-cycle>"` - Sets the duty cycle of the specified output via the Enclosure Plugin . Make sure to include the `,`
```
...
"command": "[!RELOAD]",
...
-- or --
...
"command": "[!WEB]http://localhost:5000",
...
```


### Icons

You can use any Icon of the [FontAwesome Free Solid Icon Collection](https://fontawesome.com/icons?d=gallery&s=solid&m=free). Don't prefix the icon, just paste in the name.

```
...
"icon": "print",
...
```

### Color

Any Hex Color will work here (please include the `#` upfront). If you want to use the same colors as the rest of the system check out the [FlatUI British Palette](https://flatuicolors.com/palette/gb). Most of the colors used across OctoDash come from that very same palette. However, feel free to experiment!

```
...
"color": "#f5f6fa",
...
```