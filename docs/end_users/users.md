# Users
<img src="https://img.shields.io/badge/Access-Administrator-red?style=square">

A list of the users is displayed with registered cards and registration code expiries.
You can add a new user with a name and an access code. When editing a user you can update the password.


## Device registration

When a user wants to access the system from a device you can generate a new registration code.
You can define the expiry time of the code if you want (otherwise unlimited time).

!!! warning
    The registration code is visible only in the dialog!
    You need to generate new if you lose it.

The registration code can be deleted from the user list view.


## Card registration

If a Wiegand keypad is attached to the system users can register their RFID cards.

1. In the list user select the action "Register card" of the given user
2. Put the RFID card to the Wiegand keypad

## SSH keys

You can add an SSH key to the user, so the user can access the system via SSH using the key.
Without the key, the user can access on SSH only with the password.

See the [Network terminal access](network.md#terminal-access) section.

## Edit user

You can edit the user's name and access code. You can also delete the user.