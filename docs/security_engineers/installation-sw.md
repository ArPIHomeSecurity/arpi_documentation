You can find the released images on GitHub for the Raspberry PI Zero W 2. The images have the
the ArPI software preinstalled and configured.

1. Download the image from [GitHub](https://github.com/ArPIHomeSecurity/arpi_management/releases/)
2. Use [Etcher](https://www.balena.io/etcher/) to write to an SD card
3. Configure WiFi
    1. Generate WIFI passphrase
        ```
        wpa_passphrase <ssid> [passphrase]
        ```
    2. Append the output to the file "/rootfs/etc/wpa_supplicant/wpa_supplicant.conf"

4. Start the Raspberry PI with the SD card
5. Default access:
    * Web application https://arpi.local
        * Registration code: `ABCD1234`
        * Access code: `1234`
    * SSH username and password: `argus`:`Argus.1234`
    ```bash
    ssh argus@arpi.local
    ```

!!! note
    You can find the default production settings: [Project folder]/server/src/data.py - method env_prod
