# Network
<img src="https://img.shields.io/badge/Access-Administrator-red?style=square">

We assume that the security system is installed behind a firewall/router with NAT.
You have to forward the ports 80 and 443 on the router to the IP address of the security system.

* Port 80 is open for https://letsencrypt.org/ certificate validation and redirect to port 443
* Port 443 is for secure communication with the security system

## Dynamic DNS

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
    3. Setup the /etc/hosts file on the client device

## Restrict the access to the host name

If you enable this option the security system will be accessible only on the
host name you defined.

## Enable SSH connection

You can control the status of the SSH server with this option