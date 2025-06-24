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

## Get the ArPI Image

1. **Download the latest ArPI image** from the official releases:
    - Visit: [ArPI Releases](https://github.com/ArPIHomeSecurity/arpi_management/releases)
    - Download the `.img.xz` file (latest version)

2. **Flash the image to SD card**:
    - Use [Raspberry Pi Imager](https://rpi.org/imager) or [Balena Etcher](https://balena.io/etcher)
    - Select the downloaded ArPI image
    - Flash to a 16GB+ SD card

## Configure WiFi

Since ArPI runs headless (no monitor), you need to configure WiFi before first boot:

1. After flashing, **don't eject** the SD card yet
2. Open the SD card on your computer (it will appear as "boot")
3. **Create WiFi configuration** by adding a `wpa_supplicant.conf` file:
   ```bash
   # Generate password hash for security
   wpa_passphrase "YourWiFiName" "YourWiFiPassword" > wpa_supplicant.conf
   
   # Edit the file to add country code
   nano wpa_supplicant.conf
   ```
   Add this line at the top of the file:
   ```
   country=US
   ```
   The final file should look like:
   ```
   country=US
   ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
   update_config=1
   
   network={
       ssid="YourWiFiName"
       psk=generated_hash_here
   }
   ```

## Connect with SSH

1. Insert the SD card into your Raspberry Pi and power on
2. **Wait 2-3 minutes** for the system to boot and connect to WiFi
3. Connect via SSH:
   ```bash
   ssh argus@arpi.local
   ```

5. **Enter the password** you set during imaging (default: `Argus.1234`)

!!! tip "Connection Issues?"
    - Ensure your computer and Raspberry Pi are on the same WiFi network
    - Try `ping arpi.local` to test basic connectivity

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

## Connect to Web Interface

1. Open your web browser and navigate to: `http://arpi.local`

2. Register your device (first time only):
   - Use default registration code: `ABCD1234`

3. Log in to the system:
   - Default access code: `1234`
   

## Configure system

### Add a sensor

1. Navigate to Sensors in the web interface:
    - Click on "Sensors" in the main menu
    - Click "Add Sensor"

2. Configure the sensor:
    - **Channel**: Select `CH01` (this must match the simulator)
    - **Type**: Choose `Open/Closed` or `Motion Detector`
    - **Description**: Enter something like "Front Door Test"
    - **Enabled**: Make sure it's checked ✅
    - **Area**: Assign to an area (create one if needed)
    - **Zone**: Assign to a zone (create one if needed)
    - **Zone Settings**: set delays to 0 seconds for testing

3. Save the sensor configuration

### Start the simulator

1. In your SSH terminal, start the simulator:
```bash
cd /home/argus/server
./src/simulator.py
```

2. You'll see a text-based interface with:
   - **Left panel**: 15 channel buttons (CH01-CH15) + POWER
   - **Right panel**: Keypad and 3 RFID cards
   - **Bottom panel**: System outputs (relays, indicators, siren)

### Test functionality

1. Arm your system via the web interface:
    - Go to the main dashboard
    - Click "Arm" for your area

2. Trigger the sensor in the simulator:
    - Click the CH01 button in the simulator
    - The button should turn RED (indicating triggered state)

3. Verify the alarm:
    - Check the web interface for alarm notification
    - Look for changes in the simulator's output panel
    - You should see system responses (R1 for siren, etc.)

4. Test disarming:
    - Use the keypad in the simulator to enter your access code
    - Or click one of the RFID card buttons
    - Verify the system disarms
