# My PCB Design Journal

[中文版本](./README.md)

A beginner's log of PCB design projects — from a first 8051 dev board to power boards built for a robotics arm. Each board marks a stage in the learning process. All designs were made with **LCEDA**, a free EDA tool by JLCPCB.

---

## Repository Structure

```
my_PCB_works/
├── docs/
│   ├── images/                              # Board renders and layout screenshots
│   ├── SCH_STC89C52_Dev_Board.pdf           # Schematic: 51 MCU board
│   ├── SCH_Buck_Converter_PDB.pdf           # Schematic: buck converter power board
│   └── SCH_Robot_Arm_End_PDB.pdf           # Schematic: robot arm end power board
├── MCU_Development_Board/
│   └── STC89C52_Dev_Board.eprj2            # 51 MCU dev board
└── Power_Distribution_Board/
    ├── Buck_Converter_PDB/
    │   ├── Buck_Converter_PDB.eprj2         # Power board with voltage converter (final)
    │   └── Buck_Converter_PDB_Draft.eprj2   # Same design, early draft
    └── Robot_Arm_End_PDB/
        └── Robot_Arm_End_PDB.eprj2          # Robot arm end power board
```

---

## Projects

### 1. STC89C52 MCU Dev Board
> `MCU_Development_Board/`

[View Schematic](./docs/SCH_STC89C52_Dev_Board.pdf)

Built by following a beginner-friendly tutorial series on Bilibili by [Expert电子实验室](https://www.bilibili.com/video/BV1At421h7Ui/). The series covers everything from reading datasheets and basic circuit theory to PCB layout and ordering from JLCPCB — great starting point for anyone new to hardware.

A dev board based on the STC89C52RC, a classic Chinese 8051-compatible microcontroller.

**Key Components:**
| Part | What it does |
|------|-------------|
| STC89C52RC-40I-LQFP44 | The main chip |
| AMS1117-3.3 | Converts input to 3.3V |
| TYPE-C 2.0 6PIN | USB port for power and flashing code |
| 12MHz Crystal | Clock source for the chip |
| Tactile switch 3×4mm | Reset button |

![STC89C52 Dev Board](./docs/images/STC89C52_Dev_Board_Preview.png)

---

### 2. Power Board with Voltage Converter
> `Power_Distribution_Board/Buck_Converter_PDB/`

[View Schematic](./docs/SCH_Buck_Converter_PDB.pdf)

A power distribution board that takes a high-voltage battery input and steps it down to 3.3V while also splitting it into multiple outputs for different modules.

**Key Components:**
| Part | What it does |
|------|-------------|
| LM2596SX-3.3 | Steps down voltage to 3.3V (max 3A output) |
| 68uH Inductor | Part of the step-down circuit |
| 1N5824 / 1N5825 | Diodes for circuit protection |
| 220uF + 470uF Caps | Smooth out the power supply |
| XT60-F | Battery connector input (handles high current) |
| XT30UW-F.G.Y (15A) | Waterproof power output |
| JST GH 1.25mm | Connector for smaller modules |
| KF301 5.0mm | Screw terminal for general wiring |

> **Safety:** Input voltage must be between 4.5V and 40V. The robot competition battery runs at 24V, which is within range.

**`Buck_Converter_PDB_Draft.eprj2`** is an early version made just to check if the board would fit inside the robot's frame — no converter circuit yet. I honestly forgot what I originally needed 3.3V for, but I picked the LM2596SX after some research, read the datasheet, and copied the sample circuit. Built with team budget while figuring things out as I went — looking back, the giant capacitors on the back were probably overkill for the actual load.

![Buck Converter PDB](./docs/images/Buck_Converter_PDB_Preview.png)

---

### 3. Robot Arm End Power Board
> `Power_Distribution_Board/Robot_Arm_End_PDB/`

[View Schematic](./docs/SCH_Robot_Arm_End_PDB.pdf)

A simple power distribution board that sits at the end of a robotic arm. No voltage conversion — it just splits the 24V input into multiple outputs. There's also a small PWM control circuit for an air pump mounted at the end-effector.

**Connectors:**
| Part | What it does |
|------|-------------|
| XT60-F | 24V power input |
| XT30UW-F.G.Y (15A) | Waterproof power output |
| JST GH 1.25mm | CAN bus signal in/out |
| KF301 Screw Terminal | PWM signal input for the air pump |

![Robot Arm End PDB](./docs/images/Robot_Arm_End_PDB_Preview.png)

---

## Notes

**File format:** `.eprj2` files are LCEDA Pro project files. Open them with [LCEDA Pro](https://lceda.cn/).

**Fabrication:** Export Gerber files from LCEDA and order directly from JLCPCB or similar services.

**Author:** Like CAI — [github.com/humble-learner006](https://github.com/humble-learner006) — learning the full robotics stack.

---

## License

[MIT License](./LICENSE)

Free to use, modify, and build upon. Credit appreciated but not required.

## Disclaimer

All designs in this repository are for     
learning and reference purposes only.      
No guarantees are made regarding their     
reliability or fitness for any particular  
use.
Use and manufacture at your own risk. 
