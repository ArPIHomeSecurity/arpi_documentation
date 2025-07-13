# Software Installation Guide

## Pre-built Images (Recommended)

Download ready-to-use Raspberry Pi images with ArPI pre-installed from our GitHub releases.

!!! note "What You'll need"
    - SD card (4GB or larger) + SD Card reader
    - Basic knowledge of using SSH

### Quick Installation Steps

1. **Download Image**
      
      Get the latest release from [GitHub Releases](https://github.com/ArPIHomeSecurity/arpi_management/releases/)

2. **Flash to SD Card**
      - Use [Raspberry Pi Imager](https://www.raspberrypi.org/software/) (recommended) or [Balena Etcher](https://www.balena.io/etcher/)
      - Select downloaded image and target SD card

3. **WiFi Configuration**

      There are two methods to configure WiFi for headless operation. You can choose either based on your preference:

      * **Using NetworkManager (recommended)**:
        
        Create a WiFi connection file in the `rootfs` partition at `/etc/NetworkManager/system-connections/wifi.nmconnection`:
        ```ini
        [connection]
        id=wifi
        type=wifi
        autoconnect=true

        [wifi]
        mode=infrastructure
        ssid=YourSSID

        [wifi-security]
        auth-alg=open
        key-mgmt=wpa-psk
        psk=YourPassword

        [ipv4]
        method=auto

        [ipv6]
        addr-gen-mode=default
        method=auto
        ```
        Update file permissions:
        ```bash
        sudo chmod 600 /rootfs/etc/NetworkManager/system-connections/wifi.nmconnection
        sudo chown root:root /rootfs/etc/NetworkManager/system-connections/wifi.nmconnection
        ```

      * **Legacy method using wpa_supplicant**:
        
        ```bash
        # Generate encrypted WiFi credentials
        wpa_passphrase "YourSSID" "YourPassword"
        
        # Add output to wpa_supplicant.conf
        sudo nano /rootfs/etc/wpa_supplicant/wpa_supplicant.conf
        ```


4. **System Access**
      - **Web Interface**: https://arpi.local
         - Default admin registration code: `ABCD1234`
         - Default access code: `1234`
      - **SSH Access**: `ssh argus@arpi.local`
         - Default password: `Argus.1234`

## Security Hardening (Post-Installation)

!!! warning "Change Default Credentials"
    Immediately change default passwords and codes after first login!

### Essential Security Steps

1. **Change Default Passwords**
   ```bash
   # Change system user password
   passwd argus
   
   # Change ArPI admin access code via web interface
   # Settings > Users > Admin > Change Access Code
   ```

2. **SSH Key Authentication**
      - Generate SSH key
   See: [ArPI User SSH key](../end_users/users.md#ssh-keys)

      - Disable password authentication
   See: [ArPI Network Settings](../end_users/network.md#terminal-access)


!!! info "Note"
    For a customized installation, follow the [Developers Installation Guide](../developers/installation.md).
