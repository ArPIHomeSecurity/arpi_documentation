# Developers help

## Getting the code

git clone --recursive ...

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

1. Download Rasbian
2. Use Etcher to write to a card
3. Configure wifi to access the host
4. Connect to the host
5. Resize the card
6. Update and upgrade Raspbian
7. Configure the installation
8. Install the environment
9. Install the components
10. Get registration code


### Installing from image

1. Download the image
2. Write to a card
3. Configure wifi
4. Get registration code

## Translations

## Hardware clock

The software is configured to use a DS1307 hardware clock. The configuration is prepared during the installation of the board (arpi_management/scripts/install_environment.sh).

The hardware clock is updated every hour from system clock and updates the system clock on reboot (arpi_management/arpi_server/etc/cron/hwclock).