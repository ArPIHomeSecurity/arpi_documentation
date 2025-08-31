after flashing the image:

# Testing Your ArPI System with the Simulator

The ArPI simulator allows you to test your home security system without physical sensors. This is perfect for:

- **Initial setup**: Test your system configuration before installing real sensors
- **Troubleshooting**: Verify if issues are hardware or software related
- **Learning**: Understand how the system works before committing to hardware
- **Demonstrations**: Show the system functionality

!!! info "What You'll Need"
    - A computer with WiFi capability
    - Basic knowledge of using SSH (secure shell)
    - 30-45 minutes of setup time

## Prerequisites

Before using the simulator, you need a working ArPI system image. For detailed instructions, see:
[Software installation guide](../security_engineers/installation-sw.md)

Once your device is set up and you can connect via SSH, see: [Connect with SSH](../security_engineers/ssh.md)


## Enable Simulator Mode

Once connected via SSH, enable the simulator mode:

1. Navigate to the server directory:
    ```bash
    cd /home/argus/server
    ```
2. Edit the configuration file:
    ```bash
    sudo nano .env
    ```
3. Add or modify the simulator setting:
    ```bash
    # Find and change or add this line:
    USE_SIMULATOR=true
    ```
4. Save and exit (Ctrl+X, then Y, then Enter)
5. Restart the ArPI service:
    ```bash
    sudo systemctl restart argus_monitor
    ```
6. Verify the service is running:
    ```bash
    sudo systemctl status argus_monitor
    ```
    You should see "active (running)" in green.


## Connect to Web Interface and Configure System

1. Open your web browser and navigate to: `http://arpi.local`
2. Register your device and log in. For details, see:
    - [Registering Your Device](register.md)
    - [Logging In](login.md)
3. To add and configure sensors, see:
    - [Sensors](sensors.md)
    - [Areas](areas.md)
    - [Zones](zones.md)


## Start the Simulator

1. In your SSH terminal, start the simulator:
    ```bash
    cd /home/argus/server
    ./src/simulator.py
    ```
2. You'll see a text-based interface with:
    - **Left panel**: 15 channel buttons (CH01-CH15) + POWER
    - **Right panel**: Keypad and 3 RFID cards
    - **Bottom panel**: System outputs (relays, indicators, siren)


## Test Functionality

1. Arm your system via the web interface ([see Areas](areas.md))
2. Trigger the sensor in the simulator (e.g., click the CH01 button)
3. Verify the alarm in the web interface and simulator output panel
4. Test disarming using the keypad or RFID cards in the simulator
