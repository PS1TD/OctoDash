by [MrElie](https://github.com/MrElie) and [others](https://github.com/UnchartedBull/OctoDash/issues/928)

1st u need to go to /boot and edit config.txt
`sudo nano /boot/config.txt`

at the very bottom add:
`display_lcd_rotate=2`

Note: The angle of rotation is counted clockwise. display_lcd_rotate=0 (landscape) display_lcd_rotate=1 （90 degress） display_lcd_rotate=2 （180 degrees） display_lcd_rotate=3 （270 degrees）

Note2: I'm using the 180 degrees option in this example so change to your liking.
save and
`sudo reboot now`

after it reboots you will see touchscreen not responsive because we just rotated the lcd display but not the touch screen. to rotate the touchscreen simply do the following steps:
go to:
`cd /usr/share/X11/xorg.conf.d`

find the libinput file by doing
`ls`

u can now edit it will be something like:
`sudo nano 40-libinput.conf`

in the Section "InputClass" find the Identifier that says: "libinput touchscreencatchall" and below the line MatchIsTouchScreen "on" add the following line:
`Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"`

Note1:

```
90° = Option "TransformationMatrix" "0 1 0 -1 0 1 0 0 1"
180° = Option "TransformationMatrix" "-1 0 1 0 -1 1 0 0 1"
270° = Option "TransformationMatrix" "0 -1 1 1 0 0 0 0 1"

```

Note2: Again i'm using the 180 degrees in this example change to your liking from Note1 section
Note3: The XY position of different touch screen's start point may be various, so the transformation matrix values of 90° and 270° may be the opposite. For models other than M505T, please try to adjust it yourself! This has been tested on the raspberry PI official 7 inch touchscreen.

save reboot everything should work properly
`sudo reboot now`
