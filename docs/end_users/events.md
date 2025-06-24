<img src="https://img.shields.io/badge/Access-User-orange?style=square">

The Events page provides a comprehensive view of all arm/disarm activities in your ArPI security system. This feature helps you monitor system usage, track user activities, and review security events for analysis and troubleshooting.

## Overview

The events list displays all arm and disarm actions performed on your security system, including both successful operations and any alerts that may have occurred during these processes.

## Event Information

Each event entry shows the following information:

* **Date and time** - When the arm/disarm action occurred
* **User** - Who performed the action (if identified)
* **Action type** - Whether it was an arm away, arm stay, or disarm operation
* **Status** - Success or failure of the operation
* **Alert details** - Any alerts or security issues that occurred
* **Sensor timeline** - Visual representation of sensor activation delays

## Filtering Events

You can filter the events list using the following criteria:

### Arm Type
Filter events by the type of arming operation:

* **Arm Away** - Events when the system was armed for leaving the premises
* **Arm Stay** - Events when the system was armed while staying at home
* **Disarm** - Events when the system was disarmed

### User
Filter events by specific users to see their individual activity:

* Select a specific user from the dropdown
* View only events triggered by that user
* Useful for tracking individual user behavior

### Date Range
Filter events by time period:

* **Start date** - Show events from a specific date onwards
* Use the date picker to select your desired time range
* Helpful for reviewing recent activity or investigating specific incidents

### Alert Status
Filter by whether alerts occurred:

* **With alerts** - Show only events that triggered security alerts
* **Without alerts** - Show only normal operations
* **All events** - Display both types

## Event Timeline

Each event displays a detailed timeline showing:

* **Sensor activation sequence** - The order in which sensors were triggered
* **Timing delays** - How long each sensor took to activate after the arm command
* **Zone information** - Which zones were affected during the event
* **Alert triggers** - Any sensors that caused security alerts

This timeline helps you:
* Understand the sequence of events during arming/disarming
* Identify sensors with unusual delays
* Troubleshoot system behavior
* Verify proper zone configuration

## Event Sorting

Events are automatically sorted by their start date, with the most recent events displayed first.
