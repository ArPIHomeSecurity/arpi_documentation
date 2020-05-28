# Developers help

## Getting the code

Open a terminal, navigate into your working directory and run the following command:
```bash
git clone --recurse-submodules https://github.com/ArPIHomeSecurity/arpi_management.git
```
This command will download the source code of management project of
the ArPI Home security system with the server and the webapplication components.

```
+ arpi_management: managing the software components
|--arpi_server: backend
|--arpi_webapplication: frontend
```

## Running in different modes

Goal of the different modes

1. Demo production
2. Demo development
3. Development
4. Production

### Running in demo production mode

Start the web application in demo mode

### Running in demo development mode

Start the web application in demo mode

### Running on PC in development mode

Start the web application in demo mode

### Running in demo development mode

Start the system in development mode

## Running on Raspberry

Start the system in production mode

## Installation

The different installation modes
1. From source
2. From image

### Installing the code from source

#### Prepare the SD card for installing ArPI

1. Download [Raspberry PI OS](https://www.raspberrypi.org/downloads/raspbian/) without desktop
2. Use [Etcher](https://www.balena.io/etcher/) to write to a card
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


#### Install ArPI to the prepared system

Before installing the ArPI to a running Raspberry PI system [get the code](#getting-the-code)!

1. Start the Raspberry PI Zero with the prepared SD card
2. Check the installation configuration file: install.yaml
3. Install the ArPI components with the management project from your development host (not the raspi)

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

### Installing from image

1. Download the image
2. Write to a card
3. Configure wifi
4. Get registration code

## Translations

## Hardware clock

The software is configured to use a DS1307 hardware clock. The configuration is prepared during the installation of the board (arpi_management/scripts/install_environment.sh).

The hardware clock is updated every hour from system clock and updates the system clock on reboot (arpi_management/arpi_server/etc/cron/hwclock).