This page describes how to install the security system to a Raspberry PI.
Use and SD Card with at least 8GB capacity and reliable quality to avoid data loss.

### SD Card preparation

1. Select the operating system image
    * Raspberry PI Zero W 2 [Raspberry Pi OS Lite (32-bit)](https://www.raspberrypi.org/software/operating-systems/)
2. Setup your configuration
    * user name: argus / password: Argus.1234
    * enable SSH with password authentication
    * configure WLAN
    * locale
    * hostname: arpi.local
3. Insert the card, start the Raspberry PI and connect to the host
    ```
    ssh argus@arpi.local
    ```
4. Configure some general settings with "raspi-config" and reboot
    * Enable serial port without login shell

### SSH configuration

1. For your ssh configuration in ~/.ssh/config
```
Host arpi.local
    HostName arpi.local
    # or with IP address
    # HostName 192.168.50.159
    User argus
    Port 22
    IdentityFile ~/.ssh/id_rsa
    IdentitiesOnly yes
```

2. Copy your SSH key to the host using the password from previous step
```bash
ssh-copy-id argus@arpi.local
```


### Install ArPI

Before installing the ArPI to a running Raspberry PI system [get the code](index.md#getting-the-code)!

1. Start the Raspberry PI Zero with the prepared SD card
2. Check the installation configuration file (update the values for your installation environment): install/install.yaml.
```yaml
# yaml-language-server: $schema=install_schema.json
# access of the installed arpi system
# yaml-language-server: $schema=install_schema.json
# access of the arpi host
arpi_access:
  hostname: arpi.local
  password: ## SSH password ##
  deploy_ssh_key: false
  disable_ssh_password_authentication: false

# database access
database:
  name: argus
  username: argus
  content: prod

deployment:
  board_version: 3 # or 2
  use_simulator: false
  server_environment: prod
  webapplication_path: webapplication/dist-production/browser
  extra_packages:
    - device
    - simulator
```

3. Install the ArPI components with the management project from your development host (not the Raspberry PI).
    ```
    # activate the python virtual environment
    pipenv shell
    # install the backend
    ./install.py server --prepare --bootstrap --deploy
    ```
4. Before this step you will need to [build the web application for production mode](web_application.md#production_1)!
    ```
    # install the frontend
    ./install.py webapplication
    ```
5. You can access the web application https://arpi.local  
    * Default registration code for admin: `ABCD1234`
    * Default access code: `1234`

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py => def env_prod()
    
    See on [Github](https://github.com/ArPIHomeSecurity/arpi_server/blob/master/src/data.py#L40)
