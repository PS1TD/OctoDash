You can update OctoDash easily with either [a script](#update-with-script) or [manually](#manual-update). Both versions should work on any installation. If you want to check out the script have a look in the `scripts` folder.

If you update multiple versions at a time you could encounter some issues. Manually update one version at a time, if you want to be on the safe side.

##  Update with Script

```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/update.sh | bash
```

## Manual Update
- Download the latest release. *Check for newer version (Releases) and replace v2.0.0 with the latest version*  
`wget -O octodash.deb https://github.com/UnchartedBull/OctoDash/releases/download/v2.0.0/octodash_2.0.0_armv7l.deb`
- Install the app  
`sudo dpkg -i octodash.deb`
- Reboot (or Restart OctoDash)