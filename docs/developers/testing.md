## Testing

### GSM

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
