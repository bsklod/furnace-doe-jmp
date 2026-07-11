# Furnace Oxide Growth Process — DOE & Variance Components Analysis (JMP)
 
## Overview
This project analyzes a semiconductor furnace oxide growth process using a publicly available NIST/SEMATECH dataset. The goal was to determine whether the process is capable of consistently meeting spec, and to identify the dominant sources of variation to inform a process control strategy using JMP's Design of Experiments (DOE) and variance components tools.
 
This dataset models a real semiconductor furnace oxide growth process, selected to build DOE/JMP proficiency directly applicable to fab process engineering roles.
 
## Background
In this semiconductor process step, a cassette of silicon wafers is loaded into a quartz "boat," and boats are placed into one of four zones within a furnace tube. A gas flow is introduced and the furnace is brought to temperature to grow an oxide film of a target thickness on each wafer.
 
- **Structure:** 21 production runs × 4 furnace zones × 2 wafers per zone × 2 measurement sites = 168 observations
- **Response variable:** Oxide film thickness (Angstroms)
- **Specification:** 560 Å target, ±100 Å (LSL 460 / USL 660)
## Objective
1. Determine if the furnace process is capable of consistently producing oxide film within specification.
2. Decompose total thickness variation into its component sources (run-to-run, zone-to-zone, wafer-to-wafer) to identify where process control efforts should be focused.
## Method
- **Software:** JMP Pro (Student Edition)
- **Process capability analysis:** Distribution platform with spec limits (LSL 460, Target 560, USL 660) to calculate Cpk/Ppk
- **Variance components analysis:** Nested random-effects model (REML) via Fit Model, with the hierarchy:
  - `RUN` (random)
  - `ZONE[RUN]` (random, nested)
  - `WAFER[RUN, ZONE]` (random, nested)
- **Supporting visualization:** Variability/Gauge Chart to visually inspect within-zone and within-run scatter
## Key Findings
 
**Process Capability**
| Metric | Value |
|---|---|
| Sample Mean | 563.04 Å |
| Cpk | 1.95 |
| Cp | 2.01 |
| Observed nonconformance | 0.0% (0 of 168 observations out of spec) |
 
The process is currently well within specification, with a Cpk of 1.95.
 
**Variance Decomposition**
| Source | % of Total Variation |
|---|---|
| Run-to-run | 47.4% |
| Zone-to-zone (within run) | 34.2% |
| Wafer-to-wafer (within zone) | 18.4% |
 
Run-to-run variation is the single largest contributor to total thickness variability; nearly half of all observed variation originates between production runs, exceeding the combined contribution of furnace zone position and wafer-level differences.
 
## Conclusion
Since run-to-run variation is the dominant variance source, process control efforts should prioritize investigating inputs that change between runs - incoming wafer lot variation, consumable/gas quality, and furnace conditioning between runs - rather than focusing primarily on furnace zone temperature offset calibration, which accounts for a smaller share of variation.
 
## Visuals
- Distribution and process capability output   <img width="742" height="1284" alt="FURNACE - Distribution of THICKNESS" src="https://github.com/user-attachments/assets/d9db4d25-3d32-446c-9b89-0513c7e67ef7" />

- Variability/Gauge chart by run and zone  <img width="1137" height="631" alt="FURNACE - Variability Chart of THICKNESS" src="https://github.com/user-attachments/assets/de070735-89ba-42f9-bb34-6d43779681b3" />  
- REML variance components table                                         
  <img width="631" height="352" alt="FURNACE - Fit Least Squares" src="https://github.com/user-attachments/assets/83082ff5-594f-40c1-bccd-6457247c678d" />

## Tools Used
- JMP Pro (Student Edition)
- REML variance components estimation
- Process capability analysis (Cpk/Ppk)
## Data Source
NIST/SEMATECH e-Handbook of Statistical Methods, Production Process Characterization Case Studies:
https://www.itl.nist.gov/div898/handbook/ppc/section5/ppc51.htm
