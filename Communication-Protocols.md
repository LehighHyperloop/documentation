All systems will communicate with the main controller via a [mosquitto](https://mosquitto.org/) MQTT server.

# Protocol

Topics for controllers will be in the following format:
```
/subsystem/<name>(/<verb>)
{
    "<attribute>": "<value>",
    "<attribute>": "<value>",
    ...
}
```
All subsystem controllers will publish to their respective parent topics with status updates every X ms (TODO: DETERMINE LATENCY ACROSS NETWORK).

Currently used verbs:
- set


# Subsystems

Compressor (`/subsystem/compressor`)
----------
States:
- STOPPED
- VFD_STARTING
- COMPRESSOR_STARTING
- RUNNING
- COMPRESSOR_STOPPING
- VFD_STOPPING
- FAULT
- ESTOP


Fan (`/subsystem/fan`)
---
States:
- STOPPED
- STARTING
- RUNNING
- STOPPING
- FAULT
- ESTOP