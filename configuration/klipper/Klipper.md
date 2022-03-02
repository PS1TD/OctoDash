OctoDash is not natively compatible with Klipper. If you want to use OctoDash with Klipper you have to install OctoPrint as well. Native support is coming soon.

The same necessary steps from the [OctoPrint](./Octoprint) Guide apply here. Other than that change `zBabystepGCode` in your `config.json` to `SET_GCODE_OFFSET MOVE=1 Z_ADJUST=` if you want to use Babystepping.
