# e-markdown (Engineering Markdown)

Welcome to the **Engineering Markdown (e-markdown)** repository! This project aims to establish standardized markdown-based syntaxes for various engineering documents, making them both human-readable and machine-interpretable.

> **Note:** This is an emerging collection of specifications, designed to bring consistency and interoperability to engineering documentation across disciplines.

## 📌 Table of Contents

1. [Overview](#-overview)
2. [Why e-markdown?](#-why-e-markdown)
3. [Specifications](#-specifications)
4. [Roadmap](#-roadmap)
5. [Example](#-example)
6. [Implementation](#-implementation)
7. [Contributing](#-contributing)
8. [License](#-license)

## 📌 Overview

Engineering documentation has traditionally relied on specialized software tools, creating barriers to collaboration and integration. The e-markdown project addresses this by developing open, text-based specifications that can be:

- **Version controlled** using standard tools like Git
- **Edited** with any text editor
- **Parsed** by machines for visualization and analysis
- **Shared** across teams without proprietary software requirements
- **Integrated** with modern AI and automation tools

## 💡 Why e-markdown?

Traditional engineering documentation is often locked away in proprietary formats, making it difficult to:

- Collaborate across teams and organizations
- Integrate with modern automation, AI, and data analysis tools
- Maintain version control and track changes
- Ensure long-term accessibility and interoperability

**e-markdown** solves these problems by providing:

- **Open, human-readable formats** for all engineering disciplines
- **Machine-parseable syntax** for easy integration with visualization and simulation tools
- **Standardization** across industries and document types
- **Future-proofing** of engineering knowledge and workflows

## 📚 Specifications

The e-markdown project currently includes the following specifications:

| Specification | Description | Status | Link |
|---------------|-------------|--------|------|
| **PFD Markdown** | Markdown syntax for Process Flow Diagrams (PFDs) used in chemical, petrochemical, and process industries. Defines equipment, streams, instruments, and their relationships. | Rev.0 (Initial) | [pfd-markdown/](pfd-markdown/) |
| **P&ID Markdown** | Extension of PFD Markdown for detailed Piping and Instrumentation Diagrams (P&IDs), including piping, valves, instrumentation, and control systems. | Planned | [pid-markdown/](pid-markdown/) |
| **Electrical Diagrams** | Specification for single-line and schematic electrical diagrams. | Planned | _Coming soon_ |
| **Civil/Structural Drawings** | Standardized markdown for foundation and structural element specifications. | Planned | _Coming soon_ |
| **Material Specifications** | Standardized material property documentation. | Planned | _Coming soon_ |
| **Test Procedures** | Structured test methodology documentation. | Planned | _Coming soon_ |

> See each specification directory for detailed syntax, examples, and best practices.

## 🗺️ Roadmap

| Milestone                | Description                                                      | Status         | Target Date   |
|--------------------------|------------------------------------------------------------------|---------------|--------------|
| PFD Markdown Rev.0       | Initial release of Process Flow Diagram markdown specification   | ✅ Released    | 2024-06       |
| P&ID Markdown Draft      | Draft specification for Piping and Instrumentation Diagrams      | 🚧 In Progress | Q1 2025       |
| Electrical Diagrams Spec | Initial draft for electrical single-line/schematic diagrams      | ⏳ Planned     | Q2 2025       |
| Civil/Structural Spec    | Draft for civil/structural markdown specification                | ⏳ Planned     | Q3 2025       |
| Material Specs           | Standardized material property documentation                     | ⏳ Planned     | Q3 2025       |
| Test Procedures Spec     | Structured test methodology documentation                        | ⏳ Planned     | Q4 2025       |

## 📝 Example

Here's a minimal example of a Process Flow Diagram (PFD) using e-markdown syntax:

```markdown
# Example: Simple Distillation PFD

## Limits
- [Incoming: IN-101, Description="Feed from Storage"]
  - Stream: [Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar]
  - Connects To: [Nozzle: N1, Distillation Tower: T-101]

## Equipment
[Equipment: Distillation Tower, T-101, Height=30m, Diameter=2m, Location=C5]
- [Nozzle: N1, Location=Top, Grid=C5-T]
- [Nozzle: N2, Location=Bottom, Grid=C5-B]

## Streams
[Stream: 1, Flow=100 m³/h, T=50°C, P=1 bar, Path=G1 -> C5-T]
- From: [Incoming: IN-101]
- To: [Nozzle: N1, Distillation Tower: T-101]
```

> See [pfd-markdown/README.md](pfd-markdown/README.md) for full syntax and advanced examples.

## 🛠️ Implementation

Each specification in the e-markdown family includes:

1. **Formal syntax definitions** - Clear rules for representing engineering elements
2. **Examples** - Practical demonstrations of the syntax in use
3. **Best practices** - Guidelines for effective implementation
4. **Visualization guidance** - Recommendations for rendering the markdown as diagrams

## 🤝 Contributing

We welcome contributions from the engineering community! To contribute:

1. **Provide feedback** on existing specifications
2. **Suggest new specifications** for other engineering document types
3. **Develop tools** that implement these specifications
4. **Share examples** of the specifications in use

Please see our [Contributing Guidelines](CONTRIBUTING.md) for more details.

## 📜 License

All specifications in the e-markdown project are licensed under the **Apache License 2.0**. This permissive license allows you to:

- Freely use, modify, distribute, and sell implementations of these specifications
- Include the specifications in proprietary products
- Make changes without being required to release those changes

For complete terms and conditions, see the [LICENSE](LICENSE) file.

---

Thank you for your interest in the **Engineering Markdown** project! Together, we can make engineering documentation more accessible, interoperable, and future-proof. 🚀
