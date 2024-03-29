There is a tool for manipulating the database. It is located in the `src` directory and
is called `data.py`. It has two main functions: `create` and `delete`.

## Clean up database
The `delete` function is used to clean up the database.
It removes all data from the database.

```bash
➜  server ./src/data.py -d
Clean up database...
 - Clear table disarm
 - Clear table arm_sensor
 - Clear table arm
 - Clear table alert_sensor
 - Clear table sensor
 - Clear table output
 - Clear table keypad
 - Clear table card
 - Clear table zone
 - Clear table user
 - Clear table sensor_type
 - Clear table option
 - Clear table keypad_type
 - Clear table area
 - Clear table alert
Database is empty
```

## Create new environment
The `create` function is used to create a new environment in the database.
```bash
➜  server ./src/data.py -c prod
Creating 'prod' environment...
 - Created admin user
 - Created sensor types
 - Created keypad types
 - Created keypads
Environment created
```

There are different environments prepared:

- `prod` - production environment
- `live_01` - live environment
- `test_01` - test environment

