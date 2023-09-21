
This section is for testing the functionalities of the ArPI board.
Before any tests please ensure that the services are stopped.
```bash
sudo systemctl stop argus_server argus_monitor nginx
sudo systemctl status argus_server argus_monitor nginx
```

## Sensors and relays

After ssh to the argus user:
```bash
> cd server
> sudo python src/tester.py sensor
Creating sensor adapter for GPIO pin: 19
Creating sensor adapter for GPIO pin: 20
Creating sensor adapter for GPIO pin: 26
Creating sensor adapter for GPIO pin: 21
Creating sensor adapter for GPIO pin: 12
Creating sensor adapter for GPIO pin: 6
Creating sensor adapter for GPIO pin: 13
Creating sensor adapter for GPIO pin: 16
Creating sensor adapter for GPIO pin: 7
Creating sensor adapter for GPIO pin: 1
Creating sensor adapter for GPIO pin: 0
Creating sensor adapter for GPIO pin: 5
Creating sensor adapter for GPIO pin: 23
Creating sensor adapter for GPIO pin: 24
Creating sensor adapter for GPIO pin: 25
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']
Values: ['1', '1', '0', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1', '1']


> sudo python src/tester.py relay
Relay adapter setup finished
Control relay 0 to 1, [1, 0, 0, 0, 0, 0, 0, 0]
Control relay 1 to 1, [1, 1, 0, 0, 0, 0, 0, 0]
Control relay 2 to 1, [1, 1, 1, 0, 0, 0, 0, 0]
Control relay 3 to 1, [1, 1, 1, 1, 0, 0, 0, 0]
Control relay 4 to 1, [1, 1, 1, 1, 1, 0, 0, 0]
Control relay 5 to 1, [1, 1, 1, 1, 1, 1, 0, 0]
Control relay 6 to 1, [1, 1, 1, 1, 1, 1, 1, 0]
Control relay 7 to 1, [1, 1, 1, 1, 1, 1, 1, 1]
Control relay 0 to 0, [0, 1, 1, 1, 1, 1, 1, 1]
Control relay 1 to 0, [0, 0, 1, 1, 1, 1, 1, 1]
Control relay 2 to 0, [0, 0, 0, 1, 1, 1, 1, 1]
Control relay 3 to 0, [0, 0, 0, 0, 1, 1, 1, 1]
Control relay 4 to 0, [0, 0, 0, 0, 0, 1, 1, 1]
Control relay 5 to 0, [0, 0, 0, 0, 0, 0, 1, 1]
Control relay 6 to 0, [0, 0, 0, 0, 0, 0, 0, 1]
Control relay 7 to 0, [0, 0, 0, 0, 0, 0, 0, 0]
Relay adapter cleanup finished
```

## GSM

You can use the minicom tool to test the GSM module.

```bash
# install the tool
sudo apt install minicom

# start the tool on the serial port
sudo minicom -D /dev/ttyAMA0 --baudrate 9600
```
You can turn on the local echo to see your commands: CTRL+A-Z-E

Setting the PIN code:
```
AT+CPIN="1234”
```

Testing PIN code:
```
AT+CPIN?
```

Sending SMS:
```
AT+CMGF=1
OK
AT+CMGS="+31628870634"
> This is the text message^Z
+CMGS: 198
OK
```

## RTC


```bash
> lsmod | grep ds1307     
rtc_ds1307             28672  0

> ls -lah /dev/i2c* 
crw-rw---- 1 root i2c 89, 1 Sep 21 15:32 /dev/i2c-1
crw-rw---- 1 root i2c 89, 2 Sep 21 15:32 /dev/i2c-2

> sudo i2cdetect -y 1     
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:                         -- -- -- -- -- -- -- -- 
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- 
50: -- -- -- -- -- -- -- 57 -- -- -- -- -- -- -- -- 
60: -- -- -- -- -- -- -- -- UU -- -- -- -- -- -- -- 
70: -- -- -- -- -- -- -- --                 
```
