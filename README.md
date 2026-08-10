# Class D AM Transmitter at 1 MHz - Supplementary Materials

Supplementary materials for the Class D amplitude-modulation transmitter design project. Contains simulation waveforms, FFT spectra, power measurement data, and audio passband verification supporting the main technical paper.

**For complete technical documentation, methodology, and analysis, see [docs/AM_Transmitter_Final.pdf](docs/AM_Transmitter_Final.pdf)**

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
