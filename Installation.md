You can install OctoDash [automaticly](#automatic-installation) with a script or [manually](#manual-installation) if you don't trust the script (which is open source and can be inspected in the `scripts` folder). If your setup differs from the normal Raspbian / OctoPi Installation you may want to go the manual way as well.

## Automatic Installation

The automatic scripts are meant to be run on Raspbian with OctoPrint located at the default location (`~/OctoPrint`) and the virtual environment named `venv`. If you use the OctoPi image you're good to go!

### With automatic start on boot

*Note: If you already have a Desktop Environment installed (i.e. you have a desktop and not only a console on the screen), you may want to use the version without automatic start on boot, as this script will override your Window Manager.*
```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/install.sh | bash -s -- --ptg
```

### Without automatic start on boot
```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/install-no-autostart.sh | bash -s -- --ptg
```

### Plugins
*DisplayLayerProgress is mandatory and needs to be installed for OctoDash to work. There are plans to make this optional, but currently, you need to have it installed.*

OctoPrint supports the following plugins:

- [DisplayLayerProgress](https://plugins.octoprint.org/plugins/DisplayLayerProgress/) - mandatory
- [Preheat Button](https://plugins.octoprint.org/plugins/preheat/) - adds a preheat button to OctoDash
- [Enclosure](https://plugins.octoprint.org/plugins/enclosure/) - adds support for a temperature display at the bottom of the screen
- [PSUControl](https://plugins.octoprint.org/plugins/psucontrol/) - adds the option to turn on the printer if exiting from sleep mode
- [UltimakerFormatPackage](https://plugins.octoprint.org/plugins/UltimakerFormatPackage/) - adds thumbnail images for .ufp files within OctoDash
- [PrintTimeGenius](https://plugins.octoprint.org/plugins/PrintTimeGenius/) - will greatly improve print time predictions

### Autologin
If you want OctoDash to show up directly on the screen after each boot, please make sure, that you enable Console Autologin with `sudo raspi-config`. **This will grant full access to everyone with physical access to the Raspberry Pi.**


## Manual Installation
You need to manually install the DisplayLayerProgress Plugin by OllisGit via the OctoPrint UI to enable the full functionality of OctoDash. You can also install the optional plugins listed [here](#pluings).

### Download and Install OctoDash

- Install Dependencies  
`sudo apt install libgtk-3-0 libnotify4 libnss3 libxss1 libxtst6 xdg-utils libatspi2.0-0 libuuid1 libappindicator3-1 libsecret-1-0 gir1.2-gnomekeyring-1.0`
- Download the latest release *Check for newer version and replace v2.0.0 with the latest version (Releases)*  
`wget -O octodash.deb https://github.com/UnchartedBull/OctoDash/releases/download/v2.0.0/octodash_2.0.0_armv7l.deb`
- Install the app  
`sudo dpkg -i octodash.deb`

### Start OctoDash Automatic on Boot

This is a minimal install to just display OctoDash on Raspbian LITE. It keeps the load on the Pi quite low and improves start-up time. If you use another Window Manager adjust your files according to the Documentation.

- Enable pi Console Autologin via  
`sudo raspi-config`
- Install xorg + ratpoison  
`sudo apt install xserver-xorg ratpoison x11-xserver-utils xinit libgtk-3-0`
- Create the .xinitrc file  
`nano ~/.xinitrc`
- Add the following contents:
```
    #!/bin/sh

    xset s off
    xset s noblank
    xset -dpms

    ratpoison&
    octodash
```
- make the file executable  
`sudo chmod +x .xinitrc`
- make xinit autostart on boot  
`nano ~/.bashrc`
  - add the following at the very bottom:
  ```
  if [ -z "$SSH_CLIENT" ] || [ -z "$SSH_TTY" ]; then
      xinit -- -nocursor
  fi
  ```
- reboot

## Setup without Keyboard

Don't have a keyboard connected to your Raspberry Pi? No problem.

### Send Keyboard input to Pi via SSH
You can use [xdotool](https://theembeddedlab.com/tutorials/simulate-keyboard-mouse-events-xdotool-raspberry-pi/) to send keyboard input to the Pi via SSH. This is the recommended method, as your config will be validated by OctoDash and tested if the connection works.

### Creating the config manually
*You need to know what you are doing if you face any errors please delete your config and try setting it up with xdotools*

First, you need to copy the `sample.config.json` from this repo to `.config/octodash/config.json` and then adjust to your needs. Most of the parameters should be pretty safe explanatory. If you have questions about variable types please have a look at [this file](https://github.com/UnchartedBull/OctoDash/blob/master/src/app/config/config.service.ts#L155). After a restart, OctoDash should pick up to new config file and work normally (or show you an error message, which you need to fix ;))

## Website (deprecated)

The OctoDash Website Support was dropped in v1.1.0. It is still possible, you need to figure out some things yourself, though. The app will automatically detect a normal Browser Environment and will try to load `assets/config.json`.  
The Project can be build using the Angular CLI and can be served via any WebServer.