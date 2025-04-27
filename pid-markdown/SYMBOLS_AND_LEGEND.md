# 📖 P&ID Symbols & Legend

This document defines the standard symbols and abbreviations for Piping and Instrumentation Diagram (P&ID) elements, following ISA-5.1, ISO 10628, and common industry practice. Use these as the canonical reference for all components in your P&ID Markdown files.

---

## Table of Contents

1. [Process & Utility Lines](#process--utility-lines)
2. [Valves](#valves)
3. [Piping Fittings](#piping-fittings)
4. [Instruments & Instrumentation Lines](#instruments--instrumentation-lines)
5. [Equipment](#equipment)
6. [Miscellaneous Symbols](#miscellaneous-symbols)
7. [Legend Example](#legend-example)

---

## Process & Utility Lines

| **Line Type**         | **Symbol**   | **Markdown**                  | **Description**                |
|-----------------------|--------------|-------------------------------|--------------------------------|
| Process Line          | ──────       | `[Piping: ...]`               | Main process flow              |
| Utility Line          | ══════       | `[Piping: ..., Service=Utility]` | Steam, air, water, etc.    |
| Instrument Signal     | - - - - -    | `[Instrument: ...] -.-> ...`  | Electric, pneumatic, etc.      |
| Future Line           | ⋅⋅⋅⋅⋅⋅⋅      | `[Piping: ..., Status=Future]`| Planned/future connection      |
| Underground Line      | ─ ─ ─ ─      | `[Piping: ..., Underground=Yes]` | Buried pipe                |
| Jacketed Line         | ──◯──        | `[Piping: ..., Jacketed=Yes]` | Pipe with heating/cooling jacket |

---

## Valves

| **Valve Type**            | **Symbol** | **Markdown**                              | **Description**                |
|---------------------------|------------|-------------------------------------------|--------------------------------|
| Gate Valve                | ─┬─        | `[Valve: Gate Valve, ...]`                | On/off isolation               |
| Globe Valve               | ─●─        | `[Valve: Globe Valve, ...]`               | Throttling/flow control        |
| Ball Valve                | ─◯─        | `[Valve: Ball Valve, ...]`                | Quick on/off                   |
| Butterfly Valve           | ─⊗─        | `[Valve: Butterfly Valve, ...]`           | Low-pressure on/off            |
| Check Valve               | ─▷─        | `[Valve: Check Valve, ...]`               | Prevents backflow              |
| Control Valve             | ⭘▲         | `[Valve: Control Valve, ...]`             | Automated flow control         |
| Pressure Relief Valve     | ─┴─        | `[Valve: PRV, ...]`                       | Overpressure protection        |
| Safety Valve              | ─┴┴─       | `[Valve: Safety Valve, ...]`              | Safety discharge               |
| Manual Valve              | ─┼─        | `[Valve: Manual Valve, ...]`              | General manual operation       |

---

## Piping Fittings

| **Fitting**              | **Symbol** | **Markdown**                              | **Description**                |
|--------------------------|------------|-------------------------------------------|--------------------------------|
| Elbow (90°)              | └─         | `[Fitting: Elbow, ...]`                   | 90-degree bend                 |
| Tee                      | ┬          | `[Fitting: Tee, ...]`                     | Three-way connection           |
| Reducer                  | >─         | `[Fitting: Reducer, ...]`                 | Size transition                |
| Flange                   | ║          | `[Fitting: Flange, ...]`                  | Flanged connection             |
| Blind Flange             | ║●         | `[Fitting: Blind Flange, ...]`            | End closure                    |
| Expansion Joint          | ≡          | `[Fitting: Expansion Joint, ...]`         | Thermal expansion              |
| Strainer                 | ≈          | `[Fitting: Strainer, ...]`                | Debris removal                 |
| Sight Glass              | ◊          | `[Fitting: Sight Glass, ...]`             | Visual inspection              |

---

## Instruments & Instrumentation Lines

| **Instrument**           | **Symbol** | **Markdown**                              | **Description**                |
|--------------------------|------------|-------------------------------------------|--------------------------------|
| Flow Transmitter         | ⭘FT        | `[Instrument: Flow Transmitter, ...]`     | Measures flow                  |
| Pressure Transmitter     | ⭘PT        | `[Instrument: Pressure Transmitter, ...]` | Measures pressure              |
| Temperature Transmitter  | ⭘TT        | `[Instrument: Temperature Transmitter, ...]` | Measures temperature      |
| Level Transmitter        | ⭘LT        | `[Instrument: Level Transmitter, ...]`    | Measures level                 |
| Analyzer                 | ⭘AT        | `[Instrument: Analyzer, ...]`             | Measures composition           |
| Controller               | ⬡FC        | `[Controller: Flow Controller, ...]`      | Control logic                  |
| Local Indicator          | ⭘FI        | `[Instrument: Local Indicator, ...]`      | Local display                  |
| Signal (Electric)        | - - -      | `[Instrument: ...] -.-> [Controller: ...]`| Electric signal                |
| Signal (Pneumatic)       | -.-.-      | `[Instrument: ...] -.-> [Valve: ...]`     | Pneumatic signal               |

---

## Equipment

| **Equipment**            | **Symbol** | **Markdown**                              | **Description**                |
|--------------------------|------------|-------------------------------------------|--------------------------------|
| Pump                     | ⭘→         | `[Equipment: Pump, ...]`                  | Fluid transfer                 |
| Vessel                   | ▭          | `[Equipment: Vessel, ...]`                | Storage/process vessel         |
| Column                   | ▯          | `[Equipment: Column, ...]`                | Distillation/absorption        |
| Heat Exchanger           | ▭≡▭        | `[Equipment: Heat Exchanger, ...]`        | Heat transfer                  |
| Reactor                  | ◯▭         | `[Equipment: Reactor, ...]`               | Chemical reaction              |
| Tank                     | ▭          | `[Equipment: Tank, ...]`                  | Storage tank                   |
| Compressor               | ◯→→        | `[Equipment: Compressor, ...]`            | Gas compression                |
| Fan/Blower               | ◯~         | `[Equipment: Fan, ...]`                   | Air/gas movement               |

---

## Miscellaneous Symbols

| **Item**                 | **Symbol** | **Markdown**                              | **Description**                |
|--------------------------|------------|-------------------------------------------|--------------------------------|
| Nozzle                   | ●          | `[Nozzle: N1, ...]`                       | Equipment connection           |
| Platform                 | ▬          | `[Platform: ...]`                         | Access platform                |
| Rupture Disc             | ◯          | `[Fitting: Rupture Disc, ...]`            | Overpressure protection        |
| Flame Arrestor           | ≡          | `[Fitting: Flame Arrestor, ...]`          | Explosion protection           |
| Sample Point             | ◯S         | `[Fitting: Sample Point, ...]`            | Sampling location              |
| Drain/vent               | ↓ / ↑      | `[Fitting: Drain, ...]` / `[Fitting: Vent, ...]` | Drain or vent           |

---

## Legend Example

You can include a legend section in your P&ID Markdown file as follows:

```markdown
## Symbols & Legends
- [Valve: Control Valve] = ⭘▲
- [Valve: Gate Valve] = ─┬─
- [Instrument: Flow Transmitter] = ⭘FT
- [Piping: Process Line] = ──────
- [Fitting: Flange] = ║
- [Equipment: Pump] = ⭘→
- [Nozzle] = ●
```

> For a full set of symbols, refer to the [ISA-5.1 standard](https://instrumentationtools.com/isa-5-1-instrumentation-symbols/) and your project's symbol library.

---

**Note:**  
- Always use the symbols and abbreviations defined here for consistency and clarity.
- If your project uses custom symbols, document them in this file or in a dedicated legend section of your P&ID Markdown.

## Instrumentation Symbols

| **Device/Function**         | **Symbol** | **Markdown**                                 | **Description**                        |
|-----------------------------|------------|----------------------------------------------|----------------------------------------|
| Control Valve (General)     | ⭘          | `[Valve: Control Valve, ...]`                | General control valve                  |
| Pneumatic Actuator          | ⭘→         | `[Actuator: Pneumatic, ...]`                 | Pneumatic actuator for valve           |
| Electric Actuator           | ⭘⚡         | `[Actuator: Electric, ...]`                  | Electric actuator for valve            |
| Hydraulic Actuator          | ⭘💧        | `[Actuator: Hydraulic, ...]`                 | Hydraulic actuator for valve           |
| Solenoid Valve              | ⭘S         | `[Valve: Solenoid Valve, ...]`               | Electrically actuated solenoid valve   |
| Self-Actuated Regulator     | ⭘R         | `[Valve: Regulator, ...]`                    | Self-regulating valve                  |
| Pressure Relief Valve       | ⭘PRV       | `[Valve: Pressure Relief Valve, ...]`        | Pressure relief/safety valve           |
| Vacuum Relief Valve         | ⭘VRV       | `[Valve: Vacuum Relief Valve, ...]`          | Vacuum relief valve                    |
| Flow Indicator              | ⭘FI        | `[Instrument: Flow Indicator, ...]`          | Local flow indicator                   |
| Level Indicator             | ⭘LI        | `[Instrument: Level Indicator, ...]`         | Local level indicator                  |
| Pressure Indicator          | ⭘PI        | `[Instrument: Pressure Indicator, ...]`      | Local pressure indicator               |
| Temperature Indicator       | ⭘TI        | `[Instrument: Temperature Indicator, ...]`   | Local temperature indicator            |
| Analyzer                    | ⭘A         | `[Instrument: Analyzer, ...]`                | Analytical instrument                  |
| Sample Connection           | ⭘S         | `[Fitting: Sample Point, ...]`               | Sample point                           |

---

## Interlock Logic Symbols

| **Logic Function**         | **Symbol** | **Markdown**                                 | **Description**                        |
|----------------------------|------------|----------------------------------------------|----------------------------------------|
| AND (All inputs must exist)| ◇          | `[Logic: AND, ...]`                          | All conditions must be true            |
| OR (Any input may exist)   | ◇∨         | `[Logic: OR, ...]`                           | Any condition may be true              |
| NOT (Input must not exist) | ◇¬         | `[Logic: NOT, ...]`                          | Condition must not be true             |
| Exclusive (Only one input) | ◇X         | `[Logic: EXCLUSIVE, ...]`                    | Only one input may be true             |
| Output Exists if All Inputs| ◇→         | `[Logic: OUTPUT_IF_ALL, ...]`                | Output if all inputs exist             |
| Output Exists if Any Input | ◇→∨        | `[Logic: OUTPUT_IF_ANY, ...]`                | Output if any input exists             |

---

## Function Block Symbols

| **Function**               | **Symbol** | **Markdown**                                 | **Description**                        |
|----------------------------|------------|----------------------------------------------|----------------------------------------|
| Summing                    | ∑          | `[Function: Sum, ...]`                       | Summing block                          |
| Averaging                  | ⌀          | `[Function: Average, ...]`                   | Averaging block                        |
| Proportional               | P          | `[Function: Proportional, ...]`              | Proportional function                  |
| Integral                   | I          | `[Function: Integral, ...]`                  | Integral function                      |
| Derivative                 | D          | `[Function: Derivative, ...]`                | Derivative function                    |
| High/Low Select            | H/L        | `[Function: HighSelect, ...]` / `[Function: LowSelect, ...]` | High/low select block   |
| Alarm                      | 🔔         | `[Alarm: ...]`                               | Alarm function                         |
| Manual/Auto                | M/A        | `[Function: ManualAuto, ...]`                | Manual/auto selector                   |

---

## Instrument Identification Letters (ISA-5.1)

| **First Letter** | **Measured/Indicating Variable** |
|------------------|----------------------------------|
| A                | Analysis                         |
| B                | Burner, Combustion               |
| C                | Control                          |
| D                | Density or Consistency           |
| E                | Voltage                          |
| F                | Flow                             |
| H                | Hand (Manual)                    |
| I                | Current                          |
| J                | Power                            |
| K                | Time, Schedule                   |
| L                | Level                            |
| M                | Moisture, Humidity               |
| N                | User's Choice                    |
| O                | User's Choice                    |
| P                | Pressure                         |
| Q                | Quantity                         |
| R                | Radiation                        |
| S                | Speed, Frequency                 |
| T                | Temperature                      |
| U                | Multivariable                    |
| V                | Vibration, Mechanical Analysis   |
| W                | Weight, Force                    |
| X, Y, Z          | Auxiliary, Special               |

**Succeeding Letters** (examples: T = Transmitter, I = Indicator, C = Controller, S = Switch, etc.)

---

## Typical Letter Combinations

| **Tag** | **Meaning**                  |
|---------|-----------------------------|
| FT      | Flow Transmitter            |
| FC      | Flow Controller             |
| FIC     | Flow Indicating Controller  |
| FV      | Flow Control Valve          |
| PT      | Pressure Transmitter        |
| PIC     | Pressure Indicating Controller |
| PV      | Pressure Control Valve      |
| TT      | Temperature Transmitter     |
| TIC     | Temperature Indicating Controller |
| TV      | Temperature Control Valve   |
| LT      | Level Transmitter           |
| LIC     | Level Indicating Controller |
| LV      | Level Control Valve         |
| ...     | ...                         |

> For a full list, see the [ISA-5.1 standard](https://instrumentationtools.com/isa-5-1-instrumentation-symbols/) or your project documentation.

---

## Special Abbreviations

| **Abbreviation** | **Meaning**                  |
|------------------|-----------------------------|
| FC              | Fail Closed                  |
| FO              | Fail Open                    |
| FL              | Fail Locked                  |
| LL              | Low-Low (alarm/setpoint)     |
| HH              | High-High (alarm/setpoint)   |
| SH              | Shutdown                     |
| SO              | Solenoid Operated            |
| AO              | Air Operated                 |
| MO              | Motor Operated               |
| ...             | ...                          |

---

**Note:**  
- Always use the symbols, function blocks, and tag conventions defined here for consistency and clarity.
- If your project uses custom logic or tag conventions, document them in this file or in a dedicated legend section of your P&ID Markdown. 