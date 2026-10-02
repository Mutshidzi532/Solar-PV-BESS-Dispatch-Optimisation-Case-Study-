# Solar-PV-BESS-Dispatch-Optimisation-Case-Study-
An hourly dispatch and optimisation model for a hybrid Solar PV and Battery Energy Storage System (BESS) built in Excel. Evaluates technical constraints, state of charge (SOC) dynamics, efficiency losses, network export limits, and solar curtailment.
# Solar PV + Battery Energy Storage System (BESS): Dispatch & Optimisation Case Study

**Prepared by:** Mutshidzi Madavha  
**Field:** Energy Systems / Renewable Energy  
**Tools:** Microsoft Excel  
**Focus:** Solar PV generation, battery storage, energy dispatch, curtailment, and grid export management  

---

## 1. Executive Summary
This case study examines the operation of a hybrid Solar PV and Battery Energy Storage System (BESS) supplying an electricity demand profile while operating within a defined grid export limit. 

The objective is to develop an hourly dispatch strategy that makes effective use of available solar generation, charges the battery when excess renewable energy is available, discharges the battery when demand exceeds solar generation, and limits electricity exported to the grid.

The model was developed in Microsoft Excel using an hourly energy balance and rule-based dispatch logic.

---

## 2. Problem Statement
Solar PV generation is variable throughout the day, whilst electricity demand may follow a completely different pattern. Without energy storage or appropriate dispatch controls, excess midday solar generation must be actively curtailed due to network grid export limitations. Conversely, during periods of low solar generation, expensive electricity must be imported from the utility grid to cover local consumer deficits.

---

## 3. Case Study Objective
The primary objective is to develop an hourly dispatch model that:
* Maximises the useful consumption of solar PV generation.
* Uses the BESS to shift renewable energy between periods.
* Maintains the battery within its permitted State of Charge (SOC) range.
* Respects the battery’s maximum charging and discharging power limits.
* Accounts for charging and discharging round-trip efficiencies.
* Limits electricity exported to the grid while reducing unnecessary grid imports.
* Identifies periods of active solar curtailment and provides key operational performance indicators (KPIs).

---

## 4. System Configuration & Parameters
The baseline hybrid network relies on the following structural design parameters:

| Parameter | Assumption |
| :--- | :--- |
| **Solar PV Capacity** | 100 MW |
| **BESS Energy Capacity** | 200 MWh |
| **Maximum BESS Charge Power** | 50 MW |
| **Maximum BESS Discharge Power** | 50 MW |
| **Minimum / Maximum SOC** | 20% / 100% (Initial: 50%) |
| **Round-Trip Efficiency (Charge / Discharge)**| 95% / 95% |
| **Maximum Grid Export Limit** | 40 MW |
| **Time Resolution** | 1 Hour (24-Hour Cycle) |

---

## 5. Dispatch Logic Steps
The spreadsheet engine resolves power routing rules sequentially every hour:
1. **Solar to Load:** `MIN(PV Generation, Load)`
2. **Identify Excess Energy:** `PV Generation - Load`
3. **BESS Charging:** Routes excess solar to storage up to a maximum threshold of 50 MW, accounting for a 95% efficiency drop until hitting 100% SOC.
4. **Grid Export:** Diverts remaining un-stored excess power to the grid up to a hard cap of 40 MW.
5. Curtailment:** If excess power remains, it is permanently clipped (curtailed).
6. BESS Discharging:** If solar falls short of the load, the battery fills the deficit up to 50 MW until draining to its 20% lower boundary.
7. Grid Import:** Any remaining unmet electricity demands are drawn from the utility grid.

---

## 6. Energy Balance Validation
To audit mathematical integrity across the operational horizon, every single hourly row checks out a net-zero physical equilibrium equation:

\[\text{PV} + \text{Grid Import} + \text{BESS Discharge} = \text{Load} + \text{BESS Charge} + \text{Grid Export} + \text{Curtailment}\]

---

## 7. Key Findings & Operational Trade-Offs
* Storage vs Curtailment:** Increasing battery capacity allows more excess solar generation to be stored, but battery capacity alone does not eliminate curtailment because charging power ratings and instantaneous SOC also impose hard constraints.
* Power vs Energy Capacity:** Increasing battery power capacity (MW) allows the system to absorb or release energy more quickly, while increasing energy capacity (MWh) allows the system to store energy for longer periods.
* Export Limits:
* A lower grid export limit directly inflates solar curtailment when the battery cannot absorb the additional generation.
  *SOC Management:** Maintaining a high SOC at midday increases the ability to reduce evening grid imports, but simultaneously reduces the battery’s available headroom to absorb sudden solar spikes.

---

## 8. Conclusion
The model proves that simply adding solar capacity yields diminishing returns without matching energy storage flexibility. Storage additions must balance power constraints with energy volume constraints. While larger batteries successfully curb generation losses and improve renewable integration fractions, technical efficiency overheads and diminishing optimisation returns require careful multi-scenario system balancing before full field deployment.
