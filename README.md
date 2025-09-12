# can4vscp-frankfurt-lora

![](./docs/images/opensourcehw-100x82.png)

-----

<h1>Frankfurt LoRa Gateway module</h1>

This module is part of the VSCP project. It is free to use, modify and sell. The only thing we kindly ask is that improvements and extensions are contributed back to the project (at your will). This to make the project better for everyone. All design files is licensed under the MIT license.

The full documentation for the module can be found [here](http://grodansparadis.github.io/can4vscp-frankfurt-lora/#/).

![](docs/images/frankfurt-lora_800.png)

In the repository you find the development files for the Frankfurt LoRa Gateway module. The project implements a VSCP CAN4VSCP to LoRa bridge, enabling VSCP communication over long range radio frequencies.

## Abstract

Frankfurt is a LoRa gateway module that connects to a CAN4VSCP bus and can bridge VSCP events to/from LoRa radio networks. The module enables long-range communication between VSCP devices using LoRa radio technology, extending the reach of VSCP networks beyond traditional CAN bus limitations.

The module fully adopts to the CAN4VSCP specification and can be powered directly over the bus with a 9-28V DC power source. It has a rich register set for configuration and supports bidirectional VSCP event forwarding between CAN and LoRa networks. It also features a decision matrix for dynamic event handling and filtering.

VSCP CAN modules are designed to work on a VSCP4CAN bus which use ordinary RJ-45 connectors and is powered with 9-28V DC over the same cable. This means there is no need for a separate power cable. All that is needed is a CAT5 or better twisted pair cable. Bus length can be a maximum of 500 meters with drops of maximum 24 meters length (up to a total of 120 meters). As for all VSCP4CAN modules the communication speed is fixed at 125 kbps.

All VSCP modules contain information about their own setup, manual, hardware version, manufacturer etc. You just ask the module for the information you need and you will get it. When they are started up they have a default functionality that often is all that is needed to get a working setup. If the module has something to report it will send you an event and if it is setup to react on a certain type of event it will do its work when you send event(s) to it.

<hr>

## Project files

### User manual
  * [User Manual](https://grodansparadis.github.io/can4vscp-frankfurt-lora/#)

### Schematic, PCB, 3D files etc
  * [Schematics](./schematics/)
  * Hardware design files will be made available in [KiCad](https://kicad.org) format in the `kicad` directory.
  * Gerber files for PCB production will be found in the `gerber` directory (in the `kicad` folder).

### Firmware

The firmware will be developed using modern embedded development tools.

  * Binary release files will be available [here](https://github.com/grodansparadis/can4vscp-frankfurt-lora/releases)

### MDF - Module Description File(s)
  * MDF files will be available in the `mdf` directory

### Support
If you need support, please open an issue in the [GitHub repository](https://github.com/grodansparadis/can4vscp-frankfurt-lora/issues).

### Buy a ready made modules
You can buy a ready made module from [Grodans Paradis](http://www.grodansparadis.com).

### Project related links
  * [VSCP project](https://www.vscp.org)
  * [VSCP Documentation site](https://docs.vscp.org/)
  * [VSCP Wiki](https://github.com/grodansparadis/vscp/wiki)
  * [LoRa Technology Overview](https://www.semtech.com/lora)

## Key Features

- **LoRa Radio Interface**: Long-range, low-power radio communication
- **VSCP CAN Bridge**: Seamless integration with existing VSCP4CAN networks  
- **Bidirectional Communication**: Events flow both ways between CAN and LoRa
- **Configurable RF Parameters**: Frequency, spreading factor, bandwidth, and power settings
- **Event Filtering**: Decision matrix for selective event forwarding
- **Standard VSCP Compliance**: Full VSCP register model and event support
- **Bus Powered**: Operates from 9-28V DC via CAN4VSCP bus

## Technical Specifications

- **Radio Frequency**: 433/868/915 MHz (region dependent)
- **LoRa Modulation**: Configurable spreading factor (SF7-SF12)
- **RF Power**: Adjustable up to +20 dBm
- **Range**: Up to several kilometers (line of sight)
- **CAN Interface**: 125 kbps, standard VSCP4CAN physical layer
- **Power Supply**: 9-28V DC via RJ-45 connector
- **Dimensions**: Standard DIN-rail mountable form factor

## Development Status

This project is currently in initial development phase. Documentation structure and basic framework are being established.

## Steps you should go through to adopt this for your own VSCP LoRa project

  * Review the LoRa radio parameters for your region and application requirements
  * Configure the VSCP GUID (Global Unique ID) for each module instance
  * Set up the decision matrix rules for event filtering and forwarding
  * Adjust RF parameters (frequency, power, spreading factor) as needed
  * Configure the device URL pointing to your module's XML description
  * Set manufacturer ID and device-specific parameters

The device configuration can be managed through VSCP registers or stored in EEPROM for persistent settings.
