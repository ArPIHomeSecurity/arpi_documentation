# Locations/Setup
<img src="https://img.shields.io/badge/Access-User-orange?style=square">

ArPI Home Security supports managing multiple locations. Each location represents a separate site (such as home, office, or other property) that you can control from the application.

You can access the application of the ArPI Home Security system in 3 ways:

1. Directly on your Raspberry PI device (default: [https://arpi.local](https://arpi.local))
1. On the web [https://app.arpi-security.info](https://app.arpi-security.info)
2. Through the mobile app available for Android devices: [ArPI Home Security](https://play.google.com/store/apps/details?id=com.arpi.webapplication)


!!! note
    The application on the Raspberry PI can access only to the one location configured on the device.
    Multiple locations can be managed through the web or mobile app.


## Configure location

To add or change a location, you need to set the **domain** and the **port** of the ArPI server. The default port is **443** (for secure HTTPS connections).

!!! note
    In case of using the security system on a custom domain with a **self-signed certificate**,
    you may need to add an exception in your browser to access the web interface.

After entering the domain and port, use the >>:octicons-search-16:<< icon to verify the configuration. If the connection is successful, you can save the location and proceed to the login screen.

---
**Steps:**

1. Enter the domain (e.g., `arpi.example.com`).
2. Enter the port (default: `443`).
3. Click the >>:octicons-search-16:<< icon to verify if the configuration is correct.
4. If verified, save the location.
5. Continue to login.

