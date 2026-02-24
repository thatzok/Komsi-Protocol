# KOMSI Command List

This list defines all valid command codes, their data types, and value definitions for the KOMSI protocol.

| Code  | Name               | Type             | Unit       | Value Definition                    | Comments                     |
|:------|:-------------------|:-----------------|:-----------|:------------------------------------|:-----------------------------|
| **A** | Ignition           | Boolean          | -          | 0: Off, 1: On                       |                              |
| **B** | Engine             | Boolean          | -          | 0: Off, 1: On                       |                              |
| **C** | PassengerDoorsOpen | Boolean          | -          | 0: All closed, 1: At least one open | DoorEnabled counts as open   |
| **D** | Indicator          | Enum             | -          | 0: Off, 1: Left, 2: Right           |                              |
| **E** | FixingBrake        | Boolean          | -          | 0: Off, 1: On                       |                              |
| **F** | WarningLights      | Boolean          | -          | 0: Off, 1: On                       |                              |
| **G** | MainLights         | Boolean          | -          | 0: Off, 1: On                       |                              |
| **H** | FrontDoor          | Boolean          | -          | 0: Closed, 1: Open                  |                              |
| **I** | SecondDoor         | Boolean          | -          | 0: Closed, 1: Open                  |                              |
| **J** | ThirdDoor          | Boolean          | -          | 0: Closed, 1: Open                  |                              |
| **K** | StopRequest        | Boolean          | -          | 0: Off, 1: On                       |                              |
| **L** | StopBrake          | Boolean          | -          | 0: Off, 1: On                       |                              |
| **M** | HighBeam           | Boolean          | -          | 0: Off, 1: On                       |                              |
| **N** | BatteryLight       | Boolean          | -          | 0: Off, 1: On                       |                              |
| **O** | SimulatorType      | Enum             | -          | 0: OMSI 2, 1: TheBus                |                              |
| **P** | DoorEnable         | Boolean          | -          | 0: Off, 1: On                       | "Türfreigabe"                |
| **o** | Odometer           | Integer (64-bit) | Meters (m) | Total distance traveled             | Use `uint64_t` or equivalent |
| **r** | DateTime           | String           | -          | `YYYYMMDDHHMMSS`                    | 14-digit numeric string      |
| **s** | MaxSpeed           | Integer          | km/h       | Absolute value                      |                              |
| **t** | RPM                | Integer          | -          | Absolute value                      | Revolutions per minute       |
| **u** | Pressure           | Integer          | -          | Absolute value                      |                              |
| **v** | Temperature        | Integer          | -          | Absolute value                      |                              |
| **w** | Oil                | Integer          | -          | Absolute value                      |                              |
| **x** | Fuel               | Integer          | %          | Range: 0 ... 100                    | Tank content in percent      |
| **y** | Speed              | Integer          | km/h       | Absolute value                      | Current speed                |
| **z** | Water              | Integer          | -          | Absolute value                      |                              |

---

### Implementation Guide for Complex Types

#### DateTime (`r`)

The value is a fixed-width string of 14 digits. Do not parse as a single integer to avoid overflow and loss of leading
zeros. Extract by position:

- **Year:** Pos 0-3 | **Month:** Pos 4-5 | **Day:** Pos 6-7
- **Hour:** Pos 8-9 | **Minute:** Pos 10-11 | **Second:** Pos 12-13

#### Odometer (`o`)

Since the value is in meters, it can exceed 4,294,967,295 (32-bit limit).

- **Requirement:** Must be stored as an **unsigned 64-bit integer** (`uint64_t`, `u64`).

