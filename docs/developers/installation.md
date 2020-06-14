# Installation

## Installing from image

1. Download the image from [Github](https://github.com/ArPIHomeSecurity/arpi_management/releases/)
2. Use [Etcher](https://www.balena.io/etcher/) to write to an SD card
3. Configure wifi
    1. Generate WIFI passphrase

            wpa_passphrase <ssid> [passphrase]

    2. Append the output to the file "/rootfs/etc/wpa_supplicant/wpa_supplicant.conf"

4. Start the Raspberry PI with the SD card and access it on [https://arpi.local](https://arpi.local)
5. Use the default registration code:ABCD1234 and password:1234

## Installing from source

### Prepare the SD card

1. Download [Raspberry PI OS](https://www.raspberrypi.org/downloads/raspbian/) without desktop
2. Use [Etcher](https://www.balena.io/etcher/) to write to an SD card
3. Configure wifi to access the host ([docs](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md))
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
    5. Expand filesystem
7. Update and upgrade Raspbian

        sudo apt update
        sudo apt upgrade


### Install ArPI

Before installing the ArPI to a running Raspberry PI system [get the code](#getting-the-code)!

1. Start the Raspberry PI Zero with the prepared SD card
2. Check the installation configuration file: install.yaml
3. Install the ArPI components with the management project from your development host (not the raspi). Before this step you will need to [build the web application for production mode](#building-for-production)!

        # activate the python virtual environment
        pipenv shell
        # install the prerequisites
        ./install.py environment
        ./install.py server
        # build the production webapplication before install
        ./install.py webaplication
        ./install.py database

4. Enable the services

        # after login to your raspi
        sudo systemctl enable argus_server argus_monitor nginx
        sudo systemctl start argus_server argus_monitor
        # wait some seconds
        sudo systemctl start nginx

5. You can access the web application

