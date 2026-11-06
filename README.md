# 4-bit R-2R Ladder DAC with Counter (LTspice)

Design and simulation of a **4-bit R-2R ladder digital-to-analog converter** in LTspice. The simulated outputs are checked against theory, and the DAC is then driven by a 4-bit counter to generate a staircase waveform automatically.

**Course:** Analog Circuits (BECE206L), VIT Vellore
**Author:** Dhruv Lazar
**Tools:** LTspice

---

## Design

- **R-2R ladder:** R = 10 kΩ, 2R = 20 kΩ. Only two resistor values are needed, so it's easy to build accurately.
- **Op-amp summing stage** (Rf = 2R), followed by a **−1 inverting stage** so the output is positive.
- **Reference voltage:** Vref = 5 V. Logic 1 = Vref, logic 0 = ground.
- **Resistor values are parameterised** in the schematic, so other values can be simulated easily.

Output equation:

```
Vout = (Vref / 16) · (8·B3 + 4·B2 + 2·B1 + 1·B0)
```

The resolution (1 LSB) is 5/16 = **0.3125 V**.

## Results: theory vs simulation

| B3 B2 B1 B0 | Theory (V) | LTspice (V) |
|---|---|---|
| 0000 | 0 | 0 |
| 0001 | 0.3125 | 0.3125 |
| 0010 | 0.625 | 0.6250 |
| 0100 | 1.25 | 1.2500 |
| 1000 | 2.5 | 2.4990 |
| 1100 | 3.75 | 3.7499 |
| 1111 | 4.6875 | 4.6873 |

All 16 codes match theory to within about 1%, and the output rises linearly with the input code.

## Counter-driven version

A 4-bit binary counter replaces the manual switches. It steps through codes 0000 to 1111, and the DAC outputs a staircase from 0 to 0.9375 V (with Vref = 1 V).

## Applications

- Audio output
- Function generators
- Microcontroller analog outputs
- Data acquisition

## Limitations and next steps

- Accuracy depends on how well the resistors match.
- The basic stage inverts the output, so an extra stage is needed.

Next steps:
- 8-bit or 12-bit versions
- CMOS switches
- A hardware build driven by an Arduino
