I'm sad to see you go! If something bugs you, that you think can be fixed, don't hesitate to open an issue.

You can either remove OctoDash with a [a script](#remove-with-script) or [manually](#manual-removal)

## Remove with a Script

The source for the script can be found [here](https://github.com/UnchartedBull/OctoDash/blob/main/scripts/remove.sh)

```bash
wget -qO- https://github.com/UnchartedBull/OctoDash/raw/main/scripts/remove.sh | bash
```

## Manual Removal

- Uninstall the OctoDash package

  `sudo dpkg --remove octodash`

- Remove the config files

  `rm -rf .config/octodash`

- Remove the following contents from `~/.xinitrc` if present

  ```bash
      #!/bin/sh

      xset s off
      xset s noblank
      xset -dpms

      ratpoison&
      octodash
  ```

- Remove the following contents from `~/.bashrc` if present

  ```bash
  if [ -z "$SSH_CLIENT" ] || [ -z "$SSH_TTY" ]; then
      xinit -- -nocursor
  fi
  ```
