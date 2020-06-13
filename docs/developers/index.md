# Getting the code

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

# The web application

The user interface of the security system is implemented in angular. This web application
can be used in different modes.

Goal of the different modes

1. Demo production: running on Github pages with mock REST API
2. Demo development: running locally with mock REST API
3. Development: running locally with backend service using mock adapters
4. Production: running on Raspberry PI

## Running in demo production mode

This mode is for running the web application in demo mode on Github pages with
a mock REST API.

```bash
# setting the environment
export DIST=dist-demo
# building the application
ng build --configuration=demo --localize
# move default language to the root of the output folder
npm run postbuild
# start serving the web application on http://localhost:4200
npm run serve
```

## Running in demo development mode

This mode is for running the web application in demo development mode locally with
a mock REST API.

```bash
# setting the environment
export DIST=dist-demo-dev
# building the application
ng build --configuration=demo-dev --localize
# move default language to the root of the output folder
npm run postbuild
# start serving the web application on http://localhost:4200
npm run serve
```

## Building for development mode

This mode is for running the web application in development mode with
the backend services locally. The backend services are using the mock adapters
instead of the real adapters.

1. Build the web application

```bash
# setting the environment
export DIST=dist-development
# building the application
ng build --localize
# move default language to the root of the output folder
npm run postbuild
```

2. Start the backend services

```bash
# go the server folder
cd server
# start the REST API (it also serves the web application)
./scripts/start_server.sh dev
# start the monitoring service
./scripts/start_monitor.sh dev
```


## Building for production

```bash
# setting the environment
export DIST=dist-production
# building the application
ng build --configuration=production --localize
# move default language to the root of the output folder
npm run postbuild
```

# The backend services

The backend system has two major components:

1. The server provides the REST API to communicate with the web application
2. The monitor implements the main functionality (IO handling, RTC, GSM...)

## The server

## The monitor

# Installation

The different installation modes
1. From source
2. From image

## Installing the code from source

### Prepare the SD card for installing ArPI

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


### Install ArPI to the prepared system

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

### Installing from image

1. Download the image
2. Write to a card
3. Configure wifi
4. Get registration code

# Translations

# Hardware clock

The software is configured to use a DS1307 hardware clock. The configuration is prepared during the installation of the board (arpi_management/scripts/install_environment.sh).

The hardware clock is updated every hour from system clock and updates the system clock on reboot (arpi_management/arpi_server/etc/cron/hwclock).

# GSM module

The software is configured to work with a GSM module (tested with SIM900A) on serial port /dev/ttyAMA0 9600 Baud.
The console on serial port is disabled.