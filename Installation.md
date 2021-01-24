You can install OctoDash [automaticly](#automatic-installation) with the provided script or [manually](#manual-installation), if you don't trust the script (which is open source and can be inspected in the (here)[https://github.com/UnchartedBull/OctoDash/blob/feature/update-installation-script/scripts/install.sh]). If your setup differs from the normal Raspbian / OctoPi Installation it is preferred to do the manual installation.

## Automatic Installation

If you have questions during the initial setup - please consult the [setup guide](https://github.com/UnchartedBull/OctoDash/wiki/Setup-&-Settings).

*If you want the automatic start to work make sure to setup Autologin (described in the next section)*

```
bash <(wget -qO- https://github.com/UnchartedBull/OctoDash/raw/main/scripts/install.sh)
```

### Autologin
If you want OctoDash to show up directly on the screen after each boot, please make sure, that you enable Console Autologin with `sudo raspi-config` like so:

For newer Raspbian / OctoPi installations you need to select the following:
- `1 System Options` -> `S5 Boot / Auto Login` -> `B2 Console Autologin`

For older systems you need to select Console Autologin like this:
- `3 Boot Options` -> `B2 Console Autologin`

Finally select `<Finish>` and `<Yes>` if asked to reboot

**This will grant full access to everyone with physical access to the Raspberry Pi.**

## Manual Installation
You need to manually install the DisplayLayerProgress Plugin by OllisGit via the OctoPrint UI to enable the full functionality of OctoDash. You can also install other, optional plugins listed [here](https://github.com/UnchartedBull/OctoDash/wiki/Plugins).

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

### Update Script

Please have a look at [this section](https://github.com/UnchartedBull/OctoDash/wiki/Update#in-app-update) of the wiki.

## Website (deprecated)

The OctoDash Website Support was dropped in v1.1.0. It is still possible, you need to figure out some things yourself, though. The app will automatically detect a normal Browser Environment and will try to load `assets/config.json`.  
The Project can be build using the Angular CLI and can be served via any WebServer.