# Setup and Connecting

## Network Planning

Before connecting your Frankfurt LoRa Gateway, proper network planning is essential for optimal performance.

### CAN4VSCP Network Integration

The Frankfurt module integrates seamlessly into existing VSCP4CAN networks:

**Bus Topology**
```
[Power Supply] ── [Module A] ── [Frankfurt] ── [Module B] ── [Terminator]
                      │                            │
                 [Drop Cable]                [Drop Cable]
                      │                            │
                  [Module C]                   [Module D]
```

**Key Requirements:**
* Maximum bus length: 500 meters
* Maximum drop length: 24 meters (total of all drops ≤ 120m)
* Bus speed: 125 kbps (fixed)
* Termination: 120Ω at both ends

### LoRa Network Topology

Choose the appropriate topology based on your application needs:

#### Point-to-Point Link
Best for connecting two distant locations:
```
Location A: [CAN Network] ←→ [Frankfurt A] ~~~ [Frankfurt B] ←→ [CAN Network]
                                         RF Link (up to 15km)
```

#### Star Network
Central gateway with multiple remote nodes:
```
                     Central Location
                    [Frankfurt Gateway]
                           │
                    [CAN Network Main]
                           
    Remote A    Remote B                  Remote C
[Frankfurt] ~~~ [Gateway] ~~~~~~~~~~~~~~~ [Frankfurt]
     │                                        │
[Local CAN]                              [Local CAN]
```

#### Mesh Network
Distributed network with redundant paths:
```
[Frankfurt A] ~~~~~~~~~ [Frankfurt B]
     │    \               /    │
     │     \             /     │
     │      [Frankfurt D]      │
     │             │           │
[Frankfurt C] ~~~~~~~~~~~~~~~~~ [Frankfurt E]
```

## Installation Steps

### 1. Physical Installation

**DIN-Rail Mounting:**
1. Snap the module onto standard 35mm DIN rail
2. Ensure secure mounting - module should not slide
3. Allow minimum 10mm spacing on each side for ventilation

**Wall Mounting:**
1. Mark mounting holes using module as template
2. Use appropriate screws for wall material
3. Ensure module is level and secure

**Panel Mounting:**
1. Cut rectangular opening in panel
2. Secure with provided mounting brackets
3. Ensure gasket seals properly (if outdoor rated)

### 2. Antenna Installation

**Critical**: Never power the module without antenna connected!

**Antenna Selection:**
* Choose antenna appropriate for your frequency band
* Consider gain vs coverage pattern trade-offs
* Ensure antenna is rated for outdoor use if needed

**Installation Guidelines:**
* Mount antenna as high as practically possible
* Maintain clear line-of-sight where possible
* Keep antenna away from metal objects (minimum 1λ/4 distance)
* Use quality coaxial cable with proper impedance (50Ω)
* Minimize cable length to reduce losses

**Cable Losses (per 10m @ 868 MHz):**
* RG-58: ~2.5 dB loss
* RG-213: ~1.5 dB loss  
* LMR-200: ~1.8 dB loss
* LMR-400: ~0.7 dB loss

### 3. CAN Bus Connection

**Cable Preparation:**
1. Use CAT5e or better twisted pair cable
2. Follow T-568B wiring standard
3. Use quality RJ-45 connectors
4. Test cable continuity before connection

**Connection Process:**
1. Power down the CAN network
2. Connect Frankfurt module to bus using RJ-45 cable
3. Verify termination resistors are properly placed
4. Apply power and verify LED indicators

**Bus Testing:**
```bash
# Example using VSCP Works or similar tool
- Scan for nodes on bus
- Verify Frankfurt module responds to ping
- Check GUID and node ID assignment
- Test basic register read/write operations
```

### 4. Power Supply Considerations

**Voltage Requirements:**
* Input: 9-28V DC via CAN bus
* Typical power consumption: 1.8W
* Peak power (during transmit): 3.0W

**Power Budget Calculation:**
```
Total Bus Power = Supply Capacity - Cable Losses
Frankfurt Power = 3W (peak) + 1.8W (average)
Remaining Power = Total - Frankfurt - Other Modules
```

**Example:**
* 24V, 5A supply = 120W total
* 100m cable @ 0.5W loss = 50W available
* Frankfurt peak = 3W
* Remaining for other modules = 47W

### 5. Network Configuration

**Initial Setup:**
1. Connect configuration computer to CAN bus
2. Use VSCP configuration tool
3. Set basic parameters:
   - Node ID (if not using GUID-based)
   - Decision Matrix rules
   - LoRa RF parameters

**Basic Configuration Registers:**
```
Register 0x00-0x0F: GUID (read-only)
Register 0x80: Node ID
Register 0x81: LoRa Frequency (MSB)
Register 0x82: LoRa Frequency (LSB)  
Register 0x83: Spreading Factor
Register 0x84: Transmit Power
Register 0x85: Bandwidth
Register 0x86: Coding Rate
```

## Network Testing

### 1. Basic Connectivity

**CAN Bus Test:**
```
1. Send CLASS1.PROTOCOL, Type=1 (Probe) to Frankfurt
2. Expect response within 1 second
3. Verify GUID matches module label
4. Test register read/write operations
```

**LoRa Test:**
```
1. Configure second Frankfurt with identical RF settings
2. Place modules 10-50m apart initially
3. Send test events from one CAN network
4. Verify events appear on second CAN network
5. Check RSSI and SNR values in registers
```

### 2. Range Testing

**Systematic Range Test:**
1. Start with modules close together
2. Gradually increase distance
3. Monitor packet success rate
4. Note maximum reliable range
5. Test in different environments (indoor/outdoor)

**Performance Metrics:**
* Packet Error Rate (PER)
* Received Signal Strength (RSSI)
* Signal-to-Noise Ratio (SNR)
* Round-trip time

### 3. Interference Testing

**Potential Interference Sources:**
* WiFi networks (2.4 GHz can affect 868/915 MHz)
* Other LoRa devices
* Industrial equipment
* Weather radar (in some bands)

**Testing Method:**
1. Establish baseline performance
2. Identify potential interference sources
3. Test with interferers active
4. Adjust frequency/power if needed

## Troubleshooting

### Common Connection Issues

**Module Not Responding on CAN:**
* Check power supply voltage (9-28V)
* Verify CAN bus termination
* Test cable continuity
* Check for duplicate node IDs
* Verify bus loading (< 30 mA per node)

**Poor LoRa Performance:**
* Verify antenna connection and SWR
* Check frequency settings match between modules
* Ensure spreading factor compatibility
* Test with reduced distance
* Check for RF interference

**LED Diagnostic Codes:**

| Status LED | CAN LED | LoRa LED | Meaning |
|------------|---------|----------|---------|
| Off | Off | Off | No power |
| Solid | Off | Off | Power OK, no communication |
| Flash | Solid | Off | CAN active, no LoRa |
| Flash | Flash | Flash | Normal operation |
| Fast Flash | Off | Off | Error condition |

### Advanced Diagnostics

**Register Diagnostics:**
```
0xF0: Error flags register
0xF1: CAN status register
0xF2: LoRa status register
0xF3: RF signal strength (RSSI)
0xF4: Signal-to-noise ratio (SNR)
0xF5: Packet error count
```

**Event Diagnostics:**
The module can generate diagnostic events:
* CLASS1.ERROR events for error conditions
* CLASS1.INFORMATION events for status updates
* CLASS1.MEASUREMENT events for signal quality metrics

## Network Optimization

### RF Parameter Tuning

**Spreading Factor:**
* Higher SF = better sensitivity, longer range
* Lower SF = higher data rate, shorter range
* Recommended: Start with SF9, adjust based on needs

**Transmit Power:**
* Higher power = longer range, more interference
* Lower power = shorter range, longer battery life
* Recommended: Use minimum power for required range

**Frequency Selection:**
* Avoid frequencies used by other systems
* Consider regional regulations
* Use frequency diversity for multiple channels

### Decision Matrix Optimization

**Event Filtering:**
* Only forward events that need to cross networks
* Use class/type filtering to reduce traffic
* Implement priority-based forwarding

**Network Segmentation:**
* Group related devices on same network segment
* Use Frankfurt modules to bridge segments
* Minimize cross-network traffic

### Performance Monitoring

**Key Metrics to Monitor:**
* Packet success rate
* Average RSSI/SNR
* Network utilization
* Error rates
* Power consumption

**Monitoring Tools:**
* VSCP Works for real-time monitoring
* Custom monitoring applications
* Built-in diagnostic events
* Register polling for statistics