## Global states
| States     | Telemetry States |
|------------|------------------|
| Standby    | Idle             |
| Prelaunch  | Idle             |
| Launch     | Ready            |
| Pushing    | Pushing          |
| PastPusher | Coast            |
| Braking    | Braking          |
| Stopped    | Braking          |
| Disengaged | Idle             |
| Fault      | Fault            |

## SpaceX Telemetry States
0. Fault – If seen, will cause SpaceX to abort the tube run.
1. Idle – Any state where the pod is on, but not ready to be pushed.
2. Ready – Any state where the pod is ready to be pushed.
3. Pushing – Any state when the pod detects it is being pushed.
4. Coast – Any state when the pod detects it has separated from the pusher vehicle.
5. Braking – Any state when the pod is applying its brakes.


## States
- STANDBY
  - Telemetry: Idle (1)
  - Transition conditions to PRELAUNCH:
    - Receive manual transition command from operators
- PRELAUNCH
  - Telemetry: Idle (1)
  - Set subsystem states:
    - Suspension: RUNNING
    - Inverters: RUNNING
    - Fan: RUNNING
    - Compressor: RUNNING
    - Levitation: RUNNING
    - LateralControl: EXTENDED
    - Propulsion: STOPPED
    - Braking: OFF
    - Wheels: UP
  - Transition conditions to LAUNCH:
    - All subsystem states satisfied
    - Master & Slave inverter output wattage balanced
    - Levitation Air Tank >= 100 psi
    - Pneumatic Air tank >= 100 psi
    - Receive manual transition command from operators
- LAUNCH
  - Telemetry: Ready (2)
  - Transition conditions to PUSHING:
    - Pod forward acceleration >= 0.2g
- PUSHING
  - Telemetry: Pushing (3)
  - Set subsystem states:
    - Propulsion: RUNNING
  - Transition conditions to PASTPUSHER:
    - Pod position > 1600ft
    - Time in pushing state > PUSHING_TIME_AT_MAX_ACCELERATION (TBD, waiting on mechanical team)
- PASTPUSHER
  - Telemetry: Coast (4)
  - Transition conditions to COASTING:
    - Pod position >= COAST_DISTANCE (TBD)
- COASTING
  - Telemetry: Coast (4)
  - Set subsystem states:
    - Propulsion: COASTING
  - Transition conditions to WHEEL_BRAKING:
    - Pod position >= WHEEL_BRAKING_DISTANCE (TBD, estimated 1000ft from end of track, waiting on mechanical team)
- WHEEL_BRAKING
  - Telemetry: Braking (5)
  - Set subsystem states:
    - Propulsion: BRAKING
  - Transition conditions to FRICTION_BRAKING:
    - Pod position >= FRICTION_BRAKING_DISTANCE (TBD, estimated 400ft from end of track, waiting on mechanical team)
- FRICTION_BRAKING
  - Telemetry: Braking (5)
  - Set subsystem states:
    - Braking: ON
  - Transition conditions to STOPPED:
    - Pod Velocity == 0
- STOPPED
  - Telemetry: Braking (5)
  - Set subsystem states:
      - Propulsion: STOPPED
  - Transition conditions to DISENGAGED:
    - Receive manual transition command from operators
- DISENGAGED
  - Telemetry: Idle (1)
  - Set subsystem states:
    - Levitation: STOPPED
    - Braking: OFF
    - Compressor: STOPPED
    - Fan: STOPPED
  - Transition conditions:
    - Receive manual transition command from operators
- FAULT
  - Telemetry: Fault (0)
  - Transition conditions:
    - Can only be exit through manual transition command / reset
