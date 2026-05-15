# Gravity Fall — Build Guide

## How to Build a Gravitational Energy Storage System for ~$400 USD

*This guide will walk you through building a mechanical battery that converts gravitational potential energy into usable electricity. No industrial tools required.*

---

## What You'll Build

A system where a heavy mass (15.65 kg) descends from 1.80 m through a chain-driven transmission, spinning a hub motor that generates up to 13W of electricity at 58% efficiency. The output is regulated and stored in a battery, then converted to 5V USB for device charging.

**Difficulty:** Intermediate (basic mechanical assembly + basic electrical wiring)
**Time:** 2-3 weekends
**Cost:** ~$7,000 MXN / ~$400 USD (DIY) | $15,000-$20,000 MXN if professionally fabricated
**Tools needed:** Wrench set, screwdriver, soldering iron, multimeter, drill

---

## Bill of Materials

### Mechanical

| # | Component | Specification | Qty | Source | Est. Cost (MXN) |
|---|-----------|--------------|-----|--------|-----------------|
| 1 | Wooden beams | 2" x 4" x 2m | 4 | Hardware store | $500 |
| 2 | Bicycle chains | Standard | 2 | Bike shop | $200 |
| 3 | Large sprocket | ~20 teeth | 1 | Bike shop | $150 |
| 4 | Small sprocket | Custom (1:9 ratio) | 1 | 3D print / machined | $300 |
| 5 | Steel axles | 12mm diameter | 2 | Hardware store / industrial | $400 |
| 6 | Bearings | 6201-2RS (12mm bore) | 4 | Hardware store | $200 |
| 7 | Mass container | Bucket or custom frame | 1 | Recycled | $0 |
| 8 | Sand/weights | To reach 15.65 kg total | — | Local | $50 |
| 9 | Mounting hardware | Bolts, nuts, brackets | — | Hardware store | $200 |

### Electrical

| # | Component | Specification | Qty | Source | Est. Cost (MXN) |
|---|-----------|--------------|-----|--------|-----------------|
| 10 | Hub motor | 36V, multi-pole | 1 | Online | $2,500 |
| 11 | Neodymium magnets | For magnetic brake | 4-6 | Online | $500 |
| 12 | MPPT charge controller | 10A, adjustable | 1 | Electronics store | $600 |
| 13 | LiFePO4 battery | 12V, 6Ah minimum | 1 | Electronics store | $1,200 |
| 14 | DC-DC buck converter | 12V→5V, 3A | 1 | Electronics store | $300 |
| 15 | USB-C breakout board | Female, for output | 1 | Electronics store | $50 |
| 16 | Wiring | 14-16 AWG, silicone | 2m | Electronics store | $100 |

**Estimated DIY total: ~$7,000 MXN (~$400 USD)**

*Note: Our prototype cost $15,000–$20,000 MXN because we commissioned professional carpentry and CNC machining for the frame and custom parts. The estimates above assume you build the frame yourself and 3D print custom components from the provided FreeCAD files.*

---

## Step 1: Build the Frame

**Goal:** A rigid vertical structure that supports the mass descent path and motor assembly.

1. Cut four 2m wooden beams to your desired height (we used 1.80 m effective height).
2. Assemble a rectangular frame using bolts — not nails. You need rigidity without vibration.
3. Mark the motor mounting position at the bottom and the release mechanism position at the top.
4. Ensure the frame is perfectly vertical. Use a level. Any tilt will cause the mass to swing during descent.

**Critical dimension:** The effective drop height is your total height minus the motor assembly space and top mechanism. In our case: 1.80 m total, 1.39 m effective drop, 0.41 m dead space. Minimize dead space.

---

## Step 2: Install the Chain Drive

**Goal:** A 1:9 gear ratio transmission that multiplies the slow descent into fast motor rotation.

1. Mount the large sprocket (driven) on the mass descent axle.
2. Mount the small sprocket (driver) on the motor axle.
3. Connect with the bicycle chain. Ensure proper tension — too loose and it skips, too tight and friction increases.
4. Test by hand: rotating the large sprocket one full turn should spin the small sprocket approximately 9 times.

**Why 1:9?** A falling mass moves slowly. The hub motor needs higher RPM to generate meaningful voltage. The gear ratio bridges this gap. We tested 1:5 first — it was insufficient. The jump to 1:9 was the single most impactful design change.

**Tip:** Clean and lubricate chains thoroughly before installation. Chain friction accounted for ~10% energy loss in our system.

---

## Step 3: Mount the Hub Motor and Magnetic Brake

**Goal:** Controlled energy extraction from the descending mass.

1. Secure the hub motor to the frame at the small sprocket position.
2. Position neodymium magnets around the motor's rotating element to create eddy current braking.
3. Adjust magnet distance to control braking force. Closer = more braking = slower descent = more controlled output.
4. Test: the mass should descend smoothly over ~9-10 seconds. If it falls faster, add braking force. If it barely moves, reduce it.

**Why magnetic braking?** Without it, the mass accelerates under gravity and the motor spins too fast, producing voltage spikes that can damage the electronics. The magnetic brake provides smooth, consistent energy extraction.

---

## Step 4: Wire the Electrical System

**Goal:** Convert the motor's AC output into stable, stored DC power.

```
Hub Motor (AC out) → MPPT Controller (input) → LiFePO4 Battery (12V) → DC-DC Converter → USB-C (5V out)
```

1. Connect the hub motor output wires to the MPPT controller input.
2. Connect the MPPT output to the LiFePO4 battery terminals (observe polarity!).
3. Connect the battery output to the DC-DC buck converter input.
4. Set the DC-DC converter output to 5V using the adjustment potentiometer.
5. Wire the DC-DC output to the USB-C breakout board.
6. Verify all connections with a multimeter before first test.

**Safety:** LiFePO4 batteries are among the safest lithium chemistries, but always include a fuse between the battery and the DC-DC converter. Never short-circuit the battery terminals.

---

## Step 5: Test and Measure

**Goal:** Validate performance and gather data.

### Measurements to take:
- **Voltage** at motor output, battery terminals, and USB output (multimeter)
- **Fall time** for each mass configuration (stopwatch)
- **Mass** of the descending weight (scale)

### Calculated values:
- **Gravitational PE:** Ug = m × g × h (in Joules)
- **Electrical energy:** P × t (Power × time, in Joules)
- **System efficiency:** (Electrical energy out / Gravitational PE in) × 100%

### Test protocol:
1. Start with your lowest mass. Measure and record.
2. Increase mass by 2-3 kg increments. Measure and record each time.
3. Plot at least three data points for: Efficiency vs Mass, Power vs Torque, Angular Velocity vs Mass.
4. Look for the stabilization point — where adding more mass no longer increases speed but continues increasing power. That's your optimal operating range.

---

## Step 6: Iterate

Your first build will not hit 58% efficiency. Ours didn't either. Here's what to look for:

| Problem | Likely Cause | Fix |
|---------|-------------|-----|
| Mass barely moves | Too much magnetic braking or too much chain friction | Reduce magnets or lubricate chain |
| Mass falls too fast | Not enough braking | Add magnets or move them closer |
| Low voltage output | Motor RPM too low | Increase gear ratio or add mass |
| Voltage spikes | Uncontrolled descent speed | Adjust magnetic brake for stability |
| Battery not charging | MPPT settings incorrect | Reconfigure MPPT for your battery chemistry |

---

## Your Results vs Ours

| Metric | Our Prototype | Your Build |
|--------|--------------|------------|
| Peak Power | 13W | _______ W |
| Efficiency | 58% | _______ % |
| Fall Time | 9.5 s | _______ s |
| Best Mass | 15.65 kg | _______ kg |

Share your results! Open an issue on the GitHub repository or tag us on social media.

---

## Safety Notes

- The descending mass carries significant kinetic energy. Keep hands and feet clear during operation.
- Secure the frame to a wall or floor to prevent tipping.
- Never exceed the structural capacity of your frame.
- Use proper electrical safety: fuses, insulated connections, no exposed terminals.
- LiFePO4 batteries are safe but should never be punctured, shorted, or overcharged beyond 14.6V.

---

## License

This build guide is released under the MIT License. Build it, modify it, share it. If you improve the design, submit a pull request.
