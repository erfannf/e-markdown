# P&ID Markdown Specification

This repository will contain the **P&ID Markdown Specification**, a markdown-based syntax for creating **Piping and Instrumentation Diagrams (P&IDs)** that are both human-readable and machine-interpretable.

> **Note:** This specification is currently under development. The full implementation will follow the template established by the [PFD Markdown Specification](https://github.com/erfannf/e-markdown/blob/main/pfd-markdown/README.md).

---

## 📌 Table of Contents

1. [Introduction](#-introduction)
2. [Syntax Overview](#-syntax-overview)
3. [Core Components](#-core-components)
   - [Piping](#-piping)
   - [Equipment](#-equipment)
   - [Instruments](#-instruments)
   - [Valves](#-valves)
   - [Control Systems](#-control-systems)
4. [Grid System](#-grid-system)
5. [Symbols & Legends](#-symbols--legends)
6. [Examples](#-examples)
7. [Best Practices](#-best-practices)
8. [Contributing](#-contributing)
9. [License](#-license)

---

## 🌟 Introduction

Piping and Instrumentation Diagrams (P&IDs) are critical for visualizing, designing, and documenting the detailed piping, instrumentation, and control systems of process plants across industries such as chemical, petrochemical, pharmaceutical, and energy. 

The **P&ID Markdown Specification** introduces a **markdown-based syntax** for creating standardized P&IDs that are:

- **Human-readable**: Easily understood and edited by engineers without specialized software.
- **Machine-interpretable**: Parsable by software tools, LLMs, and automation systems for visualization, validation, and analysis.
- **Extensible**: Capable of representing both simple and highly complex process systems, including safety and control logic.
- **Version-controllable**: Compatible with standard version control systems like Git for collaborative engineering workflows.

This specification builds upon the foundation of [PFD Markdown](../pfd-markdown/README.md), extending it to include:

- Detailed piping specifications (line numbers, sizes, classes)
- Comprehensive instrumentation and control system details
- Valve types, safety systems, and interlocks
- Equipment connections, utilities, and process interfaces

The syntax is designed to align with industry standards such as **ISA-5.1** (instrumentation symbols and identification), **ISO 10628** (flow diagrams for process plants), and other relevant codes, ensuring compatibility with established engineering practices and digital transformation initiatives.

---

## 📖 Syntax Overview

The P&ID Markdown syntax is designed to provide a clear, structured, and extensible way to represent all the essential elements of a Piping and Instrumentation Diagram. The syntax builds on the foundation established by PFD Markdown, but introduces additional detail and rigor to capture the full complexity of process plant design, operation, and control.

P&ID Markdown is organized into **sections**, each corresponding to a major aspect of the diagram. Each section uses a standardized, human-readable key-value format, with square brackets for primary elements and indentation or sub-lists for nested attributes and relationships.

### Key Principles

- **Explicitness**: Every piping, equipment, instrument, and control element is explicitly defined with unique identifiers and attributes.
- **Hierarchy**: The document is organized in a logical hierarchy, mirroring the way engineers think about process systems.
- **Extensibility**: The syntax is designed to accommodate new types of equipment, instruments, and control logic as needed.
- **Machine-Readability**: The format is easy to parse for software tools, enabling automation, validation, and visualization.

### Main Sections

A typical P&ID Markdown file includes the following sections:

- **Piping**: All process, utility, and instrument piping, including line numbers, sizes, classes, and specifications.
- **Equipment**: All major and minor process equipment, with detailed connection points (nozzles, flanges, etc.).
- **Instruments**: All field instruments, transmitters, analyzers, and local indicators, with tag numbers and signal types.
- **Valves**: All valve types, including control, isolation, check, relief, and safety valves, with actuation and fail-safe details.
- **Control Systems**: Controllers, logic solvers, interlocks, and signal pathways, including hardwired and digital systems.
- **Grid System**: A virtual grid for spatial organization and reference.
- **Symbols & Legends**: Standardized symbols and abbreviations for all elements.
- **Examples**: Example snippets and full diagrams.
- **Best Practices**: Guidance for effective and consistent use.

---

### Section Structure and Syntax

#### 1. **Piping**

Piping is the backbone of a P&ID. Each line is defined with a unique line number and includes attributes such as size, class, insulation, tracing, and service. Connections to equipment, valves, and instruments are explicitly listed.

**Syntax Example:**
```markdown
[Piping: 101A, Size=6", Class=150#, Material="CS", Insulation="Yes", Tracing="Steam", Service="Process Water"]
- From: [Nozzle: N1, Equipment: P-101]
- To: [Nozzle: N2, Equipment: V-101]
- Contains: [Valve: XV-101, Instrument: FT-101]
- Line_Spec: [Spec=PW-150, Design_Pressure=10 bar, Design_Temperature=120°C]
```

#### **Pipe Numbering and Line Designation**

In P&IDs, each pipe is assigned a unique **line number** (line designation) that encodes critical information about the pipe's service, size, sequence, and other attributes. This convention ensures unambiguous identification and cross-referencing throughout the plant.

A typical line number may include:

- **Service code** (e.g., QHW = Quenched Hot Water)
- **Unit or area number** (e.g., 55)
- **Sequence number** (e.g., 0001)
- **Modifiers** (e.g., B1A2 for branch, spec, or insulation)
- **Nominal pipe size** (e.g., 8")
- **Piping class or material** (e.g., ST for Steel)
- **Insulation/Tracing** (e.g., (W) for heat tracing)

**Example Line Number:**  
`QHW-55-0001B1A2-8"-ST(W)`

| Segment         | Example Value | Meaning                        |
|-----------------|--------------|--------------------------------|
| Service         | QHW          | Quenched Hot Water             |
| Unit/Area       | 55           | Unit 55                        |
| Sequence        | 0001         | Line sequence number           |
| Modifiers       | B1A2         | Branch, spec, or insulation    |
| Size            | 8"           | Nominal pipe size              |
| Material/Class  | ST           | Steel piping class             |
| Insul/Tracing   | (W)          | With heat tracing              |

**P&ID Markdown Representation:**
```markdown
[Piping: QHW-55-0001B1A2-8"-ST(W)", Service="Quenched Hot Water", Size=8", Class="ST", Tracing="W", Insulation="Yes"]
- From: [Nozzle: N1, Equipment: P-101]
- To: [Nozzle: N2, Equipment: V-101]
- Contains: [Valve: XV-101, Instrument: FT-101]
- Line_Spec: [Design_Pressure=10 bar, Design_Temperature=120°C]
```

**Notes:**
- The full line number is always included as the primary identifier.
- For clarity and machine-readability, each segment of the line number can be broken out as a separate attribute.
- The `Line_Spec` sub-element can be used for additional specification details (pressure, temperature, etc.).
- The `Contains` sub-list can enumerate all inline valves, instruments, and fittings.

**Best Practice:**  
Always follow your project or company's line numbering standard, and document the meaning of each segment in the project's Symbols & Legends or a dedicated Line Numbering Legend section.

#### 2. **Equipment**

Equipment is defined by type, tag, and attributes such as size, material, and location. Each equipment item lists its connection points (nozzles, flanges, etc.) and their grid locations.

**Example:**
```markdown
[Equipment: Vessel, V-101, Type="Vertical", Volume=10m³, Material="SS316", Location=D5]
- [Nozzle: N1, Type=Inlet, Size=8", Grid=D5-T, Service="Feed In"]
- [Nozzle: N2, Type=Outlet, Size=8", Grid=D5-B, Service="Product Out"]
```

#### 3. **Instruments**

Instruments are defined with tag, type, range, signal, and location. Each instrument is associated with a process connection (tap, nozzle, or inline) and may include local indicators or transmitters.

**Example:**
```markdown
[Instrument: Flow Transmitter, FT-101, Range=0-100 m³/h, Signal="4-20mA", Location=D5-T]
- Connected_To: [Piping: QHW-55-0001B1A2-8"-ST(W)", Tap=TP1]
- Display: [Local Indicator, FI-101, Location=D5-T]
```

#### 4. **Valves**

Valves are defined with tag, type, size, actuation, and fail position. Each valve is associated with a specific line and location, and may be connected to an actuator or instrument.

**Example:**
```markdown
[Valve: Control Valve, CV-101, Size=8", Type="Globe", Actuator="Pneumatic", Fail_Position="Closed", Location=D5-B]
- On_Line: [Piping: QHW-55-0001B1A2-8"-ST(W)"]
- Connected_To: [Instrument: FT-101]
```

#### 5. **Control Systems**

Control systems include controllers, logic solvers, interlocks, and signal paths. Each control loop is defined with its elements and signal types.

**Syntax Example:**
```markdown
[Controller: Flow Controller, FC-101, Type="PID", Location=Control Room]
- Input: [Instrument: FT-101]
- Output: [Valve: CV-101]
- Signal: [Input="4-20mA", Output="4-20mA", Protocol="HART"]
- Interlock: [Shutdown on Low Flow, Setpoint=10 m³/h]
```

#### 6. **Grid System**

A virtual grid system is used to specify the location of items on the P&ID. The grid uses letters for columns and numbers for rows (e.g., D5 = Column D, Row 5). Nozzles and instruments are assigned specific grid locations for clarity and cross-referencing.

**Example:**
```markdown
[Equipment: Vessel, V-101, Location=D5]
- [Nozzle: N1, Grid=D5-T]
- [Nozzle: N2, Grid=D5-B]
[Instrument: Flow Transmitter, FT-101, Location=D5-T]
```

#### 7. **Symbols & Legends**

A dedicated section defines the symbols and abbreviations used, ensuring clarity and standardization.

**Syntax Example:**
```markdown
## Symbols & Legends
- [Valve: Control Valve] = ⭘▲
- [Instrument: Flow Transmitter] = ⭘FT
- [Piping: Process Line] = ──────
```

---

### Document Organization

A typical P&ID Markdown file is organized as follows:

```markdown
# <Project/Unit Name>
[P&ID Number: <ID>, Revision: <Rev>, Date: <YYYY-MM-DD>]

## Piping
...

## Equipment
...

## Instruments
...

## Valves
...

## Control Systems
...

## Grid System
...

## Symbols & Legends
...

## Examples
...

## Best Practices
...
```

---

### Extending the Syntax

The P&ID Markdown syntax is designed to be extensible. New attributes, equipment types, or control logic can be added using the same key-value and hierarchical structure. This ensures the format remains relevant as engineering practices and technologies evolve.

---

By following this syntax overview, engineers and software tools can create, interpret, and validate P&IDs in a way that is both rigorous and accessible, supporting the full lifecycle of process plant design, operation, and maintenance.

---

## 🧩 Core Components

### 🛢️ Piping

Piping in P&ID Markdown is defined with a unique line number and all relevant attributes, including size, class, material, insulation, tracing, and service. Each pipe connects specific equipment or process points and may contain inline valves and instruments.

**Example:**
```markdown
[Piping: QHW-55-0001B1A2-8"-ST(W)", Service="Quenched Hot Water", Size=8", Class="ST", Tracing="W", Insulation="Yes"]
- From: [Nozzle: N1, Equipment: P-101]
- To: [Nozzle: N2, Equipment: V-101]
- Contains: [Valve: XV-101, Instrument: FT-101]
- Line_Spec: [Design_Pressure=10 bar, Design_Temperature=120°C]
```

### 🏭 Equipment

Equipment is defined by type, tag, and attributes such as size, material, and location. Each equipment item lists its connection points (nozzles, flanges, etc.) and their grid locations.

**Example:**
```markdown
[Equipment: Vessel, V-101, Type="Vertical", Volume=10m³, Material="SS316", Location=D5]
- [Nozzle: N1, Type=Inlet, Size=8", Grid=D5-T, Service="Feed In"]
- [Nozzle: N2, Type=Outlet, Size=8", Grid=D5-B, Service="Product Out"]
```

### 🎛️ Instruments

Instruments are defined with tag, type, range, signal, and location. Each instrument is associated with a process connection (tap, nozzle, or inline) and may include local indicators or transmitters.

**Example:**
```markdown
[Instrument: Flow Transmitter, FT-101, Range=0-100 m³/h, Signal="4-20mA", Location=D5-T]
- Connected_To: [Piping: QHW-55-0001B1A2-8"-ST(W)", Tap=TP1]
- Display: [Local Indicator, FI-101, Location=D5-T]
```

### 🚪 Valves

Valves are defined with tag, type, size, actuation, and fail position. Each valve is associated with a specific line and location, and may be connected to an actuator or instrument.

**Example:**
```markdown
[Valve: Control Valve, CV-101, Size=8", Type="Globe", Actuator="Pneumatic", Fail_Position="Closed", Location=D5-B]
- On_Line: [Piping: QHW-55-0001B1A2-8"-ST(W)"]
- Connected_To: [Instrument: FT-101]
```

### 🕹️ Control Systems

Control systems include controllers, logic solvers, interlocks, and signal paths. Each control loop is defined with its elements and signal types.

**Example:**
```markdown
[Controller: Flow Controller, FC-101, Type="PID", Location=Control Room]
- Input: [Instrument: FT-101]
- Output: [Valve: CV-101]
- Signal: [Input="4-20mA", Output="4-20mA", Protocol="HART"]
- Interlock: [Shutdown on Low Flow, Setpoint=10 m³/h]
```

---

## 🎨 Symbols & Legends

The following table defines standard symbols for P&ID elements, aligned with ISA-5.1 and ISO 10628.

| **Component**         | **Symbol** | **Markdown Representation**                  | **Standard**   |
|-----------------------|------------|----------------------------------------------|----------------|
| Process Line          | ──────     | `[Piping: ...]`                              | ISO 10628      |
| Instrument (Transmitter) | ⭘FT     | `[Instrument: Flow Transmitter, FT-101]`     | ISA-5.1        |
| Control Valve         | ⭘▲         | `[Valve: Control Valve, CV-101]`             | ISA-5.1        |
| Manual Valve          | ─┼─        | `[Valve: Manual Valve, MV-101]`              | ISA-5.1        |
| Controller            | ⬡FC        | `[Controller: Flow Controller, FC-101]`      | ISA-5.1        |
| Signal (Electric)     | ─ ─ ─      | `[Instrument: ...] -.-> [Controller: ...]`   | ISA-5.1        |
| Nozzle                | ●          | `[Nozzle: N1, ...]`                          | ISO 10628      |

> For a full legend, see the [ISA-5.1 standard](https://instrumentationtools.com/isa-5-1-instrumentation-symbols/) and your project's symbol library.

---

## 📚 Examples

### Minimal Example

```markdown
# Example: Simple P&ID

## Piping
[Piping: QHW-55-0001B1A2-8"-ST(W)", Service="Quenched Hot Water", Size=8", Class="ST", Tracing="W", Insulation="Yes"]
- From: [Nozzle: N1, Equipment: P-101]
- To: [Nozzle: N2, Equipment: V-101]
- Contains: [Valve: XV-101, Instrument: FT-101]

## Equipment
[Equipment: Pump, P-101, Type="Centrifugal", Power=7.5kW, Location=B3]
- [Nozzle: N1, Type=Suction, Size=8", Grid=B3-L]
- [Nozzle: N2, Type=Discharge, Size=8", Grid=B3-R]
[Equipment: Vessel, V-101, Type="Vertical", Volume=10m³, Location=D5]
- [Nozzle: N2, Type=Inlet, Size=8", Grid=D5-B]

## Instruments
[Instrument: Flow Transmitter, FT-101, Range=0-100 m³/h, Signal="4-20mA", Location=D5-T]
- Connected_To: [Piping: QHW-55-0001B1A2-8"-ST(W)", Tap=TP1]

## Valves
[Valve: Control Valve, CV-101, Size=8", Type="Globe", Actuator="Pneumatic", Fail_Position="Closed", Location=D5-B]
- On_Line: [Piping: QHW-55-0001B1A2-8"-ST(W)"]

## Control Systems
[Controller: Flow Controller, FC-101, Type="PID", Location=Control Room]
- Input: [Instrument: FT-101]
- Output: [Valve: CV-101]
```

---

## 🛠️ Best Practices

- **Use Consistent Tagging:** Follow a consistent tag and line numbering convention throughout the project.
- **Leverage the Grid System:** Assign grid locations to all major items for clarity and cross-referencing.
- **Document Symbols:** Maintain a clear legend for all symbols and abbreviations used.
- **Validate Syntax:** Use automated tools or LLMs to check for completeness and correctness.
- **Version Control:** Store all P&ID markdown files in a version-controlled repository (e.g., Git).
- **Review and Update:** Regularly review and update the P&ID as the design evolves.

---

## 🤝 Contributing

We welcome input on the development of this specification. Please open an issue to suggest features or considerations for the upcoming specification.

---

## 📜 License

This project will be licensed under the **Apache License 2.0**, consistent with the PFD Markdown Specification.

---

Thank you for your interest in the **P&ID Markdown Specification**! 🚀

## 🔢 Line Numbering Legend

| Segment         | Description                       | Example   |
|-----------------|-----------------------------------|-----------|
| Service         | Process fluid/service code        | QHW       |
| Unit/Area       | Plant unit or area number         | 55        |
| Sequence        | Line sequence number              | 0001      |
| Modifiers       | Branch, spec, or insulation code  | B1A2      |
| Size            | Nominal pipe size                 | 8"        |
| Class/Material  | Piping class or material          | ST        |
| Insul/Tracing   | Insulation/tracing code           | (W)       |

> Refer to your project documentation for the exact meaning of each segment.
