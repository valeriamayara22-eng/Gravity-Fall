# Gravity Fall: Gravitational Energy Storage System

**An open-source mechanical battery that converts gravitational potential energy into usable electricity.**

![Status](https://img.shields.io/badge/Status-Working%20Prototype-brightgreen)
![Efficiency](https://img.shields.io/badge/Efficiency-58%25-blue)
![Power](https://img.shields.io/badge/Peak%20Power-13W-orange)
![License](https://img.shields.io/badge/License-MIT-yellow)

---

## Overview

Gravity Fall is a gravitational energy storage system designed and built by high school students in Mexico City. It demonstrates that gravitational potential energy can be reliably converted into usable electrical power — no solar panels, no wind turbines, no lithium batteries required.

The system works like a **mechanical battery**: a 15.65 kg mass is lifted to a height of 1.80 m. As it descends through a chain-driven transmission system, it spins a hub motor that generates electricity. A magnetic braking system controls the descent speed, while an MPPT charge controller regulates the output for stable energy storage.

**Key results:**
- Peak electrical output: **13W** at 1.02 N·m torque
- System efficiency: **58%** (gravitational PE → electrical energy)
- Angular velocity stabilization at **15.65 kg**, confirming successful magnetic brake control
- Stable descent time of **9.5 seconds** per cycle, validated by MPPT algorithm

> **⚠️ Important note:** This is a proof-of-concept prototype for energy storage research, not a practical energy generation device. Each 9.5-second descent cycle produces approximately 123.5 J of usable electrical energy. To fully charge an iPhone 16 (12.54 Wh battery), the mass would need to be lifted and released **394 times**. The value of this project lies in validating the physics, the control system, and the efficiency of gravitational-to-electrical conversion at small scale — not in replacing existing charging methods. The engineering challenge ahead is scaling: heavier masses, taller structures, and automated return systems could make this approach practical for real-world energy storage.

---

## The Problem

Over 770 million people worldwide lack access to reliable electricity. Existing renewable solutions (solar, wind) depend on weather conditions and often require expensive lithium-ion batteries for storage — batteries that degrade over time, require rare minerals to produce, and generate toxic waste.

Gravity Fall proposes an alternative: **store energy as height**. Unlike chemical batteries, a mass doesn't degrade. It can be lifted and dropped thousands of times with zero loss of storage capacity. The system requires no fuel, no rare materials, and no grid connection.

---

## System Architecture

```
┌─────────────┐
│  Mass (15.65 kg)  │
│  Height: 1.80 m   │
│  Ug = mgh         │
└───────┬─────┘
        │ Descent (gravity)
        ▼
┌─────────────┐
│  Chain Drive      │
│  Ratio: 1:9       │
│  chains  │
└───────┬─────┘
        │ Mechanical torque
        ▼
┌─────────────┐
│  Hub Motor        │
│  Multi-pole       │
│  Magnetic brake   │
└───────┬─────┘
        │ AC output
        ▼
┌─────────────┐
│  MPPT Controller  │
│  Charge regulation│
└───────┬─────┘
        │ Regulated DC
        ▼
┌─────────────┐
│  LiFePO4 Battery  │
│  12V storage      │
└───────┬─────┘
        │ DC-DC conversion
        ▼
┌─────────────┐
│  USB-C Output     │
│  5V / Device      │
│  charging         │
└─────────────┘
```

---

## Experimental Results

### Test Configuration
- **Structure height:** 1.80 m (1.39 m effective drop, 0.41 m dead space)
- **Transmission:** Bicycle chains, 1:9 gear ratio
- **Generator:** Multi-pole hub motor with magnetic braking
- **Energy management:** MPPT charge controller + DC-DC buck converter
- **Measurement instruments:** Multimeter, tachometer, torque sensor

### Performance Data

| Mass (kg) | Torque (N·m) | Power (W) | Efficiency (%) | Angular Vel. (rad/s) | Fall Time (s) |
|-----------|-------------|-----------|----------------|---------------------|---------------|
| 10.05     | 0.65        | 5.1       | 40             | 7.85                | 9.50          |
| 12.85     | 0.83        | 8.7       | 49             | 10.48               | 9.50          |
| 15.65     | 1.02        | 13.0      | 58             | 12.75               | 9.50          |

### Key Findings

1. **Non-linear power scaling:** While mass increased by 56%, electrical power output jumped by **155%** (5.1W → 13W). This occurs because at lower loads, friction dominates; at higher loads, the motor operates in its optimal efficiency range.

2. **Efficiency scales with load:** Global efficiency improved from 40% to 58% with a slope of 3.18 per kg. Each additional kilogram of mass proportionally reduces frictional losses.

3. **Angular velocity stabilization:** At 15.65 kg, angular velocity varied by only 0.01 rad/s despite increasing mass — definitive proof that the magnetic braking system successfully controls descent speed while allowing power output to continue increasing.

4. **Constant fall time:** The 9.5-second descent remained stable across all mass configurations, validating the MPPT algorithm's ability to regulate energy extraction.

---

## Design Files

```
/cad/                              → FreeCAD parametric models (.FCStd)
  ├── (frame_structure.FCStd)       → Main wooden frame
  ├── (large_mounting_disc.FCStd)    → Large disc for sprocket mounting
  ├── (small_mounting_disc.FCStd)    → Small disc for motor coupling
  └── (metal_bracket.FCStd)          → Metal bracket for hub motor support

/images/                           → Prototype photos
  ├── (01_full_prototype_front.jpeg) → Complete structure, front view
  ├── (02_prototype_with_mass.jpeg)  → Structure with mass and descent mechanism
  ├── (03_chain_drive_closeup.jpeg)  → Chain drive and sprocket detail (top-down)
  ├── (04_side_view_transmission.jpeg) → Side view showing full transmission
  ├── (05_testing_with_energy_monitor.jpeg) → Testing session with energy monitor and LiFePO4 battery
  ├── (06_electronics_mppt_dcdc.jpeg) → MPPT controller and DC-DC converter wiring
  └── (07_cnc_machined_discs.jpeg)   → Custom CNC-machined mounting discs

/data/                             → Experimental data
  └── (experimental_results.xlsx)   → All test measurements across three mass configurations

/docs/                             → Documentation
  └── (BUILD_GUIDE.md)              → Step-by-step construction guide with BOM
```

---

## Bill of Materials

### Prototype Cost (as built)

| Component | Source | Cost (MXN) |
|-----------|--------|-----------|
| Custom wooden frame | Professional carpentry (commissioned) | $4,000 |
| Custom machined discs and supports | CNC machining from FreeCAD files | $3,500 |
| Hub motor (36V, multi-pole) | Online marketplace | $2,500 |
| Steel axles and bearings | Industrial supplier | $1,500 |
| MPPT charge controller | Electronics supplier | $1,200 |
| LiFePO4 battery (12V) | Electronics supplier | $2,000 |
| DC-DC buck converter (12V→5V) | Electronics supplier | $300 |
| Recycled bicycle chains | Local bike shop / scrap | $200 |
| Neodymium magnets (braking system) | Online marketplace | $500 |
| Sprockets and mounting hardware | Hardware store | $800 |
| Wiring, connectors, misc | Electronics supplier | $500 |
| **Total (as built)** | | **$15,000–$20,000 MXN (~$860–$1,150 USD)** |

### Estimated DIY Replication Cost

| Component | DIY Alternative | Est. Cost (MXN) |
|-----------|----------------|-----------------|
| Frame | Self-built with lumber from hardware store | $800 |
| Custom parts | 3D printed from provided FreeCAD files | $500 |
| Hub motor | Same (no cheaper alternative) | $2,500 |
| Axles and bearings | Hardware store sourcing | $600 |
| MPPT controller | Budget unit from online marketplace | $600 |
| LiFePO4 battery | Budget unit from online marketplace | $1,200 |
| DC-DC converter, chains, magnets, wiring | Same sources | $800 |
| **Total (DIY estimate)** | | **~$7,000 MXN (~$400 USD)** |

*Our prototype used professionally fabricated components for precision and durability. The FreeCAD design files are provided so builders can choose between professional fabrication, 3D printing, or manual construction based on their available tools and budget.*

---

## Areas for Improvement

- **Dead space reduction:** 41 cm of the 1.80 m structure is non-functional. Compacting the design would increase effective gravitational potential by ~30%.
- **Chain-to-belt conversion:** Replacing chains with timing belts would reduce the current 10% frictional loss.
- **Automated mass return:** Implementing a motorized or manual winch system for re-lifting the mass would enable continuous operation.
- **Multi-mass parallel system:** Running multiple masses in sequence could provide near-continuous power output.

---

## Relevance

This project directly addresses **UN Sustainable Development Goal 7: Affordable and Clean Energy**. The system is:

- **Climate-independent** — works day or night, rain or shine
- **Zero-emission** — no combustion, no chemical processes
- **Non-degrading** — unlike lithium batteries, the mass never loses capacity
- **Low-cost and replicable** — DIY replication estimated at ~$400 USD using accessible materials and provided design files
- **Educational** — demonstrates core physics principles (energy conservation, electromagnetic induction, mechanical advantage) through a functional device

---

## Background

Gravity Fall was developed as a research project for the XIV Student Research Congress of the UNAM Incorporated System (CEISI 2026) in Mexico City. The project was presented in the Physics (Experimental) category and evaluated across three phases: research protocol, written report, and oral defense before a panel of judges.

The concept builds on existing gravitational energy storage technologies:
- **[Gravity Storage](https://gravity-storage.com/)** — Industrial-scale hydraulic gravity storage
- **[GravityLight](https://www.researchgate.net/publication/324211262)** — Gravity-powered lighting for off-grid communities
- **[Huisman Equipment](https://www.huismanequipment.com/)** — Gravity energy storage demonstrator in Edinburgh

---

## Team

- Mayara Valeria Peláez Beltrán
- Leonardo Bojorquéz Berni
- Sebastián Dussauge Vaca

*Developed at Liceo Mexicano Japonés, A.C. — Mexico City, Mexico*

---

## License

This project is open source under the [MIT License](LICENSE). You are free to replicate, modify, and distribute this design. If you build your own version, we'd love to hear about it.

---

## Contact

For questions, collaboration proposals, or if you've replicated this design in your community:

📧 valerimayara22@gmail.com 

---

*"The future of energy can be written following the most fundamental laws of physics."*
