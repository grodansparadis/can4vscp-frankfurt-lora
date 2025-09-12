# Registers

*This section will contain detailed register documentation when hardware design is complete.*

## Standard VSCP Registers

The Frankfurt LoRa Gateway implements the standard VSCP register model with extensions for LoRa-specific functionality.

### Page 0 - Standard Registers (0x00-0xFF)

Standard VSCP registers as defined in the VSCP specification:

| Address | Register | R/W | Description |
|---------|----------|-----|-------------|
| 0x00-0x0F | GUID | R | Global Unique Identifier |
| 0x80 | Node ID | R/W | CAN node identifier |
| 0x81 | Status | R | Module status flags |
| 0x82 | Control | R/W | Module control flags |
| ... | ... | ... | ... |

### Page 1 - LoRa Configuration (0x100-0x1FF)

LoRa-specific configuration registers:

| Address | Register | R/W | Default | Description |
|---------|----------|-----|---------|-------------|
| 0x100-0x103 | RF_FREQUENCY | R/W | Band dependent | Operating frequency in Hz |
| 0x104 | SPREADING_FACTOR | R/W | 9 | LoRa spreading factor (7-12) |
| 0x105 | BANDWIDTH | R/W | 0 | Bandwidth setting (0=125kHz) |
| 0x106 | CODING_RATE | R/W | 1 | Coding rate (1=4/5) |
| 0x107 | TX_POWER | R/W | 14 | Transmit power in dBm |
| ... | ... | ... | ... | ... |

### Page 2 - Decision Matrix (0x200-0x2FF)

Decision matrix entries for event filtering and forwarding.

*Complete register documentation will be added as the project develops.*