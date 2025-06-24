The ArPI simulator is a powerful testing tool that allows you to develop and test the home security system
without physical hardware. It provides a graphical terminal interface for controlling all system inputs
and monitoring outputs in real-time.

## Features

- **Channel Simulation**: Control 15 sensor channels (doors, windows, motion detectors, etc.)
- **Power Input Simulation**: Simulate power failures and restoration
- **Keypad Simulation**: Send key presses (0-9, *, #) and RFID card data
- **Output Monitoring**: Real-time display of system outputs (relays, status indicators)
- **File-based Communication**: JSON files for integration with the ArPI monitoring service

The simulator uses a modern TUI (Terminal User Interface) built with the Textual library, providing an intuitive interface for testing scenarios.

## Starting the Simulator

### Prerequisites

The simulator requires the Textual library. Installation differs between environments:

- **Local Development**: get the source code from the repository and run it
- **Deployed System**: get the ArPI image and run it

### Running the Simulator

The simulator can run in two different environments with different setups and purposes:

#### Local Development

For local development, you can run the simulator directly from the source code.
```bash
# navigate to the server directory and run the simulator
pipenv run start-simulator
```

For more  details how to use the development environment, see the [Backend](../backend) and
[Webapplication](../web_application) documentation.

#### Deployed System

```bash
# Connect to your ArPI device (Raspberry Pi)
ssh argus@arpi.local

# Navigate to the server directory
cd /home/argus/server

# Run the simulator directly
./src/simulator.py
```

### User Interface

The simulator provides three main sections:

1. **Channels Panel (Left)**: 15 sensor channels plus power input
    - Each channel button represents a sensor input (CH01-CH15)
    - Click any channel button to toggle between LOW (0) and HIGH (1) states
    - RED buttons indicate HIGH/triggered state
    - GREEN buttons indicate LOW/normal state

2. **Keypad Panel (Right)**: Numeric keypad and RFID simulation
    - Numbers 0-9, * and # keys for keypad input
    - Three predefined RFID cards for access testing

3. **Outputs Panel (Bottom)**: System output monitoring
    - Displays system outputs (O0-O4, R0-R1, GO)
    - Real-time display of relay states and status indicators
    - Updates automatically when the monitoring service changes outputs

## Communication Protocol

The simulator communicates with the ArPI monitoring service through three JSON files. These files are created automatically when you first run the simulator.

### Input Files

- simulator_input.json
Controls the state of sensor channels and power input. This file is written by the simulator and read by the monitoring service.

```json
{
    "CH01": 0,    // Sensor channel 1 (0=normal, 1=triggered)
    "CH02": 0,    // Sensor channel 2
    "CH03": 0,    // Sensor channel 3
    // ... channels 4-15
    "CH15": 0,    // Sensor channel 15
    "POWER": 0    // Power input (0=normal, 1=power failure)
}
```

- simulator_keypad.json
Handles keypad input and RFID card data. The service processes pending keypad events from this file.

```json
{
    "pending_bits": 0,    // Number of bits waiting to be processed
    "data": []            // Array of keypad inputs (keys or card numbers)
}
```


### Output Files

- simulator_output.json
The monitoring service writes to this file to control outputs. The simulator reads it to update the output display.

```json
{
    "GO": 0,      // System armed indicator
    "R1": 0,      // Relay 1 (siren, etc.)
    "R0": 1,      // Relay 0 (status LED, etc.)
    "O4": 0,      // Output 4
    "O3": 0,      // Output 3  
    "O2": 0,      // Output 2
    "O1": 0,      // Output 1
    "O0": 0       // Output 0
}
```

!!! note "File Locking"
    The simulator uses file locking to prevent race conditions when multiple processes access the JSON files simultaneously.

## Configuration

The simulator configuration varies significantly between development and production environments.

### Local Development

For development, the simulator is typically enabled by default. Configuration is done through environment files:

```bash
# edit development environment file
nano /path/to/arpi_management/server/.env

# enable simulator mode for development
USE_SIMULATOR=true
```

### Deployed System

Production systems require more careful configuration management:

```bash
# SSH into your ArPI device
ssh argus@arpi.local

# Edit the production environment file
sudo nano /home/argus/server/.env

# Enable simulator mode
USE_SIMULATOR=true

# Restart the system service
sudo systemctl restart argus_monitor
```


## RFID Card Reference

The simulator includes three predefined RFID cards for testing:

| Button | Card Number | Purpose |
|--------|-------------|---------|
| Card 1 | 550021576706 | Valid user card |
| Card 2 | 550021576707 | Alternative user card |
| Card 3 | 550021576708 | Test/guest card |
