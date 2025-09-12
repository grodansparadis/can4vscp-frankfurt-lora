# KiCad Design Files

This directory will contain the KiCad project files for the Frankfurt LoRa Gateway PCB design.

## KiCad Project Structure

```
frankfurt-lora/
├── frankfurt-lora.pro        # KiCad project file
├── frankfurt-lora.sch        # Main schematic file
├── frankfurt-lora.kicad_pcb  # PCB layout file
├── libraries/                # Custom component libraries
├── 3d-models/               # 3D models for components
├── gerber/                  # Gerber files for manufacturing
└── assembly/                # Assembly drawings and files
```

## Design Files

**Schematic Design:**
- Multi-sheet schematic organized by function
- Power supply, MCU, CAN, LoRa RF sections
- Proper hierarchical design structure

**PCB Layout:**
- 4-layer PCB for mixed-signal design
- Proper RF layout techniques for LoRa
- Industrial connector placement
- EMC considerations

**Manufacturing Output:**
- Gerber files for PCB fabrication
- Excellon drill files
- Pick and place files for assembly
- Bill of materials (BOM)

## Version Control

KiCad files are stored in git with:
- Proper .gitignore for temporary files
- Release tags for production versions
- Design rule checks (DRC) clean files only

*KiCad design files will be created during hardware development phase.*