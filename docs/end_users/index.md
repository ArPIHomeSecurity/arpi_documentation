This section describes how to use the ArPI security system.

## Roles

Currently the system has two types of roles:

* user: they can only arm or disarm the system and get some read only information
* admin: they can access any functionality of the system


## Common functions

On this page we describe the function that admins and users can use similarly.

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
as well when the tamper circuit is interrupted.

### Sessions

After the login to the security system you have a session with a 15 minutes timeout.
The timeout is restarted with every change on the application.

### Language

You can change the language of the application from the menu.
You can contribute in the translation:

* [Translations](../developers/web_application.md#translations)
* [Source code](https://github.com/ArPIHomeSecurity/arpi_webapplication)
