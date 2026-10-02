# DA-PCS

This repository contains the tool and benchmark models used in the DA-PCS paper.
The tool is an extension of MTSA (Modal Transition System Analyser), and the models are written in the MTSA `.lts` format.

## Repository layout

```
.
├── target/
│   └── mtsa-1.0-SNAPSHOT.jar   # MTSA extended with DA-PCS
└── model/
    ├── DC(2,K).lts             # Drone Control,     2 drones
    ├── DC(3,K).lts             # Drone Control,     3 drones
    ├── DC(4,K).lts             # Drone Control,     4 drones
    ├── HC（2,K）.lts            # Human Control, Hall + Room A
    ├── HC（3,K）.lts            # Human Control, Hall + Rooms A, B
    └── HC（4,K）.lts            # Human Control, Hall + Rooms A, B, C
```

## Requirements

- Java (JRE) to run the jar
- Enough main memory for the larger models. The command below allocates 20 GB of heap; change `-Xmx20G` to suit your machine.

## Running the tool

From the repository root:

```bash
java -jar -Xmx20G ./target/mtsa-1.0-SNAPSHOT.jar
```

This launches the MTSA GUI. Open one of the `.lts` files under `model/`, then use the toolbar buttons to choose the synthesis method:

| Button | Method                                  |
|--------|-----------------------------------------|
| **1**  | DA-PCS (proposed)                       |
| **3**  | Exhaustive PCS (baseline)               |

## Models

Each model file name has the form `XX(n,K)`, where `n` is fixed by the file and `K` is the size parameter varied in the paper's evaluation.

### DC: Drone Control

`n` is the number of drones (`const N`). To change the model size `K`, edit the following constants in each DC file:

| Constant  | Location in file | Meaning                                      |
|-----------|------------------|----------------------------------------------|
| `MaxX`    | Environment      | Width of the grid (x-axis), minimum 2        |
| `MaxY`    | Environment      | Depth of the grid (y-axis), minimum 2        |
| `LIMIT_X` | Requirement      | x-coordinate the drones must not enter       |
| `LIMIT_Y` | Requirement      | y-coordinate the drones must not enter       |

Do **not** change `S` or `MaxH` (the maximum height). The collision requirements `P_NO_COLLISON_*` are written out for heights 1 and 2 only, so a different height no longer matches the paper's setting.

### HC: Headcount Control

`n` is the number of areas (the hall plus rooms A, B, ...). To change `K` in the paper, edit `N` at the top of each HC file:

```
const N = 6
```

`N` is the maximum number of visitors counted in each area.
