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

### Install ArPI

Before installing the ArPI to a running Raspberry PI system [get the code](index.md#getting-the-code)!

1. Start the Raspberry PI Zero with the prepared SD card
2. Check the installation configuration file (update the values for your installation environment): install.yaml
```yaml
# yaml-language-server: $schema=install_schema.json
# access of the installed arpi system
arpi_access:
  username: argus
  key_name: keys/arpi_rsa
  password: <argus password>
  hostname: arpi.local
  deploy_ssh_key: true
  disable_ssh_password_authentication: true

# database access
database:
  name: argus
  username: argus
  content: prod

# deployment settings
deployment:
  server_environment: prod
  webapplication_path: webapplication/dist-production/browser
  packages:
    postgresql_version: 15
    nginx_version: 1.26.2
  dhparam_size: 4096
  deploy_simulator: true
  salt: <random text>
  secret: <random text>

```
3. Install the ArPI components with the management project from your development host (not the Raspberry PI).
    ```
    # activate the python virtual environment
    pipenv shell
    # install the prerequisites (postgresql, nginx...)
    ./install.py environment
    # install the server component
    ./install.py -ur server
    # install the monitor component
    ./install.py -r monitor
    # install the database content
    ./install.py -u database
    ```
4. Before this step you will need to [build the web application for production mode](web_application.md#production_1)!
    ```
    ./install.py webapplication
    ```
5. You can access the web application https://arpi.local  
    * Default registration code for admin: `ABCD1234`
    * Default access code: `1234`

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py => def env_prod()
    
    See on [Github](https://github.com/ArPIHomeSecurity/arpi_server/blob/master/src/data.py#L40)
