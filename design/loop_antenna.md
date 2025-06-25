# Loop Antenna Research for BackyardRadioScope

This document collects research, design notes, and performance data for loop antennas intended for use in a compact, phased array radio telescope operating at the 1.42 GHz hydrogen line.

## Why Loop Antennas?

- **Compact size:** Suitable for dense arrays and backyard installations.
- **Broad beamwidth:** Useful for wide sky coverage and electronic beam steering.
- **Low profile:** Easier to mount and integrate into array structures.
- **Polarization:** Sensitive to the magnetic field perpendicular to the plane of the loop.

## Loop Antenna Size and Performance Table (1.42 GHz)

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

## Design Considerations

- **Element Spacing:** For phased arrays, space elements at ~0.5λ (≈10.5 cm) center-to-center to avoid grating lobes.
- **Impedance Matching:** Full-wave loops have higher impedance (~100–120 Ω), half-wave loops are closer to 50 Ω. Matching networks or baluns may be required.
- **Efficiency:** Larger loops are more efficient and broadband; smaller loops are less efficient and narrowband.
- **Construction:** Use copper wire or tubing (2–3 mm diameter) for low loss. Mount on non-conductive frames.

## Downsides of Half-Wave vs Full-Wave Loops

| Aspect                | Full-Wave Loop                  | Half-Wave Loop                      | Downsides of Half-Wave Loop                |
|-----------------------|---------------------------------|-------------------------------------|--------------------------------------------|
| Impedance             | ~100–120 Ω                      | ~50–70 Ω                            | Lower, but easier to match to 50 Ω         |
| Radiation Resistance  | Higher (better efficiency)      | Lower (less efficient, more loss)   | Lower efficiency, more loss to heat        |
| Bandwidth             | Wider                           | Narrower                            | More sensitive to frequency drift          |
| Gain                  | Slightly higher                 | Slightly lower                      | Slightly less sensitive                    |
| Size                  | Larger                          | Smaller                             | None (size is an advantage here)           |
| Pattern               | Similar (broadside)             | Similar                             | Minimal difference                         |

## Example Construction Steps

1. **Form the Loop:** Bend copper wire into a circle with the desired diameter. Leave a small gap (~2–5 mm) for the feed point.
2. **Attach Feed:** Solder the center conductor of the coax to one end of the gap, and the shield to the other. Optionally, add a small trimmer capacitor (1–5 pF) in series for impedance matching.
3. **Mount:** Secure the loop on a non-conductive frame.
4. **Impedance Matching:** Use a matching network or balun as needed.

## References

- [Wikipedia: Loop antenna](https://en.wikipedia.org/wiki/Loop_antenna)
- [ARRL Antenna Book](http://www.arrl.org/arrl-antenna-book-reference)
- [Hydrogen Line Antenna Projects](https://www.rtl-sdr.com/tag/hydrogen-line/)

---