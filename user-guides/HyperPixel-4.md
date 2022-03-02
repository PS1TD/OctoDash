by [@morphias2004](https://github.com/morphias2004)

I loaded the latest OctoPi image, did the basic config on OctoPrint to get it on the network, ran apt update and upgrade, , ran all the updates on OctoPrint to bring it up to v1.6.1 and then ran:

`sudo apt install git`

`git clone https://github.com/pimoroni/hyperpixel4 -b pi4`

`cd hyperpixel4`

`sudo ./install.sh`

`sudo reboot now`

Log back in and then run

`sudo raspi-config`

System Options > Boot/Auto Login and enabled B1 Console and B2 Console Autologin

Rebooted

`cd /boot`

`sudo nano config.txt`

Edit the bottom so it looks like this:

```
[pi4]
# Enable DRM VC4 V3D driver on top of the dispmanx display stack
**#dtoverlay=vc4-fkms-v3d**
max_framebuffers=2
**display_lcd_rotate=3**

[all]
#dtoverlay=vc4-fkms-v3d
# enable raspicam
start_x=1
gpu_mem=128

dtoverlay=hyperpixel4
enable_dpi_lcd=1
dpi_group=2
dpi_mode=87
dpi_output_format=0x7f216
dpi_timings=480 0 10 16 59 800 0 15 113 15 0 0 0 60 0 32000000 6
```

Save and reboot and the screen will now be orientated with the USB C port at the bottom. If you want the port at the top, then you need to set **display_lcd_rotate=1**

The TOUCH function will still be incorrect, but to correct this:

`cd /usr/share/X11/xorg.conf.d`

`sudo nano 40-libinput.conf`

Edit the section for the touchscreen - it is normally the second last section - by adding this line:

```
Section "InputClass"
        Identifier "libinput touchscreen catchall"
        MatchIsTouchscreen "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        **Option "TransformationMatrix" "0 -1 1 1 0 0 0 0 1"**
EndSection
```

Leave all the spaces.

Save and reboot and your touch screen should now be orientated correctly the and touch screen also calibrated correctly. If you went with the USB C port at the top, then you need to make the line **Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"**

I do not claim credit for this solution. It's a combination of the following video and articles:

https://github.com/TxBillbr/octodash-hyperpixel-fix

https://www.youtube.com/watch?v=K0A-sIUBFfU&t=2015s

https://www.instructables.com/Rotate-Raspberry-Pi-Display-and-Touchscreen/
