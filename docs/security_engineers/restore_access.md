When there isn't any user with administrator privileges who has access to the
system you need to register a new device at least for one administrator. That
is only possible through terminal access to the system.

1. Login to the device
```bash
ssh -i arpi_rsa argus@arpi.local
```

2. Generate new registration code hash
```bash
cd server
pipenv run src/hash.py {registration code}
```

3. Add registration code to user
```
# start postgres terminal (as argus user)
psql
# Find the id of the user
> SELECT * FROM "user";
# Update the user
> UPDATE "user" SET registration_code='{output of the hash.py}' WHERE id={user id};
```

4. Open the web interface
5. Unregister the device on the login page
6. Register device again using the {registration code}


!!! Warning
    Be careful of using the different formats of the registration code.
