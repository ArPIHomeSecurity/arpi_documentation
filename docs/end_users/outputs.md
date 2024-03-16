# Output list
<img src="https://img.shields.io/badge/Access-User-orange?style=square">

You can list the outputs of the system. The outputs are terminals of the board that can send signals to other 
devices when an event is triggered. Event sources can be the arm state of the system or the areas, but you can
also create a button as event source to trigger the output manually. The buttons will be
displayed on the main page of the system.

The output terminal names are R0, R1 and O0..O4.

The syren is connected by default to the GO+/GO- outputs

The list of the outputs give you an overview of the outputs and their settings.

The outputs can be sorted manually with drag and drop.


---

## Edit output
<img src="https://img.shields.io/badge/Access-Administrator-red?style=square">

When editing an output you can set the name and description first. The next option is the output terminal.
Already connected output terminals are disabled in the dropdown list.

You can select the event source:
* system: active when the system is armed
* area: active when a selected area is armed
* button: active when the button is pressed

For the output sign you can configure the delay and the duration. The delay is the time between the event and the activation of the output. The duration is the time the output is active.

Only buttons can have duration. The duration is the time the button is active after pressing.

