You can update OctoDash easily with either [a script](#update-with-script) or [manual](#manual-update). Both versions should work on any installation. If you want to check out the script have a look in the `scripts` folder.

##  Update with Script

```
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/update.sh | bash
```

## Manual Update
- Download the latest release *Check for newer version (Releases)*  
`wget -O octodash.deb https://github.com/UnchartedBull/OctoDash/releases/download/v1.1.0/octodash_1.1.0_armv7l.deb`
- Install the app  
`sudo dpkg -i octodash.deb`
- Reboot (or Restart OctoDash)