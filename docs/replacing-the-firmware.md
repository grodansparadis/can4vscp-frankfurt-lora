# Updating the Firmware

*This section will provide instructions for firmware updates when the bootloader is implemented.*

The Frankfurt LoRa Gateway includes a bootloader that allows firmware updates without requiring special programming hardware.

## Update Methods

### Over CAN Bus
Firmware can be updated through the VSCP4CAN bus using standard VSCP bootloader protocols.

### Over LoRa
Remote firmware updates may be possible over the LoRa interface (if implemented).

### Programming Interface  
Direct programming using debug interface for development purposes.

## Update Procedure

1. Verify current firmware version
2. Download appropriate firmware file
3. Enter bootloader mode
4. Upload new firmware
5. Verify installation
6. Restart module

*Detailed update procedures will be provided when the bootloader is implemented.*