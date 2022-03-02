OctoDash can be even further customized with your own, custom CSS stylesheet. Just add whatever CSS rules you like to `~/.config/octodash/custom-styles.css` and restart your Pi or OctoDash. These CSS rules will be applied after all standard CSS, you still need to use some `!important`s to overwrite some rules probably.

## Themes

// TODO

### [Nox](https://github.com/UnchartedBull/OctoDash/tree/master/themes/NOX)

![nox-screenshot](https://github.com/UnchartedBull/OctoDash/raw/master/themes/NOX/screenshots/screenshot_printing.png)

## Developing a new theme

If you want to develop and quickly test a new theme it is recommended to fire up a development instance of OctoDash (more info [here](https://github.com/UnchartedBull/OctoDash/blob/master/CONTRIBUTING.md)). This allows you to use the Chrome Debugger tools to identify class names and test your changes in realtime.

Please remember that CSS can be tricky sometimes, so your first solution might not always work. If you need additional elements / want to accomplish something that isn't possible with CSS alone - please open a new issue and state your problem. There is no guarantee that your requested element will be added though.

## Submitting a new theme

If you think, that your theme deserves to be shared with the whole community feel free to open a Pull Request. The Pull Request should include the following:

- one css file named `custom-styles.css`
- one `README.md` file with the name of your theme, your name/handle (if you like) and some screenshots (linked from screenshots folder)
- at least one screenshot (png/jpeg) in the `screenshots` sub-folder

All of these files should be inside a folder with the name of your theme in the `themes` subfolder. The NOX theme is once again a good starting point.
