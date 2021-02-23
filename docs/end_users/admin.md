
## Zones

You can see the list of the zones in the security system.
Zones can be added/removed and updated.

Every zone can be configured based on the arm types.
1. If alerting is enalbed or not
2. The delay between the alert on he sensor and the system alert

A special type of the zones is the tamper. Tamper alerts can be triggered
when the system is not armed.

## Sensors

You can see the list of the sensors in the security system.
Sensors can be added/removed and updated.

Sensors are connected to channels on the board.
Every sensor can be enabled and disabled. Disable sensor doens't trigger alerts.
The sensors will be assigned to a zone, which defined the alert behaviour for them.
Any other options currently are only documentation (they don't affect the alerting).

## Clock

You can see the date and time from three sources:

1. Network
2. System
3. Hardware clock

When no network time is available it is possible to change the system clock.
You can configure the timezone, too.

## Notifications

The system is able to send notifications by email and SMS.

### Email

Configure an SMTP credential for sending emails to an email address.

### GSM

Configure the GSM module settings to be able to send SMS messages to the given phone number.

## Networking

We assume that the security system is installed behind a firewall/router with NAT.


### Dynamic DNS

When the users want to access the security system remotely (not from the home network)
you can configure the system to use a dynamic DNS provider and access it on
the given domain name.

In case of the public IP address changes the system will update the domain name
automatically.

!!! warning
    When you want to access the system on the local network with the same
    remote domain name you have the following options:

    1. Use a router with NAT loopback
    2. Use a local DNS server for resolving the domain name to the local IP of the  security system

### Restrict the access to the host name

If you enable this option the security system will be accessible only on the
hostname you defined.

### Enable SSH connection

You can control the status of the SSH server with this option

## Users

You can manage the users of the system: add/remove/update.

You can generate new registration code for the users.
Every registration code can have an expiry time.

After the registration code is generated it will be accessible until the dialog is closed.

!!! warning
    Always share the regsitration and access codes securly.
