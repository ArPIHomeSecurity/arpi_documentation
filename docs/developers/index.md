# Developers help

## Running in demo mode

## Running on PC

## Running on Raspberry

## Installing the code from source

## Installing from image

## Translations

## Hardware clock

The software is configured to use a DS1307 hardware clock. The configuration is prepared during the installation of the board (arpi_management/scripts/install_environment.sh).

The hardware clock is updated every hour from system clock and updates the system clock on reboot (arpi_management/arpi_server/etc/cron/hwclock).