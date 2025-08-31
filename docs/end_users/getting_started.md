# Getting Started with ArPI

As a user of the ArPI Home Security System, first you need to set up your Raspberry Pi and install the ArPI software
from the [software](../security_engineers/installation-sw.md) and [hardware](../security_engineers/installation-hw.md) installation guides.

Once you have the system running, you can start using it by following these steps:

## 1. Registering Devices

To access the system, you need to register your devices. This is done by generating a registration code for each device.
There is a default registration code that is valid for the administrator user: `ABCD1234`.

For more details on how to register devices, see the [registration](register.md) section.

## 2. Accessing the System

Users can access the system through the web interface locally or remotely, but the remote access requires
some additional setup (see: [Network configuration](network.md))

* For local access, try the default address: `http://arpi.local`

On the web interface, you can login with your user's access code.
The default access code for the admin user is `1234`.

!!! danger
    The default access code is not secure. You should change it immediately after the first login.


For more details on how to access the system, see the [Login](login.md) section.

## 3. Configure areas

You can configure areas in the system to manage different parts of your home or office. Areas can be armed or disarmed independently.

For more details on how to configure areas, see the [Areas](areas.md) section.

## 4. Configure zones

Zones are used to define specific group of sensors with the same behavior.
You can create zones for different work modes, such as "Home", "Away", or "Night".

For more details on how to configure zones, see the [Zones](zones.md) section.

## 5. Configure sensors
 
Sensors are the devices that detect events in your home or office, such as motion, door/window status, etc.
You can add sensors to the system and configure their behavior.

For more details on how to configure sensors, see the [Sensors](sensors.md) section.

That's it! You are now ready to use the ArPI Home Security System.
