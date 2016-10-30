Intro
-----

All systems will communicate with the main controller via a [mosquitto](https://mosquitto.org/) MQTT server.


Subsystems
----------
- Compressor
- Fan
- Batteries


Compressor
----------
- /subsystem/compressor/state
- /subsystem/compressor/set

States:
- STOPPED
- VFD_STARTING
- COMPRESSOR_STARTING
- RUNNING
- COMPRESSOR_STOPPING
- VFD_STOPPING
- FAULT
- ESTOP

Fan
---
- /subsystem/fan/state
- /subsystem/fan/set

States:
- STOPPED
- STARTING
- RUNNING
- STOPPING
- FAULT
- ESTOP