# Developers

Help for developers/contributors.

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

## Prequisities

* python 3
* python virtualenv / pipenv
* nodejs
* docker

## Features

### Hardware clock

The software is configured to use a DS1307 hardware clock. The configuration is prepared during the installation of the board (arpi_management/scripts/install_environment.sh).

The hardware clock is updated every hour from system clock and updates the system clock on reboot (arpi_management/arpi_server/etc/cron/hwclock).

### GSM module

The software is configured to work with a GSM module (tested with SIM900A) on serial port /dev/ttyAMA0 9600 Baud.
The console on serial port is disabled.

### NoIP and Certbot
