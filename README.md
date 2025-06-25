# BackyardRadioScope
Small format software-directed radio telescope intended for backyard astronomy.

## Table of Contents
- [BackyardRadioScope](#backyardradioscope)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Goals and Vision](#goals-and-vision)
  - [Research Notes](#research-notes)
    - [To Read](#to-read)
    - [Constants](#constants)
      - [Field of View, Pixel Count, and Storage Tables](#field-of-view-pixel-count-and-storage-tables)
    - [Antenna Notes](#antenna-notes)
  - [Ideas and Brainstorming](#ideas-and-brainstorming)
    - [Signal Path Layout](#signal-path-layout)
    - [Hardware Candidates](#hardware-candidates)
  - [Software Used](#software-used)
    - [Design and Simulation](#design-and-simulation)
    - [Control](#control)
    - [Processing](#processing)
  - [Challenges and Questions](#challenges-and-questions)
  - [Next Steps](#next-steps)
  - [Image Resolution Requirements](#image-resolution-requirements)

## Introduction
This repository is currently a space for brainstorming, researching, and developing ideas for the BackyardRadioScope project. The goal is to explore the feasibility and design of a small, software-directed radio telescope for amateur astronomy enthusiasts.

## Goals and Vision
This project aims to make radio astronomy accessible to hobbyists by developing a compact, software-directed radio telescope. The key goals and vision for the project include:

- **Compact Design**: Utilize a small array of directional antennas to reduce the physical space required for operation while maintaining effective resolution.
- **Beam Steering**: Implement beam steering technology to map the sky quickly and efficiently without relying on moving parts, unlike traditional dish or horn-based telescopes.
- **Accessibility**: Design the system to be affordable and user-friendly, making it accessible to amateur astronomers and hobbyists.
- **Full-Sky Mapping**: Enable the system to resolve the entire sky efficiently, providing a comprehensive view of space-based radio signals.
- **Citizen Science**: Enable users to publish time-coded datasets, allowing for collaborative data sharing. By synchronizing data from projects deployed far apart, the system can achieve higher resolution, effectively creating a virtual radio telescope with a baseline as large as the distance between the receivers.

## Research Notes
Document findings from your research here. Include:
- Links to relevant articles, papers, or resources.
- Notes on existing technologies or similar projects.
- Technical concepts or principles to explore.

Patch Antenna Design - 
https://resources.altium.com/p/microstrip-patch-antenna-calculator-rf-designers

### To Read

- [Radio Telescope Front-End Survey](https://arxiv.org/pdf/1907.02491)
- [Introduction to Radio Astronomy](https://www.jb.man.ac.uk/ira4/IRA4%20SuppMat_Chapter1_and_Prologue.htm)
- [Antennas for Radio Astronomy](https://www.arrl.org/files/file/Antennas%20for%20Radio%20Astronomy%20-%20PDF.pdf)
- [Radio Astronomy Receivers](https://apps.dtic.mil/sti/tr/pdf/AD0268503.pdf)
- [Example Amateur Scope Build](https://physicsopenlab.org/2020/10/10/a-simple-11-2-ghz-radiotelescope/)
- [Fundamentals of Radio Astronomy](https://pulsar.sternwarte.uni-erlangen.de/black-hole/1stschool/coursematerial/Lang_Fundamentals_June09.pdf)
- [Instruments for RadioAstronomy](https://moodle2.units.it/pluginfile.php/719589/mod_resource/content/1/Lezione7-27-03-24.pdf)
- [Example Scope Build and Software Setup](https://www.rtl-sdr.com/cheap-and-easy-hydrogen-line-radio-astronomy-with-a-rtl-sdr-wifi-parabolic-grid-dish-lna-and-sdrsharp/)
- [Telescope Setup](https://www.radio-astronomy.org/node/118)
- 

### Constants

- Hydrogen Line - 1.42 GHz
  - Full Wave - 21.11 cm ( 8.32" )
  -  1/2 Wave - 10.56 cm ( 4.16" )
  -  1/4 Wave -  5.28 cm ( 2.08" )

#### Field of View, Pixel Count, and Storage Tables

**At 1 arcsecond per pixel:**

| Field of View (deg) | Arcseconds per Side | Pixels per Side | Total Pixels         | Storage (32-bit, 4 bytes/pixel) |
|---------------------|--------------------|-----------------|----------------------|----------------------------------|
| 10 × 10             | 36,000             | 36,000          | 1.296 × 10⁹          | ~5.2 GB                          |
| 30 × 30             | 108,000            | 108,000         | 1.166 × 10¹⁰         | ~46.6 GB                         |
| 60 × 60             | 216,000            | 216,000         | 4.67 × 10¹⁰          | ~186.8 GB                        |
| 120 × 120           | 432,000            | 432,000         | 1.87 × 10¹¹          | ~747 GB                          |

**At 1 arcminute per pixel:**

| Field of View (deg) | Arcminutes per Side | Pixels per Side | Total Pixels         | Storage (32-bit, 4 bytes/pixel) |
|---------------------|--------------------|-----------------|----------------------|----------------------------------|
| 10 × 10             | 600                | 600             | 360,000              | ~1.4 MB                          |
| 30 × 30             | 1,800              | 1,800           | 3,240,000            | ~12.4 MB                         |
| 60 × 60             | 3,600              | 3,600           | 12,960,000           | ~49.4 MB                         |
| 120 × 120           | 7,200              | 7,200           | 51,840,000           | ~197.1 MB                        |

**At 1 degree per pixel:**

| Field of View (deg) | Pixels per Side | Total Pixels | Storage (32-bit, 4 bytes/pixel) |
|---------------------|----------------|-------------|----------------------------------|
| 10 × 10             | 10             | 100         | ~0.0004 MB                       |
| 30 × 30             | 30             | 900         | ~0.0034 MB                       |
| 60 × 60             | 60             | 3,600       | ~0.014 MB                        |
| 120 × 120           | 120            | 14,400      | ~0.055 MB                        |

- **Note:** 1 degree = 60 arcminutes = 3,600 arcseconds.
- **Assumption:** Square field of view, 32 bits (4 bytes) per pixel.

These tables illustrate how pixel scale dramatically affects storage and processing requirements. Choose the appropriate scale for your scientific goals and hardware capabilities.

### Antenna Notes

- Return Loss - Reflection noise of signals in the antenna. 
- Antenna Wave Size - 1/4, 1/2, Full
  - Hydrogen Line - 
- Antenna spacing - 1/2 wave

### Loop Antenna Size and Performance Table (1.42 GHz)

| Fraction of Wavelength | Circumference (cm) | Diameter (cm) | Approx. Impedance (Ω) | Approx. Gain (dBi) | Efficiency (%) | Bandwidth (MHz) |
|-----------------------|--------------------|---------------|-----------------------|--------------------|----------------|-----------------|
| 1 (Full wave)         | 21.11              | 6.72          | 100–120               | 2.0–2.5            | 90–95          | 110–140         |
| 0.9                   | 19.00              | 6.05          | 90–110                | 1.8–2.2            | 85–90          | 90–120          |
| 0.8                   | 16.89              | 5.38          | 80–100                | 1.5–2.0            | 80–85          | 70–100          |
| 0.7                   | 14.78              | 4.71          | 70–90                 | 1.2–1.8            | 75–80          | 55–80           |
| 0.6                   | 12.67              | 4.03          | 60–80                 | 1.0–1.5            | 65–75          | 40–60           |
| 0.5 (Half wave)       | 10.56              | 3.36          | 50–70                 | 0.5–1.2            | 50–65          | 25–40           |
| 0.4                   | 8.44               | 2.69          | 40–60                 | 0.0–0.8            | 35–50          | 10–20           |
| 0.3                   | 6.33               | 2.02          | 30–50                 | -1.0–0.5           | 20–35          | 3–8             |
| 0.2                   | 4.22               | 1.34          | 20–40                 | -2.5–-0.5          | 10–20          | 1–2             |
| 0.1                   | 2.11               | 0.67          | 10–20                 | -5.0–-2.0          | <10            | <1              |

**Notes:**
- All values are approximate and for free-space, single-turn circular loops at 1.42 GHz (Hydrogen Line).
- Bandwidth is for VSWR < 2:1 and depends on construction and matching.
- Small loops (<0.2λ) are very inefficient and narrowband, but may be useful for compact arrays.

## Ideas and Brainstorming
Use this section to jot down ideas, no matter how rough. For example:
- Potential hardware components (e.g., SDRs, antennas).
- Software features or tools.
- Possible use cases or applications.

Currently imagined as a 3x3x3 cube of hardware delayed and filtered antennas. The cube will have one output that is a sum of the signals from all antennas (probably a microcontroller). Cube size is currently imagined to be somewhere between 6" and 1' in length/width/height with all 9 antennas evenly spaced and facing upwards. 

### Signal Path Layout
Antenna (per element)
  → Filter
  → Low-Noise Amplifier (LNA)
  → Variable Delay/Phase Shifter (for beam steering)
  → (Optional: Downconverting Mixer to IF, LO phase-locked to master clock)
  → (Optional: Analog Summing)
  → ADC (per element or summed, all ADCs clocked by master clock)
  → Controller/FPGA (also clocked by master clock)

Antenna gain pattern needs to match the area of the sky seeking to be reasonably scanned. This is a maximum of 180 degrees (horizon to horizon), but more than likely will normally be less than that by 10-20 degrees from surrounding trees and houses (140 - 160 degree total range). Filters should be inline with the antenna, and before the delay. Delay/phase shifting is used for beam steering and must be controlled remotely. A downconverting mixer can be used to shift the signal to a lower intermediate frequency (IF) for easier digitization and processing. Signals can be summed in analog before ADC, or digitized individually and summed in the controller (digital beamforming). Pre-summing may help increase signal above the noise floor before hitting the controller.

### Hardware Candidates
Functionality and cost are key concerns. The broader the band coverage the better, or have fixed to Hydrogen Line.

- **Antennas (per element)**
  - Size is the most important factor. Directionality should not be too extreme to avoid limiting the array's steering capability.
  - Helical
    - Possibly too big, unsure if antenna can be used at partial wavelength sizes
  - Dipole
    - https://www.mouser.com/datasheet/2/447/datasheet_sb617_7125g0400_1712181779-3503718.pdf
    - https://www.mouser.com/datasheet/2/4/ant_190541b97_data_sheet-3397010.pdf
  - Log Periodic
  - Loop Antenna
    - Down to 1/10 wavelength circumference
  - Patch
    - About same size as full wavelength loop antenna, maybe a little smaller

- **Filter (per element)**
  - Fixed or adjustable?
  - Nooelec SAWbird+ H1 Barebones
    - Inline filter preset to Hydrogen line (good first candidate for initial scope frequency)

- **Low-Noise Amplifier (LNA, per element)**
  - Critical for boosting weak signals with minimal added noise.

- **Variable Delay/Phase Shifter (per element)**
  - Used for beam steering, must be remotely controllable.

- **Downconverting Mixer (per element, optional)**
  - Shifts the signal to a lower intermediate frequency (IF) for easier digitization and processing.
  - Candidates:
    - [MAX2680](https://www.mouser.com/datasheet/2/609/MAX2680_MAX2682-3128292.pdf)
      - $3 per input
    - [F1152](https://www.mouser.com/datasheet/2/698/REN_F1152_DST_20120615_1-1997540.pdf)
      - $4 per input (Dual input RF to IF)
      - Unsure if this will actually work like I believe it will...

- **Analog Summing (optional)**
  - Can sum signals before digitization to improve SNR, or skip for digital beamforming.

- **ADC (per element or summed)**
  - Converts analog signals to digital for processing.

- **Controller**
  - FPGA or microcontroller for digital summing/beamforming and overall system control.

- **Master Clock**
  - Provides a synchronized clock signal to all ADCs and digital processing components (FPGA/microcontroller) to ensure coherent sampling and processing across the array.
  - If using downconverting mixers, local oscillators should be phase-locked to the master clock for channel coherence.

- **Other**
  - Power supply, enclosure, and any necessary RF shielding.

## Software Used

### Design and Simulation

### Control

### Processing

## Challenges and Questions
List any challenges or open questions you encounter during brainstorming:
- What are the limitations of small-scale radio telescopes?
- How can the system be made affordable without sacrificing performance?
- What software frameworks are best suited for this project?
- How to maintain a reasonable amount of data collection?

## Next Steps
Outline immediate next steps or tasks to focus on. For example:
- Research existing radio telescopes and operating bands.
- Identify potential hardware components.
- Explore software libraries for signal processing.

## Image Resolution Requirements

The final image produced by the BackyardRadioScope will have the following characteristics:

- **Fixed Output Size:** Images will be generated at a fixed resolution, for example 2000 × 2000 pixels.
- **Pixel Format:** Each pixel will be stored as a 32-bit value (e.g., floating point or integer, depending on processing requirements), allowing for a wide dynamic range and precise intensity representation.
- **Flexible Field of View:** The system can generate a full-sky image at maximum angular resolution, or focus on a smaller region of the sky at finer detail (e.g., arcminute or arcsecond per pixel).
- **Example Storage Requirements:**
  - 1000 × 1000 pixels × 4 bytes/pixel = ~4 MB per image
  - 2000 × 2000 pixels × 4 bytes/pixel = ~16 MB per image
  - 4000 × 4000 pixels × 4 bytes/pixel = ~64 MB per image
- **Dynamic Mapping:** The field of view and pixel scale can be adjusted, enabling both wide-field surveys and high-detail studies.
- **Calibration & Accuracy:** Calibration routines will ensure accurate mapping from sky coordinates to image pixels.
- **Output Format:** Images can be exported in standard formats (e.g., PNG, FITS) for analysis or sharing.

This approach provides predictable storage and processing requirements, while supporting both broad and detailed imaging modes.

