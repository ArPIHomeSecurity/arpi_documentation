When there isn't any user with administrator privileges who has access to the
system you need to register a new device at least for one administrator. That
is only possible through terminal access to the system.

1. Login to the device
```bash
ssh -i arpi_rsa argus@arpi.local
```

2. Generate new registration code hash
```bash
$ cd server

# list users
$ ./src/new_registration_code.py
Users:
ID: 33774305 = Administrator (admin):

# generate code for the user with id 33774305
$ ./src/new_registration_code.py -u 33774305
User doesn't have registration code

------------------------------
Code generated for user (id: 33774305): Administrator
New registration code: 293ACECEF9FF
The code never expires
```

4. Open the web interface
5. Unregister the device on the login page
6. Register device again using the generated registration code
([register device](../end_users/register.md))



