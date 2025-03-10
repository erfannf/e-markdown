# 📄 PFD Markdown Specification Rev.0

Welcome to the **PFD Markdown Specification** repository! This project defines a **markdown-based syntax** for creating **Process Flow Diagrams (PFDs)** that are both human-readable and machine-interpretable. 

> **Note:** This is **Revision 0**, representing the initial formalization of the specification. As an emerging standard, it is subject to community feedback and iterative improvement.

The syntax is designed to be intuitive, scalable, and compatible with tools like **Mermaid** for visualization. This README provides a comprehensive guide to the specification, including syntax rules, examples, and best practices.

---

## 📌 Table of Contents
1. [Introduction](#-introduction)
2. [Syntax Overview](#-syntax-overview)
3. [Core Components](#-core-components)
   - [Equipment](#-equipment)
   - [Streams](#-streams)
   - [Instruments](#-instruments)
   - [Valves](#-valves)
   - [Data Connections](#-data-connections)
4. [Grid System](#-grid-system)
5. [Symbols & Legends](#-symbols--legends)
6. [Examples](#-examples)
7. [Best Practices](#-best-practices)
8. [Contributing](#-contributing)
9. [License](#-license)

---

## 🌟 Introduction

Process Flow Diagrams (PFDs) are essential for visualizing and documenting industrial processes across chemical, petrochemical, pharmaceutical, and other process industries. This specification introduces a **markdown-based syntax** for creating standardized PFDs that can be:
- **Human-readable**: Easily understood and edited by engineers without specialized software.
- **Machine-interpretable**: Parsable by Large Language Models (LLMs), visualization tools, and simulation software.
- **Scalable**: Capable of representing both simple unit operations and complex integrated processes.
- **Version-controllable**: Compatible with standard version control systems like Git.

The syntax is aligned with industry standards including **ISO 10628** (flow diagrams for process plants), **ANSI/ISA-5.1** (instrumentation symbols and identification), and **DIN 28004** (flow sheet symbols), ensuring compatibility with established engineering practices.

---

## 📖 Syntax Overview

The PFD markdown syntax follows a hierarchical structure with clearly defined sections, each representing a fundamental component of the process diagram:

- **Limits**: Battery limits defining incoming and outgoing points where streams enter or exit the current PFD sheet, including source/destination references and descriptions
- **Equipment**: Process vessels, reactors, columns, heat exchangers, pumps, and other physical apparatus.
- **Streams**: Material flows with associated properties (flow rate, temperature, pressure, composition).
- **Instruments**: Measurement devices, sensors, transmitters, and analytical equipment.
- **Valves**: Flow control, pressure regulation, and isolation devices.
- **Data Connections**: Signal pathways between instruments, controllers, and final control elements.

Each component is defined using a standardized **key-value pair** structure within square brackets, with nested attributes denoted by indentation or sub-lists. This structure ensures both human readability and machine parseability.

---

## 🧩 Core Components

### 🚧 Limits
Limits represent the battery boundaries of the process flow diagram, defining where streams enter or exit the current PFD sheet. They are essential for connecting multiple PFDs together in a larger process system and are defined using the syntax `[Incoming: <ID>]` or `[Outgoing: <ID>]`.

#### Formal Syntax:
```markdown
## Limits
### Incoming Points
- [Incoming: <ID>, Unit=<UnitNumber>, PFD=<PFDNumber>, Location=<GridCoordinate>]
  - Stream: [Stream: <ID>, <Properties>]
  - Connects To: [<DestinationType>: <DestinationID>, <EquipmentType>: <EquipmentID>]
  - Description: "<Text describing the source of this stream>"

### Outgoing Points
- [Outgoing: <ID>, Unit=<UnitNumber>, PFD=<PFDNumber>, Location=<GridCoordinate>]
  - Stream: [Stream: <ID>, <Properties>]
  - Connects From: [<SourceType>: <SourceID>, <EquipmentType>: <EquipmentID>]
  - Description: "<Text describing the destination of this stream>"
```

#### Example:
```markdown
## Limits
### Incoming Points
- [Incoming: IN-501, Unit=501, PFD=501, Location=G1, Description="Feed from Storage Area"]
  - Stream: [Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar, Composition="H2O=90%, NaCl=10%"]
  - Connects To: [Nozzle: N1, Distillation Tower: T-101]

### Outgoing Points
- [Outgoing: OUT-503, Unit=503, PFD=503, Location=G9, Description="Product to Packaging"]
  - Stream: [Stream: 7, Flow=40 m³/h, T=35°C, P=1.5 bar, Composition="H2O=95%, NaCl=5%"]
  - Connects From: [Nozzle: N4, Distillation Tower: T-101]
```

---

### 🏭 Equipment
Equipment elements represent the physical processing units within the system and are defined using the syntax `[Equipment: <Type>, <ID>, <Attributes>]`. Equipment definitions may include physical specifications, operating parameters, and spatial coordinates.

#### Formal Syntax:
```markdown
[Equipment: <Type>, <ID>, Height=<Value> <Unit>, Diameter=<Value> <Unit>, Material="<Material>", Design_Pressure=<Value> <Unit>, Location=<GridCoordinate>]
- [Nozzle: <ID>, Location=<Position>, Grid=<GridCoordinate>, Size=<Value>, Service="<Description>"]
- [Nozzle: <ID>, Location=<Position>, Grid=<GridCoordinate>, Size=<Value>, Service="<Description>"]
...
```

#### Example:
```markdown
[Equipment: Distillation Tower, T-101, Height=30m, Diameter=2m, Material="316L SS", Design_Pressure=10 bar, Location=C5]
- [Nozzle: N1, Location=Top, Grid=C5-T, Size=6", Service="Feed Inlet"]
- [Nozzle: N2, Location=Middle, Grid=C5-M, Size=4", Service="Side Draw"]
- [Nozzle: N3, Location=Bottom, Grid=C5-B, Size=8", Service="Bottoms Outlet"]
```

---

### 🌊 Streams
Streams represent material flows between equipment and are defined using the syntax `[Stream: <ID>, <Properties>]`. Stream definitions include physical properties, flow characteristics, and routing information.

#### Formal Syntax:
```markdown
[Stream: <ID>, Flow=<Value> <Unit>, T=<Value> <Unit>, P=<Value> <Unit>, Phase="<Phase>", Composition="<Components>", Path=<StartGrid> -> <EndGrid>]
- From: [<SourceType>: <SourceID>]
- To: [<DestinationType>: <DestinationID>]
- Tap: [<TapID>, Grid=<GridCoordinate>]
  - [<ComponentType>: <ComponentID>, Grid=<GridCoordinate>]
```

#### Example:
```markdown
[Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar, Phase="Liquid", Composition="H2O=90%, NaCl=10%", Path=G1 -> C5-T]
- From: [Incoming: IN-501]
- To: [Nozzle: N1, Distillation Tower: T-101]
- Tap: [TP1, Grid=C5-T]
  - [Valve: Control Valve, CV-101, Grid=C5-T]
```

---

### 🎛️ Instruments
Instruments represent measurement, control, and analytical devices within the process system and are defined using the syntax `[Instrument: <Type>, <ID>, <Attributes>]`. Instrument definitions include measurement specifications, signal types, and placement information.

#### Formal Syntax:
```markdown
[Instrument: <Type>, <ID>, Range=<Min>-<Max> <Unit>, Unit=<Unit>, Accuracy=<Value>, Response_Time=<Value>, Grid=<GridCoordinate>]
- Placement: [<PlacementType>: <PlacementID>, <EquipmentType>: <EquipmentID>]
- Signal: [<SignalType>, <Protocol>]
```

#### Example:
```markdown
[Instrument: Temperature Sensor, TT-101, Range=0-200°C, Unit=°C, Accuracy=±0.5°C, Response_Time=5s, Grid=C5-T]
- Placement: [Nozzle: N1, Distillation Tower: T-101]
- Signal: [4-20mA, HART Protocol]
```

---

### 🚪 Valves
Valves represent flow control, isolation, and pressure regulation devices within the process system and are defined using the syntax `[Valve: <Type>, <ID>, <Attributes>]`. Valve definitions include physical specifications, materials of construction, and operational parameters.

#### Formal Syntax:
```markdown
[Valve: <Type>, <ID>, Size=<Value>, Material="<Material>", Body_Type="<Type>", Trim="<TrimType>", Cv=<Value>, Status=<Status>, Fail_Position="<Position>", Grid=<GridCoordinate>]
- Connection: [Stream: <StreamID>, Tap: <TapID>]
- Actuator: [<ActuatorType>, <ActuatorID>]
```

#### Example:
```markdown
[Valve: Control Valve, CV-101, Size=2", Material="316 Stainless Steel", Body_Type="Globe", Trim="Equal Percentage", Cv=45, Status=Open, Fail_Position="Closed", Grid=C5-T]
- Connection: [Stream: 1, Tap: TP1]
- Actuator: [Pneumatic, ACT-101, Air_Supply=3-15 psi]
```

---

### 🔗 Data Connections
Data connections represent signal pathways between instruments, controllers, and final control elements in control loops and are defined using the `-.->` syntax. These connections illustrate the flow of information and control signals throughout the process system.

#### Formal Syntax:
```markdown
[<SourceType>: <SourceID>, Grid=<GridCoordinate>] -.-> [<DestinationType>: <DestinationID>, Grid=<GridCoordinate>]
- Signal_Type: [<Type>, <Protocol>]
- Priority: [<Level>]
```

#### Example:
```markdown
[Instrument: Flow Meter, FT-101, Grid=C5-T] -.-> [Controller: FC-101, Grid=C5-T]
- Signal_Type: [Digital, Foundation Fieldbus]
- Priority: [High]

[Controller: FC-101, Grid=C5-T] -.-> [Valve: Control Valve, CV-101, Grid=C5-T]
- Signal_Type: [4-20mA, HART]
- Priority: [High]
```

#### Control Loop Example:
```markdown
# Temperature Control Loop for Distillation Column
[Instrument: Temperature Sensor, TT-101, Grid=C5-T] -.-> [Controller: TC-101, Grid=C5-T]
[Controller: TC-101, Grid=C5-T] -.-> [Valve: Control Valve, CV-101, Grid=C5-T]
```

---

### 🔀 Stream Intersections
Stream intersections represent points where multiple streams merge together or a single stream splits into multiple streams. These are critical elements in process flow diagrams and are defined using the `[Intersection: <ID>, <Attributes>]` syntax.

#### Formal Syntax:
```markdown
[Intersection: <ID>, Grid=<GridCoordinate>, Type="<MergeOrSplit>"]
- Incoming: [Stream: <ID1>] (for merge: multiple streams, for split: single stream)
- Outgoing: [Stream: <ID2>, Stream: <ID3>, ...] (for merge: single stream, for split: multiple streams)
```

#### Merge Example:
```markdown
# Two streams merging into one
[Intersection: X-1, Grid=E7, Type="Merge"]
- Incoming: [Stream: 2, Stream: 3]
- Outgoing: [Stream: 4]
```

#### Split Example:
```markdown
# One stream splitting into two
[Intersection: X-2, Grid=C5, Type="Split"]
- Incoming: [Stream: 5]
- Outgoing: [Stream: 6, Stream: 7]
```

#### Complex Example:
```markdown
# Multiple stream intersection with flow distribution
[Intersection: X-3, Grid=G5, Type="Distribution"]
- Incoming: [Stream: 8, Stream: 9]
- Outgoing: [Stream: 10, Stream: 11, Stream: 12]
- Distribution: [Stream: 8 -> Stream: 10 (70%), Stream: 11 (30%)]
- Distribution: [Stream: 9 -> Stream: 12 (100%)]
```

Stream intersections can be represented visually using diamond symbols (◇) on the diagram, with connecting lines showing the flow direction between incoming and outgoing streams.

---

## 🗺️ Grid System

A **virtual grid system** is used to specify the location of items on the PFD. The grid uses letters (columns) and numbers (rows), e.g., `G1` (Column G, Row 1). Nozzles on equipment are assigned specific grid locations, e.g., `C5-T` (Top nozzle at Column C, Row 5).

#### Example:
```markdown
[Equipment: Distillation Tower, T-101, Location=C5]
- [Nozzle: N1, Location=Top, Grid=C5-T]
- [Nozzle: N2, Location=Middle, Grid=C5-M]
- [Nozzle: N3, Location=Bottom, Grid=C5-B]
```

---

## 🎨 Symbols & Legends

The specification defines standardized symbols for representing components in visualizations, aligned with industry conventions and international standards. These symbols ensure consistent interpretation across different visualization platforms and by different stakeholders.

### Standard Symbols

| **Component**       | **Symbol**       | **Visual Representation** | **Markdown Representation**                     | **Industry Standard** |
|----------------------|------------------|--------------------------|------------------------------------------------|----------------------|
| Equipment - Vessel   | Rectangle        | ┌─────┐<br>│     │<br>└─────┘ | `[Equipment: Vessel, V-101]`                   | ISO 10628 |
| Equipment - Column   | Tall Rectangle   | ┌───┐<br>│   │<br>│   │<br>│   │<br>└───┘ | `[Equipment: Distillation Tower, T-101]`       | ISO 10628 |
| Equipment - Pump     | Circle with Arrow | ⭘→ | `[Equipment: Pump, P-101]`                    | ISO 10628 |
| Equipment - Heat Exchanger | Rectangle with Lines | ┌─┬─┬─┐<br>│ │ │ │<br>└─┴─┴─┘ | `[Equipment: Heat Exchanger, HX-101]` | ISO 10628 |
| Equipment - Reactor  | Rectangle with Rounded Corners | ╭─────╮<br>│     │<br>╰─────╯ | `[Equipment: Reactor, R-101]`    | ISO 10628 |
| Instrument - Sensor  | Circle with Text | ⭘TT | `[Instrument: Temperature Sensor, TT-101]`     | ANSI/ISA-5.1 |
| Instrument - Controller | Hexagon       | ⬡TC | `[Controller: Temperature Controller, TC-101]` | ANSI/ISA-5.1 |
| Valve - Control      | Triangle in Circle | ⭘▲ | `[Valve: Control Valve, CV-101]`             | ANSI/ISA-5.1 |
| Valve - Manual       | Gate Symbol      | ─┼─ | `[Valve: Manual Valve, MV-101]`                | ANSI/ISA-5.1 |
| Process Stream       | Solid Line       | ───────→ | `[Stream: 1, Flow=100 m³/h]`                   | ISO 10628 |
| Signal Connection    | Dashed Line      | ─ ─ ─ ─→ | `[Instrument: TT-101] -.-> [Controller: TC-101]` | ANSI/ISA-5.1 |
| Intersection         | Diamond          | ◇ | `[Intersection: X-1, Grid=E7]`                 | ISO 10628 |
| Battery Limit        | Vertical Line    | ║ | `[Incoming: IN-501]` or `[Outgoing: OUT-501]`  | ISO 10628 |

### Instrument Identification

Instruments follow the ANSI/ISA-5.1 identification system:

| **First Letter** | **Measured Variable** | **Example** |
|------------------|------------------------|-------------|
| T                | Temperature            | TT-101 (Temperature Transmitter) |
| P                | Pressure               | PT-101 (Pressure Transmitter) |
| F                | Flow                   | FT-101 (Flow Transmitter) |
| L                | Level                  | LT-101 (Level Transmitter) |
| A                | Analysis               | AT-101 (Analytical Transmitter) |

| **Second Letter** | **Function**          | **Example** |
|-------------------|------------------------|-------------|
| T                 | Transmitter            | TT-101 (Temperature Transmitter) |
| I                 | Indicator              | TI-101 (Temperature Indicator) |
| C                 | Controller             | TC-101 (Temperature Controller) |
| S                 | Switch                 | TS-101 (Temperature Switch) |
| E                 | Element (Sensor)       | TE-101 (Temperature Element) |

### Line Types

| **Line Type**    | **Visual Representation** | **Usage**                                     |
|------------------|--------------------------|-----------------------------------------------|
| Solid Line       | ───────                | Process Streams (material flow)               |
| Dashed Line      | ─ ─ ─ ─                | Signal Connections (information flow)         |
| Double Line      | ═══════                | Steam or Utility Lines                        |
| Dotted Line      | ⋅⋅⋅⋅⋅⋅⋅                | Future or Proposed Connections                |

### Color Coding (Optional)

| **Color**        | **Usage**              | **Example**                                  |
|------------------|------------------------|----------------------------------------------|
| Green            | Normal Operation       | `[Stream: 1, Color=Green]`                   |
| Red              | High Temperature/Pressure | `[Stream: 2, Color=Red]`                  |
| Blue             | Cooling Water          | `[Stream: 3, Color=Blue]`                    |
| Yellow           | Warning/Caution        | `[Instrument: PT-101, Status=Alarm, Color=Yellow]` |
| Purple           | Chemical/Hazardous     | `[Stream: 4, Content="H2SO4", Color=Purple]` |

---

## 📚 Examples

### Simple PFD Example
```markdown
# FCC Unit 502
[PFD Number: 502, Revision: 1.0, Date: 2023-10-15]

## Limits
### Incoming Points
- [Incoming: IN-501, Unit=501, PFD=501, Location=G1]
  - Stream: [Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar]
  - Connects To: [Nozzle: N1, Distillation Tower: T-101]

## Equipment
[Equipment: Distillation Tower, T-101, Height=30m, Diameter=2m, Location=C5]
- [Nozzle: N1, Location=Top, Grid=C5-T]
- [Nozzle: N2, Location=Middle, Grid=C5-M]
- [Nozzle: N3, Location=Bottom, Grid=C5-B]

## Streams
[Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar, Path=G1 -> C5-T]
- From: [Incoming: IN-501]
- To: [Nozzle: N1, Distillation Tower: T-101]
- Tap: [TP1, Grid=C5-T]
  - [Valve: Control Valve, CV-101, Grid=C5-T]

## Instruments
[Instrument: Temperature Sensor, TT-101, Range=0-200°C, Unit=°C, Grid=C5-T]
- Placement: [Nozzle: N1, Distillation Tower: T-101]

## Data Connections
[Instrument: Flow Meter, FT-101] -.-> [Controller: FC-101]
[Controller: FC-101] -.-> [Valve: Control Valve, CV-101]
```

### Complex PFD Example
This is a more complex example that shows how to connect multiple instruments and valves to a single stream. Covers intersections of multiple streams, multiple instruments, and multiple valves. Also shows metadata of virtual mesh item placed on the grid.

```
# FCC Unit 502
[PFD Number: 502, Revision: 1.0, Date: 2023-10-15]

## Limits
### Incoming Points
- [Incoming: IN-501, Unit=501, PFD=501, Location=G1]
  - Stream: [Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar]
  - Connects To: [Nozzle: N1, Distillation Tower: T-101]

### Outgoing Points
- [Outgoing: OUT-503, Unit=503, PFD=503, Location=G9]
  - Stream: [Stream: 7, Flow=40 m³/h, T=35°C, P=1.5 bar]
  - Connects From: [Nozzle: N4, Distillation Tower: T-101]

## Equipment
### Distillation Tower
[Equipment: Distillation Tower, T-101, Height=30m, Diameter=2m, Location=C5]
- [Nozzle: N1, Location=Top, Grid=C5-T]
- [Nozzle: N2, Location=Middle, Grid=C5-M]
- [Nozzle: N3, Location=Bottom, Grid=C5-B]
- [Nozzle: N4, Location=Side, Grid=C5-S]

### Pump
[Equipment: Pump, P-101, Power=5kW, Location=C9]

### Heat Exchanger
[Equipment: Heat Exchanger, HX-101, Type=Shell and Tube, Location=E7]

### Tank
[Equipment: Tank, T-102, Capacity=1500L, Location=G5]

[Equipment: Tank, T-103, Capacity=1000L, Location=G7]

## Streams
### Stream 1 (Incoming from Unit 501)
[Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar, Path=G1 -> C5-T]
- From: [Incoming: IN-501]
- To: [Nozzle: N1, Distillation Tower: T-101]
- Tap: [TP1, Grid=C5-T]
  - [Valve: Control Valve, CV-101, Grid=C5-T]

### Stream 2
[Stream: 2, Flow=70 m³/h, T=55°C, P=2 bar, Path=C5-M -> E7]
- From: [Pump: P-101]
- To: [Heat Exchanger: HX-101]
- Tap: [TP2, Grid=E7]
  - [Valve: Control Valve, CV-102, Grid=E7]

### Stream 3
[Stream: 3, Flow=30 m³/h, T=30°C, P=1.5 bar, Path=E7 -> G5]
- From: [Heat Exchanger: HX-101]
- To: [Tank: T-102]
- Tap: [TP3, Grid=G5]
  - [Valve: Control Valve, CV-103, Grid=G5]

### Stream 4 (Split from Stream 2)
[Stream: 4, Flow=20 m³/h, T=55°C, P=2 bar, Path=E7 -> G7]
- From: [Intersection: X-1, Grid=E7]
- To: [Tank: T-103]
- Tap: [TP4, Grid=G7]
  - [Valve: Control Valve, CV-104, Grid=G7]

### Stream 5 (Merge into Stream 3)
[Stream: 5, Flow=10 m³/h, T=40°C, P=1.5 bar, Path=G7 -> G5]
- From: [Tank: T-103]
- To: [Intersection: X-2, Grid=G5]
- Tap: [TP5, Grid=G5]
  - [Valve: Control Valve, CV-105, Grid=G5]

### Stream 6 (Bottom Stream from T-101)
[Stream: 6, Flow=50 m³/h, T=60°C, P=1.5 bar, Path=C5-B -> G5]
- From: [Nozzle: N3, Distillation Tower: T-101]
- To: [Tank: T-102]
- Tap: [TP6, Grid=G5]
  - [Valve: Control Valve, CV-106, Grid=G5]

### Stream 7 (Outgoing to Unit 503)
[Stream: 7, Flow=40 m³/h, T=35°C, P=1.5 bar, Path=C5-S -> G9]
- From: [Nozzle: N4, Distillation Tower: T-101]
- To: [Outgoing: OUT-503]

### Intersections
- [Intersection: X-1, Grid=E7]
  - Incoming: [Stream: 2]
  - Outgoing: [Stream: 3, Stream: 4]
- [Intersection: X-2, Grid=G5]
  - Incoming: [Stream: 3, Stream: 5]
  - Outgoing: [Stream: 6]

## Instruments
### Flow Meters
[Instrument: Flow Meter, FT-101, Range=0-200 m³/h, Unit=m³/h, Grid=C5-T]
- Placement: [Tap: TP1, Stream: 1]

[Instrument: Flow Meter, FT-102, Range=0-50 m³/h, Unit=m³/h, Grid=G7]
- Placement: [Tap: TP4, Stream: 4]

### Temperature Sensors
[Instrument: Temperature Sensor, TT-101, Range=0-200°C, Unit=°C, Grid=E7]
- Placement: [Tap: TP2, Stream: 2]

[Instrument: Temperature Sensor, TT-102, Range=0-100°C, Unit=°C, Grid=G5]
- Placement: [Tap: TP5, Stream: 5]

[Instrument: Temperature Sensor, TT-103, Range=0-200°C, Unit=°C, Grid=C5-T]
- Placement: [Nozzle: N1, Distillation Tower: T-101]

[Instrument: Temperature Sensor, TT-104, Range=0-200°C, Unit=°C, Grid=C5-M]
- Placement: [Nozzle: N2, Distillation Tower: T-101]

### Pressure Sensors
[Instrument: Pressure Sensor, PT-101, Range=0-10 bar, Unit=bar, Grid=G5]
- Placement: [Tap: TP3, Stream: 3]

### Level Sensors
[Instrument: Level Sensor, LT-101, Range=0-100%, Unit=%, Grid=C5-B]
- Placement: [Nozzle: N3, Distillation Tower: T-101]

## Data Connections
### Flow Control Loop
[Instrument: Flow Meter, FT-101, Grid=C5-T] -.-> [Controller: FC-101, Grid=C5-T]
[Controller: FC-101] -.-> [Valve: Control Valve, CV-101, Grid=C5-T]

[Instrument: Flow Meter, FT-102, Grid=G7] -.-> [Controller: FC-102, Grid=G7]
[Controller: FC-102] -.-> [Valve: Control Valve, CV-104, Grid=G7]

### Temperature Control Loop
[Instrument: Temperature Sensor, TT-101, Grid=E7] -.-> [Controller: TC-101, Grid=E7]
[Controller: TC-101] -.-> [Valve: Control Valve, CV-102, Grid=E7]

[Instrument: Temperature Sensor, TT-102, Grid=G5] -.-> [Controller: TC-102, Grid=G5]
[Controller: TC-102] -.-> [Valve: Control Valve, CV-105, Grid=G5]

[Instrument: Temperature Sensor, TT-103, Grid=C5-T] -.-> [Controller: TC-103, Grid=C5-T]
[Instrument: Temperature Sensor, TT-104, Grid=C5-M] -.-> [Controller: TC-104, Grid=C5-M]

### Pressure Control Loop
[Instrument: Pressure Sensor, PT-101, Grid=G5] -.-> [Controller: PC-101, Grid=G5]
[Controller: PC-101] -.-> [Valve: Control Valve, CV-103, Grid=G5]

### Level Control Loop
[Instrument: Level Sensor, LT-101, Grid=C5-B] -.-> [Controller: LC-101, Grid=C5-B]
[Controller: LC-101] -.-> [Valve: Control Valve, CV-106, Grid=C5-B]

## Stream Table
| Stream | From               | To                 | Flow (m³/h) | Temp (°C) | Pressure (bar) | Composition       | Path       |
|--------|--------------------|--------------------|-------------|-----------|----------------|-------------------|------------|
| 1      | Incoming: IN-501   | Nozzle: N1, T-101  | 100         | 50        | 1              | H2O=90%, NaCl=10% | G1 -> C5-T |
| 2      | Pump: P-101        | Heat Exchanger: HX-101 | 70      | 55        | 2              | H2O=90%, NaCl=10% | C5-M -> E7 |
| 3      | Heat Exchanger: HX-101 | Tank: T-102    | 30      | 30        | 1.5            | H2O=90%, NaCl=10% | E7 -> G5   |
| 4      | Intersection: X-1  | Tank: T-103        | 20          | 55        | 2              | H2O=90%, NaCl=10% | E7 -> G7   |
| 5      | Tank: T-103        | Intersection: X-2  | 10          | 40        | 1.5            | H2O=90%, NaCl=10% | G7 -> G5   |
| 6      | Nozzle: N3, T-101  | Tank: T-102        | 50          | 60        | 1.5            | H2O=90%, NaCl=10% | C5-B -> G5 |
| 7      | Nozzle: N4, T-101  | Outgoing: OUT-503  | 40          | 35        | 1.5            | H2O=90%, NaCl=10% | C5-S -> G9 |

```


---

## 🛠️ Best Practices
1. **Use Consistent Naming**: Follow a consistent naming convention for IDs (e.g., `T-101`, `P-101`).
2. **Leverage the Grid System**: Use grid coordinates to precisely locate items.
3. **Consolidate Instruments**: Group all instruments in a dedicated section for readability.
4. **Validate with LLMs**: Test the markdown with LLMs to ensure interpretability.

---

## 🤝 Contributing

We welcome contributions! If you have suggestions or improvements, please:
1. Fork the repository.
2. Create a new branch.
3. Submit a pull request.

---

## 📜 License

This project is licensed under the **Apache License 2.0**. This permissive license allows you to:

- Freely use, modify, distribute, and sell this software
- Include the software in proprietary products
- Make changes to the code without being required to release those changes

The license requires you to:
- Include the original copyright notice
- State significant changes made to the software
- Include the Apache License notice when distributing the software

For the complete terms and conditions, see the [LICENSE](LICENSE) file.

---

Thank you for using the **PFD Markdown Specification**! 🚀