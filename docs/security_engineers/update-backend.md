
# Update Backend

Use this page to update the ARPI backend service on a deployed device.
The update script downloads and installs the latest backend release that matches the selected options.

## Before You Start

- Ensure the device has internet access.
- Run commands with a user that has permission to install/update system services.
- If possible, make a backup or snapshot before updating production systems.

## Standard Backend Update

Run the installer script directly from the ARPI application host:

```bash
curl -sSL https://app.arpi-security.info/install.py | /usr/bin/python3
```

This command fetches the current installer and executes the default update workflow.

## Installer Options

To view all available parameters:

```bash
curl -sSL https://app.arpi-security.info/install.py | /usr/bin/python3 - --help
usage: - [-h] [--prerelease] [--board-version BOARD_VERSION] [--use-simulator]

options:
  -h, --help            show this help message and exit
  --prerelease          Use latest prerelease
  --board-version BOARD_VERSION
                        Board version (2 or 3)
  --use-simulator       Use simulator
```

!!! warning
  Changing the board version updates Raspberry Pi configuration.
  Restart the device after the update so all configuration changes are applied.

## Common Scenarios

- Install latest prerelease:

  ```bash
  curl -sSL https://app.arpi-security.info/install.py | /usr/bin/python3 - --prerelease
  ```

- Force board version 2:

  ```bash
  curl -sSL https://app.arpi-security.info/install.py | /usr/bin/python3 - --board-version 2
  ```

- Run with simulator enabled:

  ```bash
  curl -sSL https://app.arpi-security.info/install.py | /usr/bin/python3 - --use-simulator
  ```

## After Update

- Confirm the backend service is running.
- Verify you can sign in to the web application.
- Check system logs if any startup or connectivity issue appears.
