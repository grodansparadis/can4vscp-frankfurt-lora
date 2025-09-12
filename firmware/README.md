# Firmware

This directory will contain the firmware source code and binary releases for the Frankfurt LoRa Gateway.

## Development Environment

The firmware will be developed using modern embedded development tools:

- **IDE**: Platform-independent development environment
- **Compiler**: ARM GCC toolchain
- **RTOS**: FreeRTOS or bare-metal implementation
- **Libraries**: VSCP protocol stack, LoRa driver libraries

## Source Code Organization

```
src/
├── main.c              # Main application entry point
├── vscp/               # VSCP protocol implementation
├── lora/               # LoRa radio driver
├── can/                # CAN interface driver  
├── config/             # Configuration management
├── dm/                 # Decision matrix implementation
├── bootloader/         # Bootloader source (if included)
└── hal/                # Hardware abstraction layer
```

## Binary Releases

Binary releases will be provided in multiple formats:
- `.hex` files for programming tools
- `.bin` files for bootloader updates
- `.elf` files with debug information

## Build Instructions

Detailed build instructions will be provided including:
- Toolchain setup and requirements
- Build system configuration  
- Debugging and testing procedures
- Release packaging process

*Firmware development will begin after hardware design is complete.*