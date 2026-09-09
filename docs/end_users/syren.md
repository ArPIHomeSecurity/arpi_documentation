![Access: Administrator](https://img.shields.io/badge/Access-Administrator-red?style=square)

Configure global sounder behaviors, operational delays, and alert thresholds for the primary syren.

---

### Syren Volume

Controls the acoustic output level of the syren during system alerts.

* **Normal**: The syren operates at default acoustic volume when an alert condition occurs.
* **Silent alert**: The syren remains silent during an alert. Notifications (SMS/Email/MQTT) will still be dispatched.
* **Loud alarm**: Forces maximum syren output during an alert, overriding individual sensors configured as silent.

### Syren Timing

Manages operational time offsets and duration limits for the alarm sounder.

* **Delay**: Time offset (in seconds) between initial alert detection and physical syren activation.
* **Stop time**: Total duration (in seconds) the syren will sound before automatically silencing. A value of `0` disables auto-stop (syren sounds continuously until manual disarm).

```text
          Alert Triggered                          Syren Muted
              |                                       |
              v<- Delay (s) ->|<--- Stop Time (s) --->|
        ======+---------------+=======================+======> Time (s)
                            |                       |
                            +-- Syren Active (ON) --+
```

### Alert Sensitivity (Duty-Cycle Threshold)

Alert sensitivity prevents false alarms from unstable or fluttering sensors by measuring the duty cycle of the active signal within a moving time window.

* **Custom Sensitivity**: Instead of triggering immediately on a brief contact state change, the system measures what percentage of time the sensor remains active during a sliding time window.
  * **Time Window**: The rolling duration (in seconds) over which the sensor state is monitored.
  * **Threshold Percentage**: The minimum active time percentage (0–100%) required to activate the syren.

> **Formula:**
> 
> **Active Ratio (%) = (Total Active Time in Window / Time Window Duration) * 100**
> 
> The syren triggers when **Active Ratio (%) > Threshold (%)**.

#### Practical Example

If the **Time Window** is set to **10 seconds** and the **Threshold** is **40%**:

* A brief 1-second glitch accounts for 10% active time (less than 40%) -> **No alarm triggered**.
* If the sensor flickers or stays closed for a total of **5 seconds** out of 10 seconds (50% active time, which exceeds 40%) -> **Syren triggers**.

```text
                  |<----- Sliding Window (10s) ------------->|

    Sensor [ High ]             |--|     |----|         |----|
    Signal [ Low  ]_____________|  |_____|    |_________|    |
                                (1s)      (2s)           (2s)

    Active Time: 1s + 2s + 2s = 5s / 10s (Duty Cycle = 50%)
    Threshold  : ------------ 40% Duty Cycle Line ------------

    Result     : 50% > 40% Threshold  ===>  [ ALARM ACTIVATED ]
```

!!! Note
    **Sensor Override**: Individual sensor properties can override the global syren sensitivity settings. See [Sensor configuration](../sensors/).

### Test syren

The "Test" button will sound the syren for 5 seconds. This is useful for testing the syren.
