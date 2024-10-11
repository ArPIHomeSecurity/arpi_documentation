
For testing the system you can use a simulator for controlling the channels, the power input and the
keypad with RFID cards. You can also see the state of the outputs.
You can change the state of the channels or the power input, send key presses or RFID card ids 
from the keypad without any hardware.
The simulator is available only from the terminal and you can use it in the local development
environment by default but also can be enabled in the deployed system.

The simulator is a simple Python script which you can start with the following command:

```bash
# in the local development environment
pipenv run src/simulator.py 

# in the deployed system
cd /home/argus/server
./src/simulator.py
```

The simulator communicates with the service through two files.
The files will be created on the first execution of the simulator.

* simulator_input.json
```json
{
    "CH01": 0,
    "CH02": 0,
    "CH03": 0,
    "CH04": 0,
    "CH05": 0,
    "CH06": 0,
    "CH07": 0,
    "CH08": 0,
    "CH09": 0,
    "CH10": 0,
    "CH11": 0,
    "CH12": 0,
    "CH13": 0,
    "CH14": 0,
    "CH15": 0,
    "POWER": 0
}
```
* simulator_output.json
```json
{
    "GO": 0,
    "R1": 0,
    "R0": 1,
    "O4": 0,
    "O3": 0,
    "O2": 0,
    "O1": 0,
    "O0": 0
}
```
* simulator_keypad.json
```json
{
    "pending_bits": 0,
    "data": []
}
```

When the simulator is prepared you have to configure the argus_monitor service for using the simulator.

```bash
# change the configuration in the ~/server/.env
USE_SIMULATOR=true

# restart the service
sudo systemctl restart argus_monitor
```
