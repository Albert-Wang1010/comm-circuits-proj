### What's Included

Each analysis directory contains:
- **Simulation Waveforms** - LTspice screenshots at key operating points
- **Extracted Data** - `.meas` results and computed performance metrics
- **Design Characterization** - Time-domain, frequency-domain, and power analysis

**Materials provided:**
- Complete LTspice schematic (`.asc` file and rendered PNG)
- Modulated rail and switching-node waveforms at rail extremes
- FFT spectra for THD calculation and FCC emissions verification
- Power breakdown showing DC supply current, buffer dissipation, and load power
- Audio passband verification at 250 Hz, 1 kHz, and 5 kHz

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
| DC Power (final stage) | ≤ 100 mW | **83.9 mW** |
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

**Approach:** Iterative simulation-driven design starting from the topology on p. 105 of the course notes, with successive optimization of the audio chain, RF buffer, and Class D output stage. Distortion and power were minimized jointly by tracking `.meas` outputs across design iterations, using FFT-derived modulation depth and sideband ratios as the primary distortion metric.

**Key design decisions** (detailed in the paper):
- **Vbe multiplier** (Q4) replaces series diodes for push-pull crossover bias (diodes not in permitted parts list)
- **RF buffer supplied from modulated rail** rather than fixed VDD — reduces distortion from ~15% to <5% by ensuring the RF drive tracks the modulation envelope
- **Asymmetric base drive**: large steady-state base resistors (2.2 kΩ) with 470 pF speedup capacitors bypass R2/R3 during transitions, keeping switching sharp while minimizing DC dissipation
- **Class C bias** on the RF buffer (Q3 biased just below threshold) narrows conduction angle, further reducing average current draw

For pole-zero analysis of the LC tank, transformer coupling calculations, sizing rationale, and complete design methodology, refer to the main paper.

---

## Academic Context

Completed as part of Columbia University's **Electronic Circuits (ELEN E4314)** course, Spring 2025. Demonstrates iterative RF/analog circuit design methodology under strict parts and power constraints, from topology selection through FCC-compliant simulation verification.

**Author:** Albert Wang  
**Institution:** Columbia University, Department of Electrical Engineering  
**Contact:** aw3741@columbia.edu

---

## Acknowledgments

The author thanks Christopher Moronta and Caitlin O'Dea for contributions to the audio-chain design and iterative simulation debugging.

---

*For questions about the design methodology, technical details, or collaboration opportunities, please refer to the paper first, then contact via email.*
