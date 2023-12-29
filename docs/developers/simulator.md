
For testing the system you can use a simulator for controlling the channels and the power input.
With the simulator you can change the state of the channels and the power input without any hardware.
The simulator is available only from the terminal and you can use it in the local development environment
but also in the deployed system.

The simulator is a simple Python script which you can start with the following command:

```bash
# in the local development environment
pipenv run src/simulator.py 

# in the deployed system
cd /home/argus/server
./src/simulator.py
```

The simulator is not part of the deployed system and you have to copy it manually to the server 
and prepare the environment for it.

```bash
sudo pip install textual==0.1.18
sudo pip install pyfiglet==0.8.post1
```

The simulator communicates with the service through two files.
The files will be created on the first execution of the simulator.

* channels.json
```json
{
    "CH01": 0.247828446754,
    "CH02": 0.247828446754,
    "CH03": 0.247828446754,
    "CH04": 0.247828446754,
    "CH05": 0.247828446754,
    "CH06": 0.247828446754,
    "CH07": 0.247828446754,
    "CH08": 0.247828446754,
    "CH09": 0.247828446754,
    "CH10": 0.247828446754,
    "CH11": 0.247828446754,
    "CH12": 0.247828446754,
    "CH13": 0.247828446754,
    "CH14": 0.247828446754,
    "CH15": 0.247828446754
}
```
* power.json
```json
{
    "POWER": 0.93736749953
}
```

When the simulator is prepared you have to configure the argus_monitor service for using the simulator.

```bash
# change the configuration in the ~/server/.env
USE_SIMULATOR=true

# restart the service
sudo systemctl restart argus_monitor
```
