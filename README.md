# TaxaScope (KRIBB-KCTC Bioinformatics Toolkit)

[![Version](https://img.shields.io/badge/version-1.0-green.svg)](https://github.com/YourRepo/TaxaScope)
[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://github.com/YourRepo/TaxaScope)
[![License](https://img.shields.io/badge/license-Academic%20Use-orange.svg)](LICENSE)

Korean Collection for Type Cultures (KCTC), Korea Research Institute of Bioscience and Biotechnology (KRIBB)

TaxaScope is an integrated, GUI-driven bioinformatics toolkit designed for microbial genome analysis within the Windows ecosystem. Developed at **KRIBB-KCTC**, it aims to bridge the gap between complex command-line workflows and user-friendly research applications.

## Documentation and Complete Analysis Tutorial

For reviewers and users, a complete GitHub-accessible manual is provided here:

- **[TaxaScope User Manual](docs/TaxaScope_User_Manual.md)**
- **[HTML User Guide](BioToolkit_Guide.html)**

The manual includes:

- a complete end-to-end analysis case tutorial
- Figure 2 explaining the GUI workflow and numbered operation steps
- working directory and input format guidance
- database download and reuse instructions
- batch workflow configuration
- result inspection and preview workflow
- output directory structure
- reproducibility report documentation, including HTML, Markdown, and JSON outputs


## 🚀 Key Features
- **One-Click Analysis**: Automated workflows for Prokka, BUSCO, CheckM2, dbCAN, antiSMASH, and ANI/AAI.
- **NCBI Data Fetcher**: Integrated module to batch download genomes from NCBI using GCA/GCF accessions.
- **Micro-Kernel Architecture**: Every tool runs in an isolated, version-locked container (Podman/Docker).
- **Publication Ready**: Built-in high-resolution visualization (PNG/SVG) and summary reports.
- **Zero Configuration**: Automated setup of WSL2 and container runtimes.

## 🏗 Architecture
TaxaScope uses a 4-layer architecture to ensure stability and reproducibility:
1. **Presentation (UI)**: CustomTkinter-based modern GUI.
2. **Orchestration**: Python/PowerShell scripts managing data flow and tool sequencing.
3. **Analysis Core**: Containerized micro-services (Tools + Bundled Databases).
4. **Infrastructure**: Host Windows OS with WSL2 backend.

## 🛠 Included Tools
| Tool | Function |
| :--- | :--- |
| **Prokka** | Rapid Genome Annotation |
| **ANI/AAI** | Taxonomic Identity and Species Delimitation | 
| **dbCAN3** | Carbohydrate-Active Enzyme Identification |
| **antiSMASH 7** | Biosynthetic Gene Cluster Analysis |
| **CheckM2** | Machine Learning-based Quality Assessment |
| **BUSCO** | Lineage-specific Completeness Check |
| **PhyloPhlAn** | Core-Gene Phylogeny |
| **Get Data** | Batch NCBI Genome Downloader (via Datasets API) |

<img width="1916" height="1029" alt="image" src="https://github.com/user-attachments/assets/69093f22-e0cb-4a13-b01a-d653ad878088" />
Figure 1. TaxaScope Architecture. The system operates on a four-layer model:
User Interface (Layer 1): Provides a rigorous GUI for parameter tuning and results visualization.
Orchestration Engine (Layer 2): Manages task scheduling and resource allocation across the host system.
Analysis Core (Layer 3): Executes bioinformatic tools (e.g., Prokka, antiSMASH) within isolated micro-kernels (containers) to ensure reproducibility.
Infrastructure (Layer 4): Handles data I/O and hardware interaction seamlessly.

![Figure 2. Graphical user interface of TaxaScope and workflow configuration](docs/assets/figure2_taxascope_gui_workflow.png)
Figure 2. Graphical user interface (GUI) of TaxaScope and workflow configuration. Numbered elements indicate key workflow steps: (1) environment setup, including WSL2 and the container engine (Podman/Docker); (2) working directory selection for input data, intermediate files, and outputs; (3) database download; (4) module parameter configuration; (5) optional NCBI data acquisition or local sequence input; (6) batch workflow selection; and (7) one-click workflow execution. A complete explanation is provided in the [TaxaScope User Manual](docs/TaxaScope_User_Manual.md).
The TaxaScope graphical user interface provides a file-system–based workflow for configuring and executing prokaryotic genome analyses. The left panel displays the working directory and detected input files. The central panel allows users to select and combine analysis modules into a batch workflow, including genome statistics, annotation, quality assessment, phylogeny, and functional mining. The right panel presents real-time execution status and progress monitoring, as well as a live preview of the analysis results. This interface abstracts containerized execution and resource management, enabling guided, no–command-line analysis on local desktop systems.


## 📦 Getting Started
1. Download the [Latest Release](URL).
2. Run `TaxaScope.exe`.
3. Follow the **[Installation Guide](Installation_Guide.md)** to setup the environment.
4. See the **[TaxaScope User Manual](docs/TaxaScope_User_Manual.md)** for the complete GUI workflow tutorial, Figure 2 guide, output structure, and reproducibility report documentation.

## 📜 Publication and Citation
If you use TaxaScope in your research, please cite:
> [Author List], TaxaScope: An Integrated Platform for Reproducible Microbial Genome Analysis. *Journal Name* (2025). [DOI]

## ⚖ License
This software is provided for **Academic Use Only**. Please see the [LICENSE](LICENSE) file for full details regarding usage restrictions and attribution.
- The KCTC logo is a trademark of KRIBB and is not included under the open-source grant.
