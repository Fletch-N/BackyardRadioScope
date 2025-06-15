# BackyardRadioScope
Small format software-directed radio telescope intended for backyard astronomy.

## Table of Contents
- [BackyardRadioScope](#backyardradioscope)
  - [Table of Contents](#table-of-contents)
  - [Introduction](#introduction)
  - [Goals and Vision](#goals-and-vision)
  - [Research Notes](#research-notes)
    - [Constants](#constants)
    - [Antenna Notes](#antenna-notes)
  - [Ideas and Brainstorming](#ideas-and-brainstorming)
    - [Signal Path Layout](#signal-path-layout)
    - [Hardware Candidates](#hardware-candidates)
  - [Challenges and Questions](#challenges-and-questions)
  - [Next Steps](#next-steps)

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

### Constants

- Hydrogen Line - 1.42 GHz
  - Full Wave - 21.11 cm ( 8.32" )
  -  1/2 Wave - 10.56 cm ( 4.16" )
  -  1/4 Wave -  5.28 cm ( 2.08" )

### Antenna Notes

- Return Loss - Reflection noise of signals in the antenna. 
- Antenna Wave Size - 1/4, 1/2, Full
  - Hydrogen Line - 
- Antenna spacing - 1/2 wave

## Ideas and Brainstorming
Use this section to jot down ideas, no matter how rough. For example:
- Potential hardware components (e.g., SDRs, antennas).
- Software features or tools.
- Possible use cases or applications.

Currently imagined as a 3x3x3 cube of hardware delayed and filtered antennas. The cube will have one output that is a sum of the signals from all antennas (probably a microcontroller). Cube size is currently imagined to be somewhere between 6" and 1' in length/width/height with all 9 antennas evenly spaced and facing upwards. 

### Signal Path Layout
Antenna (per element) => Filter => Low-Noise Amplifier (LNA) => Variable Delay/Phase Shifter (for beam steering) => (Optional: Analog Summing) => ADC (per element or summed) => Controller (for digital summing/processing)

Antenna gain pattern needs to match the area of the sky seeking to be reasonable scanned. This is a maximum of 180 degrees (horizon to horizon), but more than likely will normally be less than that by 10-20 degrees from surrounding trees and houses (140 - 160 degree total range). Filters should be inline with the antenna, and before the delay. Delay/phase shifting is used for beam steering and must be controlled remotely. Signals can be summed in analog before ADC, or digitized individually and summed in the controller (digital beamforming). Pre-summing may help increase signal above the noise floor before hitting the controller.

### Hardware Candidates
Functionality and Cost are key concerns. Active or passive? The broader the band coverage the better, or have fixed to Hydrogen Line.

- **Antennas**
  Thinking size is the most important factor here. Directionality is secondary, and should not be too extreme to prevent limiting the directional capabilities of the phased array.
  - Helical
    - Possibly too big, unsure if antenna can be used at partial wavelength sizes
  - Dipole
    - https://www.mouser.com/datasheet/2/447/datasheet_sb617_7125g0400_1712181779-3503718.pdf
    - https://www.mouser.com/datasheet/2/4/ant_190541b97_data_sheet-3397010.pdf
  - Log Periodic
  - Loop Antenna
    -  down to 1/10 wavelength circumfrence
  - Patch
    - about same size as full wavelength loop antenna, maybe a little smaller
- **Filter**
  - Fixed or Adjustable?
  - Nooelec SAWbird+ H1 Barebones
    - Inline filter preset to Hydrogen line ( good first candidate for inital scope frequency )
- **Delay**
- **Controller**
  - FPGA
  - Microcontroller

## Challenges and Questions
List any challenges or open questions you encounter during brainstorming:
- What are the limitations of small-scale radio telescopes?
- How can the system be made affordable without sacrificing performance?
- What software frameworks are best suited for this project?

## Next Steps
Outline immediate next steps or tasks to focus on. For example:
- Research existing radio telescopes and operating bands.
- Identify potential hardware components.
- Explore software libraries for signal processing.

---

