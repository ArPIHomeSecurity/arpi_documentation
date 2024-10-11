# Zone list
<img src="https://img.shields.io/badge/Access-User-orange?style=square">

You can list the zones of the system. The zones are a set of sensors that are grouped together.
The zones can be sorted manually with drag and drop.

The configuration of the zone displays the alert and arm delays of the sensors based on the arm state.

The zone shows the list of the assigned sensors. If you want to move a sensor to another zone, you can do it by editing the sensor and changing the zone.

Zones can be deleted if they have no sensors assigned.

---
## Edit zone
<img src="https://img.shields.io/badge/Access-Administrator-red?style=square">

* **Name**: A short name of the zone.
* **Description**: A longer description of the zone.

Use the check boxes if you want to enable alerting in the given arm state. You can set a delay
before arming the sensors and a delay before alerting.

* **Arm states**: The arm states of the system. The arm states are the following:
    * **Disarmed**: The system is not armed.
    * **Armed home**: The system is armed in home mode. The home mode is used when you are at home.
    * **Armed away**: The system is armed in away mode. The away mode is used when you are not at home.

* **Delays**:
    * **Arm delay**: The delay before arming the sensors. It helps to leave the house after arming
    the system.
    * **Alert delay**: The delay before alerting. It helps to disarm the system before the alerting.

!!! Hint
    For creating a tamper zone you have to enable the alerting in all the arm states and set
    the delays to 0.
