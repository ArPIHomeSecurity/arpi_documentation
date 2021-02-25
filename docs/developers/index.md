Help for developers/contributors.

!!! note
    The development on the Raspberry PI can be time consuming.
    Use your pc for development and deploy the code changes to a Raspberry PI.

## Getting the code for local development

Open a terminal, navigate into your working directory and run the following command:
```bash
git clone --recurse-submodules https://github.com/ArPIHomeSecurity/arpi_management.git
```
This command will download the source code of management project of
the ArPI Home security system with the server and the web application components.

```
+ arpi_management: managing the software components
|--arpi_server: backend
|--arpi_webapplication: frontend
```

## Prerequisites for development

* python 3
* python pipenv (for management and server)
* nodejs (for the web application)
* docker (for management and server)
* For PyGObject on Ubuntu/Debian (for server)
```bash
    sudo apt install \
        gcc \
        libgirepository1.0-dev \
        libcairo2-dev \
        pkg-config \
        python3-dev \
        gir1.2-gtk-3.0
```

Preparing environments:

* Server: python
    ```bash
    pipenv install --dev
    ```
* Web application: angular
    ```bash
    npm install --dev
    ```

## Features

### Hardware clock

The software is configured to use a DS1307 hardware clock. The configuration is prepared
during the installation of the board (arpi_management/scripts/install_environment.sh).

The hardware clock is updated every hour from system clock and updates
the system clock on reboot (arpi_management/arpi_server/etc/cron/hwclock).

### GSM module

The software is configured to work with a GSM module (tested with SIM900A) on serial port /dev/ttyAMA0 9600 Baud.
The console on serial port is disabled.

### NoIP

You can use a NoIP provider for accessing the security system remotely
on the same domain name.

### Certbot

You can switch the connection of the web application to a signed HTTPS connection
with the help of Certbot.
