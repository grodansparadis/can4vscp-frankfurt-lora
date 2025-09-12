# Events

*This section will document VSCP events supported by the Frankfurt module.*

The Frankfurt LoRa Gateway supports standard VSCP events and generates module-specific events for status and diagnostics.

## Supported Event Classes

### CLASS1.PROTOCOL (0x00)
Standard VSCP protocol events for node management and configuration.

### CLASS1.ALARM (0x01)  
Alarm events for error conditions and system status.

### CLASS1.SECURITY (0x02)
Security-related events (if implemented).

### CLASS1.MEASUREMENT (0x10)
Measurement events including RF signal quality metrics.

### CLASS1.DATA (0x15)
Data transport events for bridged information.

### CLASS1.INFORMATION (0x14)
Informational events for system status and diagnostics.

### CLASS1.CONTROL (0x1E)
Control events for module configuration and operation.

*Detailed event specifications will be provided during development.*