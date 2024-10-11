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


* **Name**: A short name of the output.
* **Description**: A longer description of the output.
* **Channel**: The output terminal of the board.
* **Trigger**:
    * Area: The output will be triggered when the selected area is armed.
    * System: The output will be triggered when the system is armed.
    * Button: The output will be triggered when the button is pressed on the web interface.

* **Delay**: The delay before the output is activated.
* **Duration**: The duration of the output activation. Only button type triggers can have duration.
