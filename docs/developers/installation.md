This page describes how to install the security system to a Raspberry PI.

## Installing from image

1. Download the image from [GitHub](https://github.com/ArPIHomeSecurity/arpi_management/releases/)
2. Use [Etcher](https://www.balena.io/etcher/) to write to an SD card
3. Configure WiFi
    1. Generate WIFI passphrase

            wpa_passphrase <ssid> [passphrase]

    2. Append the output to the file "/rootfs/etc/wpa_supplicant/wpa_supplicant.conf"

4. Start the Raspberry PI with the SD card
5. You can access the web application https://arpi.local
   * Default registration code for admin: ABCD1234
   * Default access code: 1234

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py - method env_prod


## Installing from source

### Prepare the SD card

1. Download [Raspberry Pi OS Lite](https://www.raspberrypi.org/software/operating-systems/)
2. Use [Etcher](https://www.balena.io/etcher/) to write the image to an SD card
3. Configure WiFi to access the host ([docs](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md))
    1. Generate WIFI passphrase

            wpa_passphrase <ssid> [passphrase]

    2. Append the output to the file "/rootfs/etc/wpa_supplicant/wpa_supplicant.conf"

4. Enable ssh connections: create a file with name "ssh" in the /boot
5. Insert the card, start the Raspberry PI and connect to the host

        ssh pi@raspberrypi.local

6. Configure some general settings with "raspi-config" and reboot
    1. Locale
    2. Keyboard
    3. Timezone
    4. Enable serial
    4. Enable ssh
    5. Expand file system
7. Update and upgrade Raspbian

        sudo apt update
        sudo apt upgrade


### Install ArPI

Before installing the ArPI to a running Raspberry PI system [get the code](index.md#getting-the-code-for-local-development)!

1. Start the Raspberry PI Zero with the prepared SD card
2. Check the installation configuration file: install.yaml
3. Generate your ssh keys
   
        ssh-keygen -t rsa -b 4096 -f ./arpi

4. Install the ArPI components with the management project from your development host (not the Raspberry PI). Before this step you will need to [build the web application for production mode](#building-for-production)!

        # activate the python virtual environment
        pipenv shell
        # install the prerequisites
        ./install.py environment
        ./install.py server
        # build the production webapplication before install
        ./install.py webaplication
        ./install.py database

5. Enable the services

        # after login to your raspi
        sudo systemctl enable nginx argus_server argus_monitor
        sudo systemctl start nginx argus_server argus_monitor

6. You can access the web application https://arpi.local
   * Default registration code for admin: ABCD1234
   * Default access code: 1234

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py - method env_prod



