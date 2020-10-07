Common issues, that you may encounter are listed here, a fix, if available, will be there too. If you get an issue or error, that isn't listed here please open a [new issue](https://github.com/UnchartedBull/OctoDash/issues/new). Please make sure to fill out all the information, that is requested in the templates!

## Table of Contents

- [Installation](#installation)
  - [wget: missing URL](#wget-missing-url)
  - [getting errors during installaion](#errors-during-installation)
  - [not starting automatically](#not-starting-automatically)
  - [Cannot open virtual console 2](#cannot-open-virtual-console-2)
  - [Cannot open display, Xinit failing, ...](#cannot-open-display-xinit-failing-)
- [Setup](#setup)
  - [Host and Port](#host-and-port)
- [Usage](#usage)
  - [Config is invalid](#config-is-invalid)
  - [OctoDash isn't waiting for my board to fully boot](#octodash-isnt-waiting-for-my-board-to-fully-boot)
  - [Filament Change is slower than specified in configuration
](https://github.com/UnchartedBull/OctoDash/wiki/Troubleshooting#filament-change-is-slower-than-specified-in-configuration)

## Installation
Any errors, that you may encounter during the installation of OctoDash.

### wget: missing URL
#### Problem
You've most likely exceeded the GitHub Rate Limit, therefore the newest release can't be retrieved from the server.
#### Fix
Wait an hour until your Rate Limit gets reset.

### errors during installation
#### Problem
You are getting several errors during the installation of OctoDash.
#### Fix
Please update your software to the newest version first and try reinstalling

### not starting automatically
#### Problem
OctoDash is not starting automatically, even though you installed it via the normal script.
#### Fix
Make sure you are logged in (auto-login can be enabled with the [raspi-config](https://www.opentechguides.com/how-to/article/raspberry-pi/134/raspbian-jessie-autologin.html) tool). If that does not fix the issue make sure you can start OctoDash via the command `octodash` (you may need to execute `export DISPLAY=:0` and `ratpoison` beforehand).

### Cannot open virtual console 2
#### Problem
This issue comes up on some systems and prevents OctoDash from starting up correctly.
#### Fix
Fix the Xorg permission with `sudo chmod ug+s /usr/lib/xorg/Xorg` and restart your Raspberry

### Cannot open display, Xinit failing, ...
#### Problem
You ran the installing script and restarted your Pi, but rather than seeing OcotDash you're just getting some error messages or just a blinking cursor at the very top of your screen. 
#### Fix
This in many cases is a problem with the display setup and occurs with some of the displays. There are multiple (closed) issues to also look at.
First thing to do is to check, whether you installed the drivers for your display (these are **NOT** included with OctoDash) and run the install script again for good measure. 
If you are sure, that you have the correct drivers installed here are some other things to try (make sure to reboot after each step to see if it is working):
- Double Check that B2 is selected for the Boot Options in `raspi-config`
- Connect a display via HDMI to see if OctoDash is available on the screen connected via HDMI
- If you got a guide from your seller instructing you to change some settings (i.e. via `raspi-config`) - try just installing the driver without doing any of the subsequent steps listed in the guide.
- Try reconfiguring your x11 server: `sudo dpkg-reconfigure x11-common`
- Install additional packages, which my be needed for OctoPi distrobutions: `sudo apt install libpam0g-dev libx11-dev`
- Install even more packages: `sudo apt install raspberrypi-ui-mods` (please try the above first)
- Allow any user to use xinit: [Stackexchange](https://unix.stackexchange.com/questions/478742/error-when-trying-to-use-xorg-only-console-users-are-allowed-to-run-the-x-serve/529945#529945)
- Install Desktop Environment: `sudo /home/pi/scripts/install-desktop`

## Setup
Any errors, that you may encounter during the setup of OctoDash.

### Host and Port
#### Problem
If you're unsure what to enter in those fields or you're getting errors.

#### Fix
Always try `localhost` or `127.0.0.1` for the host and `5000` for the port if you're running OctoDash on the same machine as OctoPrint. For more information about those values visit the [setup guide](https://github.com/UnchartedBull/OctoDash/wiki/Setup-&-Settings).

## Usage
Any errors, that you may encounter during the usage of OctoDash.

### Config is invalid
#### Problem
You're getting a message, telling you that your config is invalid alongside with some weird technical-looking things. This can either happen if you upgrade to many versions at a time (I'm trying to merge configs from the previous release, if possible, so if you're upgrading from 1.4.0 to 1.4.1 you should be fine, but if you're going directly to 1.4.2 you might run into this error) 
#### Fix
If you're unsure about what the errors mean you can always just delete that file `rm ~/.config/octodash/config.json` and reboot your Pi. This will open the initial setup screen again and will create a new, valid config for you. **All your configuration data for OctoDash will be lost, OctoPrints data isn't touched.**

If you understand what needs to be changed in your config please go ahead and edit it with your favorite text editor. You can find the config at `~/.config/octodash/config.json`. 

If you want more information about the config / settings have a look [here](https://github.com/UnchartedBull/OctoDash/wiki/Setup-&-Settings).

### OctoDash isn't waiting for my board to fully boot
#### Problem
This issue can occur if your board is taking to long to boot up. OctoDash will try to connect 3 times in the time span of 15 seconds, which might not be enough for some boards to boot up.
#### Fix
Please try the fork of [OctoPrint PortLister](https://github.com/mikekscholz/OctoPrint-PortLister) by [@mikekschloz](https://github.com/mikekscholz).

### Filament Change is slower than specified in configuration
#### Problem
Even though the feed speed is setup correctly in OctoDash, the speed at which filament is retracted / extruded does not change during the filament change process
#### Fix
OctoPrint defines a maximum speed for each axis, which will overwrite the speed of any axis command with a higher speed. Please make sure to update your Printer Profile accordingly to your OctoDash configuration.