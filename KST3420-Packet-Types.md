# KST3120 Packets Types

## Uplink

One payload is sent with both Battery, Switch, and Error packets concatenated.

Check the documentation in the Javascript Parser for more detail.

Example: `007801FE00900101FFFF0100`

| Packet Type | Key      | Length | Value  | Decoded Value |
|-------------|----------|--------|--------|---------------|
| Battery     | `0x0078` | `0x01` | `0xFF` | 3.05V         |
| Switch      | `0x0090` | `0x01` | `0x01` | Pressed       |
| Error       | `0xFFFF` | `0x01` | `0x00` | No Error      |


## Downlink

A downlink payload can be sent to change the uplink interval time in minutes.
**FPort** 2 is used for sending a Downlink.
Valid range for Uplinks is `0x01` to `0x240`. Which equals to 1 minute to 240 minutes (4 hours)

Example: `0100011E` = Set Uplink Interval to 30mins

| Packet Type     | Key      | Length | Value  | Decoded Value |
|-----------------|----------|--------|--------|---------------|
| Uplink Interval | `0x0100` | `0x01` | `0x1E` | 30 Minutes    |


## Battery Lookup Table

| Voltage | Sensed Battery | Percent Remaining |
|---------|----------------|-------------------|
| 2.75v   | 202            | 5%                |
| 2.80v   | 212            | 20%               |
| 2.85v   | 222            | 70%               |
| 2.90v   | 232            | 85%               |
| 2.95v   | 244            | 90%               |
| 3.00v   | 254            | 100%              |
| 3.05v   | 255            | 100%              |

## Switch States

| Packet Type        | Key      | Length | Value  | Decoded Value   |
|--------------------|----------|--------|--------|-----------------|
| Switch Not Pressed | `0x0090` | `0x01` | `0x00` | 0 - Not Pressed |
| Switch Pressed     | `0x0090` | `0x01` | `0x01` | 1 - Pressed     |

## Error States

| Example      | Key      | Length | Value  | Notes                             |
|--------------|----------|--------|--------|-----------------------------------|
| `0xFFFF0100` | `0xFFFF` | `0x01` | `0x00` | No Error                          |
| `0xFFFF0104` | `0xFFFF` | `0x01` | `0x04` | Unknown Error; Cannot Read Switch |