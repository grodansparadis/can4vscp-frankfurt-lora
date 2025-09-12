# Getting Started

## Unboxing

When you receive your Frankfurt LoRa Gateway module, the package should contain:

* Frankfurt LoRa Gateway module
* Quick start guide
* Mounting hardware (if DIN-rail version)

## Initial Setup

### 1. Physical Installation

The Frankfurt module can be installed in different ways depending on your configuration:

**DIN-Rail Mounting**
* Mount the module on a standard 35mm DIN rail
* Ensure proper spacing for ventilation
* Connect the CAN4VSCP bus using RJ-45 cables

**Wall Mounting**
* Use the provided mounting holes
* Ensure the antenna has clear line-of-sight where possible
* Keep away from metal objects that may interfere with RF

### 2. Network Connection

Connect the module to your existing VSCP4CAN network:

1. Connect RJ-45 cable to the CAN bus
2. Ensure bus termination is properly configured
3. Power will be provided through the CAN4VSCP bus

### 3. Antenna Connection

**Important**: Never operate the module without an antenna connected, as this may damage the RF circuitry.

1. Connect the appropriate antenna for your frequency band
2. Ensure the antenna is suitable for outdoor/indoor use as needed
3. Verify the antenna connector matches (typically SMA)

### 4. Initial Configuration

The module comes with default settings that should work for most applications:

* **Frequency**: Default regional frequency (433/868/915 MHz)
* **Spreading Factor**: SF9 (balance of range vs data rate)
* **Transmit Power**: +14 dBm (moderate power)
* **VSCP Node ID**: Auto-assigned from GUID

### 5. Testing Communication

Use a VSCP tool like VSCP Works to verify the module is responding:

1. Send a "Read Register" command to register 0xD0 (GUID byte 0)
2. Verify you receive a response
3. Check that the module appears in your VSCP network scan

### 6. LoRa Network Setup

If you have multiple Frankfurt modules:

1. Ensure all modules use the same frequency and modulation settings
2. Configure unique node IDs to avoid conflicts
3. Set up appropriate decision matrix rules for event forwarding

## Next Steps

* [Learn about the module functionality](./function.md)
* [Configure the hardware settings](./hardware.md)  
* [Set up network connections](./connecting.md)
* [Program the decision matrix](./decisionmatrix.md)

## Troubleshooting

**Module not responding on CAN bus:**
* Check power supply voltage (9-28V DC)
* Verify CAN bus termination
* Ensure correct wiring

**Poor LoRa range:**
* Check antenna connection and type
* Verify line-of-sight conditions
* Adjust transmit power if needed
* Consider antenna positioning

**LoRa communication problems:**
* Ensure all modules use identical frequency settings
* Check spreading factor compatibility
* Verify bandwidth settings match