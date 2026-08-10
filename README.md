# Class D AM Transmitter at 1 MHz - Supplementary Materials

Supplementary materials for the Class D amplitude-modulation transmitter design project. Contains simulation waveforms, FFT spectra, power measurement data, and audio passband verification supporting the main technical paper.

**For complete technical documentation, methodology, and analysis, see [docs/AM_Transmitter_Final.pdf](docs/Comm_Circuits_Final_Proj.pdf)**

---

## Project Overview

**Title:** *Design of a Class D AM Transmitter at 1 MHz on a Single 6 V Supply*

**Key Results:**
- DC dissipation (final stage): 84 mW @ 6 V single supply
- Load power: 13.0 mW into 500 Ω
- Modulation depth: 71% (FFT-derived) at 1 kHz audio
- Total harmonic distortion: 3.4%
- Out-of-band emissions: >28 dB below carrier (8 dB FCC Part 15 margin)
- Audio passband: 234 Hz – 5.85 kHz (−3 dB)
- Parts count: 6 BJTs, 1 op-amp (within budget)

**Architecture:**
- Passive audio bandpass filter with LM358 unity-gain buffer
- Complementary push-pull audio buffer with V_BE-multiplier biasing
- Reverse-wired audio transformer (8.33× step-up) for supply-rail modulation
- Class C RF input buffer referenced to the modulated rail
- Complementary Class D switching pair (2N2907A / 2N2222A)
- Series-LC output tank, Q = 10

---

## Repository Contents

This repository provides **supplementary figures and simulation data** that extend beyond what's included in the main paper. All materials are organized by analysis type for easy reference.

### Structure
```
am-transmitter/
├── docs/
│   └── AM_Transmitter_Final.pdf     # Complete technical paper (primary documentation)
│
├── sim/
│   └── am_transmitter.asc           # LTspice schematic source
│
└── figures/
    ├── architecture/                # Full schematic, block-level diagrams
    ├── switching/                   # Switching-node and rail waveforms
    ├── fft_analysis/                # Spectra for THD and emissions verification
    ├── power_analysis/              # .meas output, power budget breakdown
    └── audio_band_verification/     # Passband endpoints at 250 Hz / 1 kHz / 5 kHz
```

### What's Included

Each analysis directory contains:
- **Simulation Waveforms** - LTspice screenshots at key operating points
- **Extracted Data** - `.meas` results and computed performance metrics
- **Design Characterization** - Time-domain, frequency-domain, and power analysis

**Additional materials beyond the paper:**
- Complete LTspice schematic (`.asc` source and rendered PNG)
- Modulated rail and switching-node waveforms at rail extremes
- FFT spectra for THD calculation and FCC emissions verification
- Power breakdown showing DC supply current, buffer dissipation, and load power
- Audio passband verification at 250 Hz, 1 kHz, and 5 kHz
- Optimization history across design iterations

---

## Quick Links

- **Main Paper:** [docs/AM_Transmitter_Final.pdf](docs/AM_Transmitter_Final.pdf)
- **Complete Schematic:** [figures/architecture/schematic_full.png](figures/architecture/schematic_full.png)
- **FFT Analysis:** [figures/fft_analysis/](figures/fft_analysis/)
- **Switching Waveforms:** [figures/switching/](figures/switching/)
- **Power Analysis:** [figures/power_analysis/](figures/power_analysis/)
- **Audio Band Verification:** [figures/audio_band_verification/](figures/audio_band_verification/)

---

## Design Specifications

| Parameter | Specification | Achieved |
|-----------|--------------|----------|
| Supply Voltage | 6 V single supply | 6 V |
| Carrier Frequency | 1 MHz | 1 MHz |
| Load | 500 Ω | 500 Ω |
| Modulation | AM via power-supply modulation | High-level (rail) modulation |
| DC Power (final stage) | ≤ 100 mW | **84 mW** |
| Modulation Depth | ~70% | **71%** |
| Audio Distortion @ 70% mod | < 10% | **3.4%** |
| Out-of-band Emissions | ≥ 20 dB below carrier | **> 28 dB** below carrier |
| Audio Passband | ~250 Hz – 5 kHz | 234 Hz – 5.85 kHz |
| RF Input | 1 V peak, 50 Ω source | ✓ |
| Audio Input | 1 V peak, 50 Ω source | ✓ |
| Parts (BJTs / op-amps) | ≤ 6 / ≤ 3 | 6 / 1 |

---

## Design Methodology

**Simulator:** LTspice XVII  
**Transistor models:** Manufacturer-provided SPICE models for 2N2222A (Q2N2222Y) and 2N2907A  
**Transformer:** Mouser 42TL001 (Lp = 300 mH, n = 8.333, k = 1)  
**Approach:** Back-to-front design flow — tank Q and load first, then switching pair, RF buffer, and audio chain — with iterative optimization tracked through `.meas` outputs across design revisions

**Key design decisions** (detailed in the paper):
- **Tank Q = 10** derived from the FCC Part 15 mask; the 1707 kHz band edge is the limiting case, requiring Q ≥ 9 for 20 dB attenuation
- **RF buffer supplied from the modulated rail** rather than fixed V_DD — reduces distortion from ~15% to <5% by eliminating the constant-amplitude pedestal in the base drive
- **V_BE multiplier** (Q4) replaces series diodes for push-pull crossover bias (diodes not in permitted parts list)
- **Asymmetric base drive**: 2.2 kΩ steady-state base resistors with 330 pF speed-up capacitors bypass R2/R3 during transitions, keeping switching sharp while minimizing DC dissipation. Sweeping R2/R3 from 1 kΩ to 2.2 kΩ was the single largest power improvement (108 mW → 84 mW); increasing the speed-up caps to 680 pF degraded performance and was reverted
- **Class C bias** on the RF buffer (Q3 biased just below threshold) narrows conduction angle, further reducing average current draw

For pole-zero analysis of the LC tank, transformer coupling calculations, sizing rationale, and complete design methodology, refer to the main paper.

---

## Academic Context

Completed as part of Columbia University's **Electronic Circuits (ELEN E4314)** course, Spring 2026. Demonstrates iterative RF/analog circuit design methodology under strict parts and power constraints, from topology selection through FCC-compliant simulation verification.

**Author:** Albert Wang  
**Institution:** Columbia University, Department of Electrical Engineering  
**Contact:** aw3741@stanford.edu

Course project completed with Christopher Moronta and Caitlin O'Dea.

---

*For questions about the design methodology or technical details, please refer to the paper first, then contact via email.*
