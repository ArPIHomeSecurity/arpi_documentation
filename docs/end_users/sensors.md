# Sensor list
<img src="https://img.shields.io/badge/Access-User-orange?style=square">

You can list the sensors of the system. The sensors are the devices that are used
to detect the events. The sensors can be sorted manually with drag and drop.

You need to connect the sensors to the input terminals of the board. The input terminals are named CH01-CH15.

List of the sensors give you an overview of the sensors and their settings.

---

## Edit sensor
<img src="https://img.shields.io/badge/Access-Administrator-red?style=square">

* **Channel**: When editing a sensor you can set the input terminal first. Already connected input terminals are disabled in the dropdown list. You can also disconnect a sensor if you don't want
to use it, but keep the other settings.

* **Type**: The type of the sensor is currently not used in the behavior of the system, but 
it is used to give you a hint of the type of the sensor.

* **Description**: You can set a longer description of the sensor.

* **Enabled** If the sensor is disabled, it will not be used in the system for alerting.

* **Hidden**: If the sensor is hidden, it will not be displayed in the list of sensors on
the main page.

* **Syren**: You can control how to use the syren in case of an alert coming from this sensor.
    * System: The syren will be controlled by the system.
    * Load: The syren will be used independently from the system.
    * Silent: The syren will not be used independently from the system.

* **Sensitivity**: You can control how to evaluate the active state of the sensor.
    * System: The sensitivity will be controlled by the system.
    * Instant alert: The sensor will be evaluated as active immediately.
    * Custom: You can set the sensitivity of the sensor with a sliding time window and a threshold.
    The sensor state will be evaluated as active if the number of active states in the time window
    is greater than the threshold.

* **Area**: The sensor must be assigned to an area and will be used for alert when the area
is armed. See: [Area configuration](areas.md)

* **Zone**:  The sensor must be assigned to a zone and will be used for alert based on the zone configuration. See: [Zone configuration](zones.md)
