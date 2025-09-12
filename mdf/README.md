# Module Description Files (MDF)

This directory contains VSCP Module Description Files for the Frankfurt LoRa Gateway.

## What is an MDF?

An MDF (Module Description File) is an XML file that describes a VSCP module's capabilities, registers, events, and configuration options. It enables VSCP tools to automatically discover and configure modules.

## Frankfurt MDF Files

The Frankfurt module MDF will include:

- Module identification and version information
- Register definitions for configuration
- Event definitions for communication
- Decision matrix structure
- Remote variable definitions
- User interface descriptions for configuration tools

## File Naming Convention

- `frankfurt_v{major}.{minor}.{patch}.xml` - Production releases
- `frankfurt_dev.xml` - Development versions

*MDF files will be created during firmware development and updated with each release.*