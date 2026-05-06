# Discrete A741 Operational Amplifier

A discrete-component replica of the classic uA741 operational amplifier, designed in JLC EDA Pro.

This project brings the internal architecture of the uA741 out of the IC package and onto a visible PCB. The goal is educational as much as practical: the differential input stage, gain stage, compensation, output buffer, protection choices, and offset-trim behavior can all be studied as real components instead of an invisible silicon die.

The board is not meant to be a modern precision op-amp replacement. It is a buildable, probeable, and visually explicit hardware interpretation of one of the most recognizable analog ICs.

## Features

- Discrete transistor-level uA741-style topology.
- Differential input stage, intermediate voltage-gain stage, Miller compensation, and output buffer.
- 0805 passive components for compact layout.
- SOT-223 transistor packages for easier hand soldering than very small SMD packages.
- Integrated offset-trim potentiometer support.
- Input-stage protection diodes for the lower reverse breakdown voltage of discrete transistors.
- JLC EDA Pro project export, Altium schematic/PCB export, manufacturing outputs, and preview documents included.

## Hardware Overview

The design follows the familiar three-stage op-amp structure:

```text
Differential input stage
  -> high-gain intermediate stage with compensation
  -> class-AB style output buffer
```

The reference design uses discrete transistor pairs where the original integrated circuit relies on closely matched devices. Because discrete transistors do not naturally share the same process environment, device matching is one of the most important parts of a successful build.

## Component Selection & Design Notes

All resistors and capacitors in this project are specified in 0805 surface-mount packages. Transistors are selected in SOT-223 packages for their current-handling capability and relative ease of manual soldering.

Recommended transistor families:

| Device | Type | Notes |
| --- | --- | --- |
| `BCP53-16` | PNP transistor | Used for PNP positions in the discrete op-amp core. |
| `BCP56-16` | NPN transistor | Used for NPN positions in the discrete op-amp core. |

## Key Considerations

1. Transistor Matching

   The uA741 architecture depends heavily on matched transistor behavior, especially in current-mirror and differential-pair sections. For best results, measure and select closely matched devices before soldering. If direct current-gain measurement is not available, matching base-emitter voltage under the same test current is a useful practical approximation.

2. Matched Pairs

   The reference build selected six closely matched transistor pairs. In the article build log, the matched pairs were selected to within about 1 mV of base-emitter voltage difference.

3. Input-Stage Protection

   The original uA741 input devices tolerate much larger reverse base-emitter voltage than common discrete substitutes. Discrete BCP53/BCP56 devices have much lower reverse base-emitter breakdown voltage, so the design adds Schottky protection diodes in the input stage.

4. Protection Diode Matching

   If the Schottky protection diodes are installed, select a matched pair with similar forward voltage. A mismatch will add input offset and disturb the symmetry of the input stage.

5. Authenticity Option

   The protection diode positions may be shorted for a more direct structural replica, but then the differential input voltage must be kept within a safe range. Excessive differential input voltage can permanently damage the input transistors.

6. Offset Trim

   The board includes support for offset trimming. In the reference voltage-follower test, the output/input offset was about 0.7 mV before installing the trim potentiometer and below 0.1 mV after adjustment.

7. Mechanical Interface

   The external connection holes are sized for M1.4 screws and stripped DuPont wire ends. This makes the board convenient for bench probing and also gives it a display-object form factor.

## Repository Contents

| Path | Description |
| --- | --- |
| `Altium_741_2025-12-09.zip` | Altium export containing the schematic and PCB files. |
| `ProPrj_741_2025-12-09.epro` | JLC EDA Pro project export. |
| `Documentation/SCH_741_Schematic_2025-12-09.pdf` | Schematic PDF preview. |
| `Documentation/PCB_741_PCB_2025-12-09.pdf` | PCB PDF preview. |
| `Manufacturing/Gerber_741_PCB_2025-12-09.zip` | Gerber manufacturing export. |
| `Manufacturing/BOM_Board1_741_PCB_2025-12-09.csv` | Bill of materials export. |
| `Manufacturing/PickAndPlace_741_PCB_2025-12-09.xlsx` | Pick-and-place export. |
| `Mechanical/3D_741_PCB_2025-12-09.step` | 3D STEP model export. |
| `LICENSE` | MIT license. |
| `README.md` | Project introduction and design notes. |

## Opening the Project

Use `ProPrj_741_2025-12-09.epro` to import the project back into JLC EDA Pro.

Use `Altium_741_2025-12-09.zip` if you want to inspect or modify the exported Altium schematic and PCB files.

## Project Status

This repository contains editable source exports and manufacturing outputs for the current public release. Review all fabrication and assembly files before ordering hardware.

## Background

- Background article: https://mp.weixin.qq.com/s/IK9VtsLIkvPyMW0aoyFaIw

## License

This project is released under the MIT License.
