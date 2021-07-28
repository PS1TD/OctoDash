You can update OctoDash easily from within the app or with either [a script](#update-with-script) or [manually](#manual-update).

If you update multiple versions at a time you could encounter some issues. Manually update one version at a time, if you want to be on the safe side.

## In-App Update
OctoDash also supports In-App updates (v2.0 and up). This requires some initial setup though, which can be either done manually or automatically during installation. 

Since every package installation requires root privileges you need to set up a script for the installation and enable passwordless sudo for that specific script. Please note that this is a slight security compromise since that script allows anyone with access to the pi (even with no sudo access) to install the package located at `/tmp/octodash.deb`. So technically someone could copy a malicious package to that location and install it without any elevated rights. 

While this is a fairly small security risk for most users, if even one at all, please keep this in the back of your mind, especially if multiple users are working on the machine that is running OctoPrint.

Manual Setup:

- Create the update script `~/scripts/update-octodash` with the following contents:
```
#!/bin/bash

dpkg -i /tmp/octodash.deb
rm /tmp/octodash.deb
```
- Make the script executable:  
`sudo chmod +x ~/scripts/update-octodash`
- Enable passwordless sudo for the update script (`/etc/sudoers.d/update-octodash`):
```
pi ALL=NOPASSWD: /home/pi/scripts/update-octodash
```
- In-App update should work now (once a new version is available)

##  Update with Script
If you want to check out the script have a look in the `scripts` folder.

```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/update.sh | bash
```

## Manual Update
- Download the latest release. *Check for newer version (Releases) and replace v2.0.0 with the latest version*  
`wget -O octodash.deb https://github.com/UnchartedBull/OctoDash/releases/download/v2.0.0/octodash_2.0.0_armv7l.deb`
- Install the app  
`sudo dpkg -i octodash.deb`
- Reboot (or Restart OctoDash)