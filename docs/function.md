# Functionality

## Overview

The Frankfurt LoRa Gateway module serves as a bridge between VSCP4CAN networks and LoRa radio networks. It enables long-range, low-power wireless communication while maintaining full VSCP protocol compatibility.

## Key Features

### LoRa Radio Communication

The module incorporates a high-performance LoRa transceiver providing:

* **Long Range**: Up to several kilometers line-of-sight
* **Low Power**: Optimized for battery-operated remote nodes
* **Robust Modulation**: Excellent performance in noisy environments
* **Configurable Parameters**: Frequency, spreading factor, bandwidth, power

### VSCP Protocol Bridge

**Bidirectional Event Forwarding**
* Events from CAN bus are forwarded to LoRa network
* Events from LoRa network are forwarded to CAN bus
* Configurable filtering through decision matrix
* Event translation and routing

**Full VSCP Compliance**
* Standard VSCP register model
* Complete event class/type support
* GUID-based addressing
* Automatic node discovery

### Decision Matrix

The built-in decision matrix enables intelligent event handling:

* **Event Filtering**: Forward only relevant events
* **Conditional Logic**: Based on class, type, data content
* **Action Triggers**: Control local functions or generate new events
* **Network Optimization**: Reduce unnecessary radio traffic

## Operating Modes

### Bridge Mode (Default)

In bridge mode, the module automatically forwards events between networks:

* CAN events → LoRa transmission
* LoRa reception → CAN events
* Configurable bidirectional filtering
* Automatic collision avoidance

### Gateway Mode

Advanced mode with protocol translation and routing:

* Multi-network support
* Event aggregation and distribution
* Network topology management
* Advanced filtering and routing rules

## LoRa Network Topology

### Point-to-Point

Direct communication between two Frankfurt modules:
```
[CAN Network A] ←→ [Frankfurt A] ~~~ [Frankfurt B] ←→ [CAN Network B]
```

### Star Network

One central gateway with multiple remote nodes:
```
                    [Frankfurt Central]
                           |
        [Remote A] ~~~ [Gateway] ~~~ [Remote B]
                           |
                    [Remote C]
```

### Mesh Network

Distributed network with multiple gateways:
```
[Frankfurt A] ~~~ [Frankfurt B] ~~~ [Frankfurt C]
     |                                   |
[Frankfurt D] ~~~~~~~~~~~~~~~~~~~~~~~~ [Frankfurt E]
```

## Event Processing

### Incoming CAN Events

1. **Reception**: Event received from CAN4VSCP bus
2. **Decision Matrix**: Evaluate DM rules for this event
3. **Filter Check**: Determine if event should be forwarded
4. **LoRa Transmission**: Send over radio if criteria met
5. **Local Action**: Execute any local actions defined in DM

### Incoming LoRa Events

1. **Reception**: LoRa packet received and validated
2. **Decoding**: Extract VSCP event from LoRa payload
3. **Decision Matrix**: Evaluate DM rules for this event
4. **Origin Check**: Prevent loops (don't forward back to originator)
5. **CAN Transmission**: Send to CAN bus if criteria met

## RF Parameters

### Frequency Bands

The module supports different frequency bands depending on regional regulations:

* **433 MHz**: Global ISM band
* **868 MHz**: European ISM band  
* **915 MHz**: North American ISM band

### Modulation Parameters

**Spreading Factor (SF7-SF12)**
* Higher SF = longer range, lower data rate
* Lower SF = shorter range, higher data rate
* Default: SF9 (good balance)

**Bandwidth**
* 125 kHz, 250 kHz, 500 kHz options
* Narrower = better sensitivity, lower data rate
* Default: 125 kHz

**Coding Rate**
* 4/5, 4/6, 4/7, 4/8 options
* Higher rate = better error correction, lower data rate
* Default: 4/5

**Transmit Power**
* Adjustable from +2 dBm to +20 dBm
* Higher power = longer range, more power consumption
* Default: +14 dBm

## Network Management

### Address Management

* **GUID-based addressing**: Each module has unique 16-byte GUID
* **Node ID assignment**: Automatic or manual configuration
* **Collision detection**: Automatic handling of address conflicts

### Network Discovery

* **Heartbeat events**: Regular "I'm alive" messages
* **Node enumeration**: Automatic discovery of network topology
* **Service announcement**: Broadcast of available services

### Quality of Service

* **Priority levels**: Critical vs. normal event handling
* **Retry mechanisms**: Automatic retransmission of important events
* **Flow control**: Prevent network congestion
* **Error reporting**: Notification of communication failures

## Power Management

### Operating Modes

**Normal Mode**
* Full functionality active
* Continuous CAN and LoRa monitoring
* Typical power consumption: 100-200 mA

**Low Power Mode**
* Reduced polling intervals
* Sleep between activities
* Typical power consumption: 50-100 mA

**Sleep Mode**
* Minimal functionality
* Wake on specific events
* Typical power consumption: 5-10 mA

### Power Supply

* **Input voltage**: 9-28V DC via CAN4VSCP bus
* **Internal regulation**: Efficient switching power supply
* **Backup power**: Optional battery backup support