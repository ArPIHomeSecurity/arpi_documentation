This page describes how to install the security system to a Raspberry PI.

# Installing from image

1. Download the image from [GitHub](https://github.com/ArPIHomeSecurity/arpi_management/releases/)
2. Use [Etcher](https://www.balena.io/etcher/) to write to an SD card
3. Configure WiFi
    1. Generate WIFI passphrase
        ```
        wpa_passphrase <ssid> [passphrase]
        ```
    2. Append the output to the file "/rootfs/etc/wpa_supplicant/wpa_supplicant.conf"

4. Start the Raspberry PI with the SD card
5. You can access the web application https://arpi.local
    * Default registration code for admin: ABCD1234
    * Default access code: 1234
    * Default password for argus user on SSH: Argus.1234

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py - method env_prod


## Installing from source

You have two options to prepare the SD card with

* Balena Etcher
* Rapberry PI Imager


### Prepare the SD Card
#### Prepare the SD card with **Etcher**

1. Download the operating system image
    * Raspberry PI Zero W [Raspberry Pi OS Lite (32-bit)](https://www.raspberrypi.org/software/operating-systems/)
    * Raspberry PI Zero W 2 [Raspberry Pi OS Lite (64-bit)](https://www.raspberrypi.org/software/operating-systems/)
2. Use [Etcher](https://www.balena.io/etcher/) to write the image to an SD card
3. Configure WiFi to access the host ([docs](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md))
    1. Generate WIFI passphrase
        ```
        wpa_passphrase <ssid> [passphrase]
        ```
    2. Append the output to the file "/rootfs/etc/wpa_supplicant/wpa_supplicant.conf"

4. Enable ssh connections: create a file with name "ssh" in the /boot
5. Insert the card, start the Raspberry PI and connect to the host

        ssh pi@raspberrypi.local

6. Configure some general settings with "raspi-config" and reboot
    1. Locale
    2. Keyboard
    3. Timezone
    4. Enable serial port
    5. Enable i2c
    6. Enable ssh
    7. Expand file system
7. Update and upgrade Raspbian
    ```
    sudo apt update
    sudo apt upgrade
    ```

#### Prepare the SD card with **Raspberry PI Imager**

1. Select the operating system image
    * Raspberry PI Zero W [Raspberry Pi OS (Legacy) Lite (32-bit)](https://www.raspberrypi.org/software/operating-systems/)
    * Raspberry PI Zero W 2 [Raspberry Pi OS (Legacy) Lite (32-bit)](https://www.raspberrypi.org/software/operating-systems/)
2. Setup your configuration
    * user name: pi
    * enable SSH with password authentication
    * configure WLAN
    * locale
3. Insert the card, start the Raspberry PI and connect to the host
    ```
    ssh pi@raspberrypi.local
    ```
4. Configure some general settings with "raspi-config" and reboot
    * Enable serial port
    * Enable i2c
    * Enable ssh
    * Expand file system
5. Update and upgrade Raspbian
    ```
    sudo apt update
    sudo apt upgrade
    ```


### Install ArPI

Before installing the ArPI to a running Raspberry PI system [get the code](index.md#getting-the-code)!

1. Start the Raspberry PI Zero with the prepared SD card
2. Check the installation configuration file (update the values for your installation environment): install.yaml
3. Generate your ssh keys
    ```
    ssh-keygen -t rsa -b 4096 -f ./arpi
    ```
4. Install the ArPI components with the management project from your development host (not the Raspberry PI).
    ```
    # activate the python virtual environment
    pipenv shell
    # install the prerequisites
    ./install.py environment
    ./install.py -u server
    ./install.py monitor
    ./install.py database
    ```
5. Before this step you will need to [build the web application for production mode](web_application.md#production_1)!
    ```
    ./install.py webapplication
    ```
6. Enable the services
    ```
    # after login with ssh to your raspi
    sudo systemctl enable nginx argus_server argus_monitor
    sudo systemctl start nginx argus_server argus_monitor
    ```
7. You can access the web application https://arpi.local  
Default registration code for admin: ABCD1234  
Default access code: 1234

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py => def env_prod()
