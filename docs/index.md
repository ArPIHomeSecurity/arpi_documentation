# ArPI - Modern Home Security System

ArPI is a Raspberry Pi-based home security system designed for modern smart homes with professional-grade security features.

## Project Overview

ArPI transforms traditional security systems by replacing outdated control panels with a modern,
connected solution while preserving existing wiring and sensors.

### Key Features

✅ **Secure Access** - Reliable and secure access to your home security system  
✅ **User Management** - Multiple users with different access levels and RFID card support  
✅ **Remote Access** - Access your security system from anywhere via web or mobile  
✅ **Smart Notifications** - SMS and email alerts for system events and power outages  
✅ **Multi-location Support** - Manage multiple locations or areas with flexible configuration  
✅ **Programmable Outputs** - Control external devices with programmable relay outputs  
✅ **GSM Communication** - SMS notifications and voice calls without internet connection  
✅ **Home Automation** - Integration with Home Assistant, Domoticz, and MQTT systems  
✅ **Wiegand Keypad** - PIN, RFID card, or fingerprint control via Wiegand protocol  
✅ **Power Monitoring** - Detect and alert on power outages with UPS support  
✅ **Real-time Clock** - Precise timekeeping without internet via hardware RTC  
✅ **Responsive Design** - Multi-language web interface with dark mode support  


## What You Need

### Required Components
1. **Existing Security System** - Wired sensors, keypads, and sirens from your current system
2. **Raspberry Pi** - Pi Zero 2 W or Pi 4 (minimum 1GB RAM recommended)
3. **ArPI Interface Board** - Custom adapter board for connecting security system components
4. **MicroSD Card** - Class 10, 16GB+ capacity for reliable storage

### Optional Enhancements  
- **GSM Module** - For SMS/voice notifications without internet (SIM900A compatible)
- **Real-time Clock** - DS1307 module for accurate timekeeping offline
- **UPS with Battery** - Uninterruptible power supply for power outages
- **Wiegand Keypad** - Modern keypad with PIN/RFID/fingerprint support

### System Requirements
- **Network Connection** - Ethernet or WiFi for remote access
- **Power Supply** - 5V 3A adapter with optional battery backup
- **Enclosure** - Weather-resistant housing for outdoor installations


## No ArPI Board, No Problem!

If you don't have the ArPI interface board, you can still use the software with a Raspberry Pi.
The simulator mode allows you to test the system without any external hardware.
You can control channels, power input, and keypad inputs through a simple JSON interface.

For more details on how to use the simulator, see the [Simulator](end_users/simulator.md) documentation.
