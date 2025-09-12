# Hardware

## Overview

The Frankfurt LoRa Gateway is designed as a compact, professional IoT module suitable for industrial and commercial applications. It features robust construction, wide temperature range operation, and compliance with relevant EMC standards.

## Block Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                    Frankfurt LoRa Gateway                       │
│                                                                 │
│  ┌──────────┐    ┌─────────────┐    ┌──────────────────────────┐ │
│  │  CAN     │    │             │    │     LoRa Transceiver     │ │
│  │Interface │────│ Microcon-   │────│      (SX1276/78)        │ │
│  │          │    │ troller     │    │                          │ │
│  └──────────┘    │             │    └──────────┬───────────────┘ │
│       │          │             │               │                 │
│  ┌──────────┐    │             │    ┌─────────────────────────┐   │
│  │   Power  │────│             │    │    RF Frontend         │   │
│  │ Supply   │    │             │    │   & Antenna Interface  │   │
│  │          │    │             │    │                        │   │
│  └──────────┘    └─────────────┘    └─────────────────────────┘   │
│       │                                         │                 │
│  ┌──────────┐                                   │                 │
│  │   LED    │                              ┌─────────┐            │
│  │Indicators│                              │ Antenna │            │
│  │          │                              │Connector│            │
│  └──────────┘                              └─────────┘            │
└─────────────────────────────────────────────────────────────────┘
```

## Physical Specifications

### Dimensions
* **Length**: 100 mm
* **Width**: 70 mm  
* **Height**: 25 mm (plus antenna connector)
* **Weight**: Approximately 85g

### Enclosure
* **Material**: ABS plastic with flame retardant properties
* **Color**: Light gray with blue accent
* **Mounting**: DIN-rail clip or wall-mount holes
* **Protection**: IP40 rating (indoor use)
* **Operating Temperature**: -25°C to +70°C
* **Storage Temperature**: -40°C to +85°C
* **Humidity**: 5% to 95% non-condensing

## Electrical Specifications

### Power Supply
* **Input Voltage**: 9-28V DC (via CAN4VSCP bus)
* **Power Consumption**:
  - Typical: 150 mA @ 12V (1.8W)
  - Peak (transmitting): 250 mA @ 12V (3W)
  - Sleep mode: 10 mA @ 12V (0.12W)
* **Reverse Polarity Protection**: Yes
* **Overvoltage Protection**: Yes (up to 35V)

### CAN Interface
* **Physical Layer**: ISO 11898-2 compliant
* **Bit Rate**: 125 kbps (fixed)
* **Connector**: RJ-45 (VSCP4CAN standard)
* **Isolation**: 2.5kV galvanic isolation
* **Termination**: Software configurable 120Ω

### LoRa Radio Specifications
* **Frequency Bands**:
  - 433 MHz: 433.05 - 434.79 MHz
  - 868 MHz: 863 - 870 MHz
  - 915 MHz: 902 - 928 MHz
* **Modulation**: LoRa, GFSK, OOK
* **Sensitivity**: Down to -148 dBm
* **Output Power**: +2 to +20 dBm (software configurable)
* **Frequency Stability**: ±10 ppm
* **Antenna Impedance**: 50Ω

### RF Performance
* **Range** (typical conditions):
  - Line of sight: 5-15 km
  - Urban environment: 1-3 km
  - Indoor: 100-500 m
* **Data Rate**: 0.3 - 37.5 kbps (depending on settings)
* **Link Budget**: Up to 157 dB

## Microcontroller

### Main Processor
* **Type**: 32-bit ARM Cortex-M microcontroller
* **Flash Memory**: 256 KB
* **RAM**: 64 KB
* **EEPROM**: 4 KB (configuration storage)
* **Clock**: 48 MHz internal oscillator
* **Watchdog**: Hardware watchdog timer

### Interfaces
* **CAN Controller**: Built-in CAN peripheral
* **SPI**: For LoRa transceiver communication
* **UART**: Debug interface (internal use)
* **GPIO**: LED indicators and control signals

## Connectors and Interfaces

### CAN4VSCP Bus Connector (RJ-45)

Pin configuration according to VSCP4CAN standard:

| Pin | Function | Wire Color |
|-----|----------|------------|
| 1   | CANH     | White/Orange |
| 2   | CANL     | Orange |
| 3   | +12V     | White/Green |
| 4   | GND      | Blue |
| 5   | GND      | White/Blue |
| 6   | +12V     | Green |
| 7   | Not used | White/Brown |
| 8   | Not used | Brown |

### Antenna Connector
* **Type**: SMA female connector
* **Impedance**: 50Ω
* **VSWR**: < 1.5:1 across operating band

### Debug Interface
* **Type**: Tag-Connect TC2030 (internal use only)
* **Signals**: SWDIO, SWCLK, VCC, GND, RST, SWO

## LED Indicators

### Status LED (Green)
* **Solid**: Module powered and operational
* **Slow Flash**: Normal operation, no activity
* **Fast Flash**: Active CAN/LoRa communication
* **Off**: No power or module failure

### CAN LED (Yellow)
* **Solid**: CAN bus active
* **Flash**: CAN message activity
* **Off**: No CAN communication

### LoRa LED (Blue)
* **Flash**: LoRa transmission
* **Double Flash**: LoRa reception
* **Off**: No LoRa activity

## Antenna Requirements

### Antenna Types
* **Whip Antenna**: Omnidirectional, moderate gain
* **PCB Antenna**: Compact, integrated solutions
* **External Antenna**: High-gain, directional options

### Specifications
* **Frequency**: Must match operating band
* **Impedance**: 50Ω
* **VSWR**: < 2:1 preferred, < 3:1 acceptable
* **Connector**: SMA male
* **Polarization**: Vertical recommended

### Installation Guidelines
* **Height**: Higher is generally better
* **Clearance**: Keep away from metal objects
* **Cable**: Use low-loss coaxial cable (RG-58 or better)
* **Length**: Minimize cable length to reduce losses
* **Grounding**: Proper RF ground plane recommended

## Environmental Considerations

### EMC Compliance
* **Emission**: EN 61000-6-3 (Generic emission standard)
* **Immunity**: EN 61000-6-2 (Generic immunity standard)
* **Radio**: EN 300 220 (SRD radio equipment)

### Safety Standards
* **Low Voltage**: EN 60950-1
* **RoHS**: Compliant (lead-free construction)

### Installation Environment
* **Indoor Use**: IP40 protection suitable for most indoor environments
* **Ventilation**: Ensure adequate airflow around module
* **Vibration**: Suitable for typical building installation
* **Altitude**: Up to 2000m above sea level

## Regulatory Information

### Frequency Allocations

**433 MHz Band (Global)**
* ISM band allocation
* No license required in most countries
* Check local power limitations

**868 MHz Band (Europe)**
* SRD (Short Range Device) allocation
* ETSI EN 300 220 compliance
* Duty cycle limitations may apply

**915 MHz Band (Americas)**
* ISM band allocation
* FCC Part 15 compliance (US)
* IC RSS-210 compliance (Canada)

### Certifications

Planned certifications:
* **CE**: European Conformity (EU)
* **FCC**: Federal Communications Commission (US)
* **IC**: Industry Canada (Canada)
* **RCM**: Regulatory Compliance Mark (Australia)