<img src="https://img.shields.io/badge/Access-Administrator-red?style=square">


* **Syren volume**: 
    * Normal: The syren will be used as normal.
    * Silent alert: The syren will not be used in case of an alert.
    * Loud alarm: The syren will be forced to sound in case of an alert even if the sensor (the source of the alert) is configured as silent.

* **Syren timing**:
    * Delay: The syren will be delayed with the configured delay after the alert.
    * Stop time: The syren will be stopped after the configured stop time. 0 means no stop time.

* **Alert sensitivity**: You can set custom sensitivity for the system.
    * Custom: You can set the sensitivity of the syren with a sliding time window and a threshold. The syren state will be evaluated as active if the number of active states in the time window is greater than the threshold. This is useful for sensors that are not reliable. This option can be overridden by the sensor settings. See: [Sensor configuration](sensors.md)

The "Test" button will sound the syren for 5 seconds. This is useful for testing the syren.
