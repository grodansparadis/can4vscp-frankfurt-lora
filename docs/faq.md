# FAQ - Frequently Asked Questions

## General Questions

### Q: What is the Frankfurt LoRa Gateway?
**A:** The Frankfurt is a VSCP4CAN to LoRa bridge module that enables long-range wireless communication between VSCP networks. It allows you to extend VSCP networks beyond the physical limitations of CAN bus wiring.

### Q: How far can LoRa communication reach?
**A:** Range depends on many factors including:
- Line-of-sight: 5-15 km typical
- Urban environments: 1-3 km  
- Indoor: 100-500 meters
- Antenna height and type
- Transmit power settings
- Environmental conditions

### Q: Can multiple Frankfurt modules work together?
**A:** Yes, Frankfurt modules can be deployed in various topologies:
- Point-to-point links
- Star networks (hub and spoke)
- Mesh networks with multiple paths
- Mixed topologies

## Technical Questions

### Q: What frequencies does Frankfurt support?
**A:** Frankfurt supports three main ISM bands:
- 433 MHz (global ISM band)
- 868 MHz (European SRD band)
- 915 MHz (Americas ISM band)

The specific model determines which band is supported.

### Q: Is a license required to operate Frankfurt modules?
**A:** No license is required as Frankfurt operates in license-free ISM bands. However, you must comply with local power and duty cycle regulations.

### Q: Can Frankfurt work with existing VSCP4CAN networks?
**A:** Yes, Frankfurt is fully compatible with standard VSCP4CAN networks. It appears as a regular VSCP node and follows all VSCP protocols and conventions.

### Q: What power supply is required?
**A:** Frankfurt is powered through the CAN4VSCP bus:
- Input voltage: 9-28V DC
- Typical power: 1.8W
- Peak power: 3W (during transmission)

## Installation Questions

### Q: What type of antenna should I use?
**A:** Antenna selection depends on your application:
- **Omnidirectional whip**: Good for point-to-multipoint
- **High-gain directional**: Best for long-range point-to-point
- **PCB antenna**: Compact but limited range
- **External antenna**: Best performance, weather protection needed

### Q: How do I mount Frankfurt modules?
**A:** Frankfurt offers multiple mounting options:
- DIN-rail mounting (standard 35mm rail)
- Wall mounting (using provided holes)
- Panel mounting (with optional brackets)

### Q: Can Frankfurt be used outdoors?
**A:** The module itself is rated IP40 (indoor use), but it can be used outdoors with proper enclosure. The antenna should be outdoor-rated if exposed to weather.

### Q: What cables do I need?
**A:** For CAN connection, use:
- CAT5e or CAT6 twisted pair cable
- Standard RJ-45 connectors  
- Follow T-568B wiring standard

For antenna, use appropriate coaxial cable (RG-58, LMR-200, etc.) with SMA connectors.

## Configuration Questions

### Q: How do I configure Frankfurt modules?
**A:** Configuration can be done through:
- VSCP Works software via CAN bus
- VSCP register read/write commands
- Decision matrix programming
- Web interface (if available)

### Q: What is the Decision Matrix?
**A:** The Decision Matrix is a powerful feature that allows you to program rules for:
- Event filtering (which events to forward)
- Action triggers (what to do when events match)
- Network optimization (reducing unnecessary traffic)
- Custom behaviors without firmware changes

### Q: How do I prevent event loops?
**A:** Frankfurt includes loop prevention mechanisms:
- Automatic origin tracking
- Configurable forwarding rules
- Decision matrix filtering
- Built-in timeout mechanisms

### Q: Can I use different LoRa settings on different modules?
**A:** All modules in a LoRa network must use compatible settings:
- **Must match**: Frequency, spreading factor, bandwidth, coding rate
- **Can differ**: Transmit power, node addresses
- **Recommended**: Use identical settings for best compatibility

## Troubleshooting Questions

### Q: Frankfurt doesn't appear on my CAN network. What should I check?
**A:** Check these items in order:
1. Power supply voltage (9-28V DC)
2. CAN bus termination (120Ω at both ends)
3. Cable wiring and connections
4. Bus loading (total current draw)
5. Duplicate node IDs on network

### Q: LoRa communication isn't working. What should I check?
**A:** Common LoRa issues:
1. **Antenna connection** - Never operate without antenna
2. **Frequency settings** - Must match exactly between modules
3. **Spreading factor** - Must be compatible
4. **Range** - Start testing at close distance
5. **Interference** - Check for other radio sources
6. **Line of sight** - Obstacles significantly reduce range

### Q: How can I test LoRa range?
**A:** Use this systematic approach:
1. Configure two Frankfurt modules identically
2. Start with modules 10m apart
3. Send test events and verify reception
4. Gradually increase distance
5. Monitor RSSI and packet success rate
6. Note maximum reliable range

### Q: What do the LED indicators mean?
**A:** LED status meanings:

**Status LED (Green):**
- Solid: Powered and operational
- Slow flash: Normal operation
- Fast flash: Active communication
- Off: No power or failure

**CAN LED (Yellow):**
- Solid: CAN bus active
- Flash: CAN message activity
- Off: No CAN communication

**LoRa LED (Blue):**
- Flash: LoRa transmission
- Double flash: LoRa reception
- Off: No LoRa activity

## Performance Questions

### Q: How many events per second can Frankfurt handle?
**A:** Event handling capacity depends on:
- LoRa data rate (0.3-37.5 kbps)
- Spreading factor setting
- Event size and filtering
- Network congestion
- Typical: 10-100 events/second

### Q: How do I optimize LoRa performance?
**A:** Key optimization strategies:
- Use minimum spreading factor for required range
- Implement intelligent event filtering
- Adjust transmit power appropriately
- Use proper antenna system
- Monitor and manage network traffic

### Q: Can Frankfurt handle real-time applications?
**A:** Frankfurt is suitable for many real-time applications, but consider:
- LoRa has inherent latency (100ms-several seconds)
- Best for monitoring and control, not high-speed data
- Use appropriate spreading factor for latency requirements
- Implement proper error handling

## Regulatory Questions

### Q: What regulatory approvals does Frankfurt have?
**A:** Frankfurt is designed for compliance with:
- CE marking (Europe)
- FCC Part 15 (USA)
- IC RSS-210 (Canada)
- RCM (Australia)

Check specific model documentation for current certifications.

### Q: Are there duty cycle restrictions?
**A:** Some regions have duty cycle limits:
- **Europe**: 1% duty cycle in 868 MHz band
- **USA/Canada**: No duty cycle limits in 915 MHz
- **Global**: 433 MHz typically no restrictions

Frankfurt automatically manages duty cycles where required.

### Q: Can I change the transmit power?
**A:** Yes, transmit power is software configurable:
- Range: +2 to +20 dBm
- Must comply with local regulations
- Higher power = longer range but more interference
- Use minimum power needed for reliable communication

## Support Questions

### Q: Where can I get technical support?
**A:** Support is available through:
- GitHub repository issues
- VSCP community forums
- Direct support from Grodans Paradis AB
- Local distributors

### Q: How do I report bugs or request features?
**A:** Use the GitHub repository:
- Open issues for bugs
- Use discussions for questions
- Submit pull requests for contributions
- Follow the issue templates provided

### Q: Is the firmware open source?
**A:** Yes, Frankfurt is part of the open-source VSCP project:
- Source code available on GitHub
- MIT license for most components
- Community contributions welcome
- Documentation freely available

### Q: Can I modify the firmware?
**A:** Yes, the firmware can be modified:
- Source code available
- Standard development tools supported
- Debug interfaces available
- Bootloader supports field updates
- Consider contributing improvements back