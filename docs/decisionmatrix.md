# Decision Matrix

The Decision Matrix (DM) is a powerful feature that allows the Frankfurt LoRa Gateway to make intelligent decisions about event handling, filtering, and forwarding. It provides a flexible way to configure how events are processed without requiring firmware changes.

## Overview

The Decision Matrix consists of a table of rules, where each rule defines:
* **Conditions** to match against incoming events
* **Actions** to take when conditions are met
* **Parameters** to customize the action behavior

Each Frankfurt module can store up to 32 decision matrix entries, providing extensive flexibility for event handling.

## Decision Matrix Structure

Each DM entry consists of 8 bytes:

| Byte | Name | Description |
|------|------|-------------|
| 0 | oaddr | Originating address (sender node ID) |
| 1 | flags | Control flags and conditions |
| 2 | class_mask | VSCP class mask |  
| 3 | class_filter | VSCP class filter |
| 4 | type_mask | VSCP type mask |
| 5 | type_filter | VSCP type filter |
| 6 | action | Action code to execute |
| 7 | param | Action parameter |

## Flags Register (Byte 1)

| Bit | Name | Description |
|-----|------|-------------|
| 7 | ENABLE | 1 = Entry enabled, 0 = disabled |
| 6 | OADDR_ENABLE | 1 = Check originating address |
| 5 | HARDCODED | 1 = Entry cannot be changed |
| 4 | MATCH_ZONE | 1 = Check zone in event data |
| 3 | MATCH_SUBZONE | 1 = Check subzone in event data |
| 2 | RESERVED | Reserved for future use |
| 1 | RESERVED | Reserved for future use |
| 0 | RESERVED | Reserved for future use |

## Event Matching

### Class and Type Filtering

The class and type filters work together using bitwise operations:
```
if ((event_class & class_mask) == class_filter) {
    if ((event_type & type_mask) == type_filter) {
        // Rule matches
    }
}
```

**Examples:**

Match all CLASS1.MEASUREMENT events:
* class_mask = 0xFF, class_filter = 0x10
* type_mask = 0x00, type_filter = 0x00

Match specific temperature events:
* class_mask = 0xFF, class_filter = 0x10  
* type_mask = 0xFF, type_filter = 0x06

### Originating Address

When OADDR_ENABLE is set, the rule only matches events from the specified node:
* oaddr = 0x00: Match events from any node
* oaddr = 0x01-0xFE: Match events from specific node ID
* oaddr = 0xFF: Match events from this module only

### Zone and Subzone

When MATCH_ZONE/MATCH_SUBZONE are set, the rule checks the zone/subzone bytes in the event data against the module's configured zone/subzone values.

## Actions

### System Actions (0x00-0x0F)

| Code | Action | Description |
|------|--------|-------------|
| 0x00 | NOOP | No operation (disable entry) |
| 0x01 | FORWARD_CAN | Forward event to CAN bus |
| 0x02 | FORWARD_LORA | Forward event to LoRa |
| 0x03 | DROP | Drop event (don't forward) |
| 0x04 | STORE | Store event in local buffer |
| 0x05 | SEND_STATUS | Send module status event |

### LoRa Actions (0x10-0x1F)

| Code | Action | Description |
|------|--------|-------------|
| 0x10 | SET_POWER | Set LoRa transmit power |
| 0x11 | SET_FREQ | Set LoRa frequency |
| 0x12 | SET_SF | Set spreading factor |
| 0x13 | SET_BW | Set bandwidth |
| 0x14 | SCAN_FREQ | Scan for activity on frequency |
| 0x15 | MEASURE_RSSI | Measure current RSSI |

### Local Actions (0x20-0x2F)

| Code | Action | Description |
|------|--------|-------------|
| 0x20 | SET_LED | Control LED indicators |
| 0x21 | RESET_STATS | Reset communication statistics |
| 0x22 | SAVE_CONFIG | Save configuration to EEPROM |
| 0x23 | REBOOT | Restart module |
| 0x24 | FACTORY_RESET | Reset to factory defaults |

### User Actions (0x80-0xFF)

These action codes are reserved for custom application-specific actions.

## Configuration Examples

### Example 1: Basic Bridge Mode

Forward all events bidirectionally:

**DM Entry 0 - CAN to LoRa:**
```
oaddr: 0x00        // Any originating address
flags: 0x80        // Enabled only
class_mask: 0x00   // Match any class
class_filter: 0x00
type_mask: 0x00    // Match any type  
type_filter: 0x00
action: 0x02       // Forward to LoRa
param: 0x00
```

**DM Entry 1 - LoRa to CAN:**
```
oaddr: 0xFF        // From LoRa interface
flags: 0xC0        // Enabled + check address
class_mask: 0x00   // Match any class
class_filter: 0x00
type_mask: 0x00    // Match any type
type_filter: 0x00
action: 0x01       // Forward to CAN
param: 0x00
```

### Example 2: Temperature Monitoring

Forward only temperature events, adjust LoRa power based on value:

**DM Entry 0 - Temperature Events:**
```
oaddr: 0x00        // Any sensor
flags: 0x80        // Enabled
class_mask: 0xFF   // Exact class match
class_filter: 0x10 // CLASS1.MEASUREMENT
type_mask: 0xFF    // Exact type match
type_filter: 0x06  // Temperature
action: 0x02       // Forward to LoRa
param: 0x00
```

**DM Entry 1 - High Temperature:**
```
oaddr: 0x00        
flags: 0x80        // Enabled
class_mask: 0xFF   
class_filter: 0x10 // CLASS1.MEASUREMENT
type_mask: 0xFF    
type_filter: 0x06  // Temperature
action: 0x10       // Set LoRa power
param: 0x14        // +20 dBm for urgent alerts
```

### Example 3: Event Filtering by Zone

Forward events only from specific zones:

**DM Entry 0 - Zone 1 Events:**
```
oaddr: 0x00        
flags: 0x90        // Enabled + match zone
class_mask: 0x00   // Any class
class_filter: 0x00
type_mask: 0x00    // Any type
type_filter: 0x00
action: 0x02       // Forward to LoRa  
param: 0x01        // Zone 1
```

### Example 4: Selective Alarm Forwarding

Forward only alarm events, drop routine status:

**DM Entry 0 - Drop Heartbeats:**
```
oaddr: 0x00
flags: 0x80        // Enabled
class_mask: 0xFF
class_filter: 0x09 // CLASS1.PROTOCOL
type_mask: 0xFF
type_filter: 0x01  // Heartbeat
action: 0x03       // Drop event
param: 0x00
```

**DM Entry 1 - Forward Alarms:**
```
oaddr: 0x00
flags: 0x80        // Enabled  
class_mask: 0xFF
class_filter: 0x01 // CLASS1.ALARM
type_mask: 0x00    // Any alarm type
type_filter: 0x00
action: 0x02       // Forward to LoRa
param: 0x14        // High power for alarms
```

## Programming the Decision Matrix

### Via VSCP Registers

The DM entries are stored in registers starting at 0x120:

```
DM Entry 0: Registers 0x120-0x127
DM Entry 1: Registers 0x128-0x12F
...
DM Entry 31: Registers 0x220-0x227
```

### Via Configuration Events

Send CLASS1.PROTOCOL events to modify DM entries:

**Write DM Entry:**
* Class: 0x00 (CLASS1.PROTOCOL)
* Type: 0x30 (Write matrix entry)  
* Data: [entry_index, 8_bytes_of_entry]

**Read DM Entry:**
* Class: 0x00 (CLASS1.PROTOCOL)
* Type: 0x31 (Read matrix entry)
* Data: [entry_index]

### Via Configuration Software

Use VSCP Works or other configuration tools:
1. Connect to CAN bus
2. Discover Frankfurt module
3. Open Decision Matrix configuration
4. Edit entries using GUI
5. Write configuration to module

## Best Practices

### Performance Optimization

1. **Order matters**: Place most frequently matched rules first
2. **Use specific filters**: Avoid overly broad matches
3. **Limit forwarding**: Only forward necessary events
4. **Group related rules**: Keep similar rules together

### Network Design

1. **Avoid loops**: Prevent events from bouncing between networks
2. **Use priority**: Critical events should have dedicated rules
3. **Monitor utilization**: Watch for excessive radio traffic
4. **Plan for growth**: Leave room for future rules

### Troubleshooting

1. **Test incrementally**: Add rules one at a time
2. **Use debug actions**: Send status events for debugging
3. **Monitor statistics**: Check forwarding counters
4. **Document rules**: Keep records of DM configuration

## Advanced Features

### Conditional Logic

Combine multiple conditions for complex logic:
```
IF (class == MEASUREMENT AND type == TEMPERATURE AND zone == 1)
   THEN forward with high power
ELSE IF (class == ALARM)  
   THEN forward immediately
ELSE
   DROP
```

### Dynamic Reconfiguration

Rules can be modified at runtime:
* Via VSCP register writes
* Through configuration events
* Using remote management tools

### Event Transformation

Some actions can modify events before forwarding:
* Change priority levels
* Add/remove data bytes  
* Modify zone/subzone information
* Insert timestamps

This powerful decision matrix system enables sophisticated event handling and network optimization without requiring custom firmware development.