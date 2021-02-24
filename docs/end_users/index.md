This section describes how to use the ArPI security system.

## Roles

Currently the system has two types of roles:

* user: they can only arm or disarm the system and get some read olny information
* admin: they can access any functionalty of the system


## Common functions

On this page we describe the function that admins and users can use similarly.
### Registering device

Registering a device for the security system will enable a specific
user to access the system from the registered device (PC, mobile, etc.).
Users should receive registration codes from the administrator(s) of the system.

Accepted registration code formats:

* ABC-DEF-123
* ABCDEF123
* abc-def-123
* abcdef123

!!! todo
    Define the default registration code of admin after first install.

### Login
You can login to the security system with a registered user on a registered device.
Use the access code of the user to login the system.

Accepted access code format: any digits with at least 4 length

!!! todo
    Define the default access code of admin after first install.

### Arm/disarm

Logged in users can arm and disarm the system on the main page.

### Sabotage

You can receive sabotage alert from the security system in disarmed state
as well when the tamper circiut is interrupted.

### Sessions

After the login to the security system you have a session with a 15 minutes timeout.
The timeout is restarted with every change on the application.

### Language

You can change the language of the application from the menu.
You can contribute in the translation:

* ![translations](developers/web_application#translations)
* https://github.com/ArPIHomeSecurity/arpi_webapplication
