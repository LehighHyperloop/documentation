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
All subsystem controllers will publish to their respective parent topics with status updates every X ms (TODO: DETERMINE LATENCY ACROSS NETWORK) or during any state change.

Currently used verbs:
- set

Global
------
States:
- STANDBY
- PRE_LAUNCH
- VROOOOOOOOOOM
- PAST_PUSHER
- COASTING
- STOPPED
- DISENGAGED


# Subsystems

Compressor (`/subsystem/compressor`)
------------------------------------
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
----------------------
States:
- STOPPED
- RUNNING
- FAULT
- ESTOP

Propulsion (`/subsystem/propulsion`)
------------------------------------
States:
- STOPPED
- FORWARD
- FAULT
- ESTOP

Levitation (`/subsystem/levitation`)
------------------------------------
States:
- STOPPED
- RUNNING
- FAULT
- ESTOP

Inverters (`/subsystem/inverters`)
----------------------------------
States:
- STOPPED
- RUNNING
- FAULT
- ESTOP

Braking (`/subsystem/braking`)
------------------------------
States:
- OFF
- ON
- FAULT
- ESTOP
