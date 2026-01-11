# TaxaScope-KRIBB-KCTC
TaxaScope is an integrated, GUI-driven bioinformatics toolkit designed for microbial genome analysis within the Windows ecosystem. Developed at **KRIBB-KCTC**, it aims to bridge the gap between complex command-line workflows and user-friendly research applications.
# TaxaScope (KRIBB-KCTC Bioinformatics Toolkit)

[![Version](https://img.shields.io/badge/version-1.1-green.svg)](https://github.com/YourRepo/TaxaScope)
[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://github.com/YourRepo/TaxaScope)
[![License](https://img.shields.io/badge/license-Academic%20Use-orange.svg)](LICENSE)

TaxaScope is an integrated, GUI-driven bioinformatics toolkit designed for microbial genome analysis within the Windows ecosystem. Developed at **KRIBB-KCTC**, it aims to bridge the gap between complex command-line workflows and user-friendly research applications.

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

## 📦 Getting Started
1. Download the [Latest Release](URL).
2. Run `TaxaScope.exe`.
3. Follow the **[Installation Guide](Installation_Guide.md)** to setup the environment.

## 📜 Publication and Citation
If you use TaxaScope in your research, please cite:
> [Author List], TaxaScope: An Integrated Platform for Reproducible Microbial Genome Analysis. *Journal Name* (2025). [DOI]

## ⚖ License
This software is provided for **Academic Use Only**. Please see the [LICENSE](LICENSE) file for full details regarding usage restrictions and attribution.
- The KCTC logo is a trademark of KRIBB and is not included under the open-source grant.
