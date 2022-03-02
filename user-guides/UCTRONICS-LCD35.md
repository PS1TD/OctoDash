# UCTRONICS LCD35 SPI Install

by [@theshortest](https://github.com/theshortest)

### Update and upgrade

```bash
sudo apt-get update
sudo apt-get upgrade
```

### Driver Install

```bash
git clone https://github.com/UCTRONICS/UCTRONICS_HSLCD35.git
cd UCTRONICS_HSLCD35/Octoprint
sudo chmod +x UCTRONICS_HSLCD35_SHOW
sudo ./UCTRONICS_HSLCD35_SHOW
```

### Octodash Install

```bash
bash <(wget -qO- https://github.com/UnchartedBull/OctoDash/raw/master/scripts/install.sh)
```

### fbturbo install

https://github.com/UnchartedBull/OctoDash/issues/1013

```bash
sudo apt-get install libgtk-3-0 xserver-xorg xinit x11-xserver-utils
sudo apt-get install git build-essential xorg-dev xutils-dev x11proto-dri2-dev
sudo apt-get install libltdl-dev libtool automake libdrm-dev
git clone https://github.com/ssvb/xf86-video-fbturbo.git

cd xf86-video-fbturbo
autoreconf -vi
./configure --prefix=/usr
make
sudo make install
sudo cp xorg.conf /etc/X11/xorg.conf
```

### SPI not working fix

```bash
sudo nano /etc/X11/xorg.conf.d/99-fbdev.conf
Change: Option "fbdev" "/dev/fb1" to Option "fbdev" "/dev/fb0"
Ctrl-O, enter, Ctrl-X
```

### Not necessary unless installing a desktop to do recalibration

https://www.raspberrypi.org/forums/viewtopic.php?t=203483

```bash
sudo apt-get install xinput-calibrator
```

### Config edit doc

This calibration and matrix rotation is speciific to the display it was created on but my very well work for others.
TransformationMatrix sequence is a counterclockwise rotation other matrix rotations found here. (https://github.com/swkim01/waveshare-dtoverlays)

```bash
sudo nano /etc/X11/xorg.conf.d/99-calibration.conf

Section "InputClass"
        Identifier      "calibration"
        MatchProduct    "ADS7846 Touchscreen"
        Option  "TransformationMatrix" "0 -1 1 1 0 0 0 0 1"
        Option  "MinX"  "23529"
        Option  "MaxX"  "23165"
        Option  "MinY"  "47871"
        Option  "MaxY"  "49100"
        Option  "SwapXY"        "1" # unless it was already set to 1
        Option  "InvertX"       "0"  # unless it was already set
        Option  "InvertY"       "0"  # unless it was already set
EndSection
```
