You can install OctoDash [automatic](#automatic-installation) with a script or [manual](#manual-installation) if you don't trust the script (which is OpenSource and can be inspected in the `scripts` folder) or your setup differs from the normal Raspbian Installation. All scripts are written for the Raspberry Pi 2 (and higher). It is not recommended to install OctoDash on a Pi 1, because of the lack of power.

## Automatic Installation

The automatic scripts are meant to be run on Raspbian with OctoPrint located at the default location (`~/OctoPrint`) and the virtual environment named `venv`. If you use the OctoPi image you're good to go!

OctoPrint will install the following plugins by default:

- [DisplayLayerProgress](https://plugins.octoprint.org/plugins/DisplayLayerProgress/) - mandatory
- [PrintTimeGenius](https://plugins.octoprint.org/plugins/PrintTimeGenius/) - optional, will greatly improve TimePredictions can be enabled via the `--ptg` flag

### With automatic start on boot

*Note: If you already have a Desktop Environment installed (i.e. you have a desktop and not only a console on the screen), you may want to use the version without automatic start on boot, as this script will override your Window Manager.*
```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/install.sh | bash -s -- --ptg
```

### Without automatic start on boot
```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/install-no-autostart.sh | bash -s -- --ptg
```
## Manual Installation
You need to install the DisplayLayerProgress Plugin by OllisGit to enable the full functionality of OctoDash. The API is currently not in the final plugin, so please install the plugin with the following link: https://github.com/UnchartedBull/OctoPrint-DisplayLayerProgress/archive/master.zip.

### Download and Install OctoDash

- Download the latest release *Check for newer version and replace v1.0.0 with the latest version (Releases)*  
`wget -O octodash.deb https://github.com/UnchartedBull/OctoDash/releases/download/v1.0.0/octodash_1.0.0_armv7l.deb`
- Install the app  
`sudo dpkg -i octodash.deb`
- If you get an error while installing you may need to install the missing dependencies.  
`sudo apt install -f && sudo dpkg -i octodash.deb`

### Start OctoDash Automatic on Boot

This is a super-minimal install to just display OctoDash on Raspbian LITE. Good thing is, that it keeps the load and the Pi quite low and improves start-up time. If you use another window manager adjust your files according to the Documentation.

- Enable pi Console Autologin via  
`sudo raspi-config`
- Install xorg + ratpoison  
`sudo apt install xserver-xorg --no-install-recommends ratpoison x11-xserver-utils xinit`
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
- `nano ~/.bashrc`
- add the following at the very bottom:
```
if [ -z "$SSH_CLIENT" ] || [ -z "$SSH_TTY" ]; then
    xinit -- -nocursor
fi
```
- reboot


If you get the `Cannot open virtual console 2 (Permission denied)` error run `sudo chmod ug+s /usr/lib/xorg/Xorg` and reboot.

## Website (deprecated)

The OctoDash Website Support was dropped in v1.1.0. It is still possible, you need to figure out some things yourself, though. The app will automatically detect a normal Browser Environment and will try to load `assets/config.json`.  
The Project can be build using the Angular CLI and can be served via any WebServer.