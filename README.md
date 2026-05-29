# TaxaScope (KRIBB-KCTC Bioinformatics Toolkit)

[![Version](https://img.shields.io/badge/version-1.0-green.svg)](https://github.com/pyx647/TaxaScope-KRIBB-KCTC)
[![Platform](https://img.shields.io/badge/platform-Windows-blue.svg)](https://github.com/pyx647/TaxaScope-KRIBB-KCTC)
[![License](https://img.shields.io/badge/license-Academic%20Use-orange.svg)](LICENSE)

Korean Collection for Type Cultures (KCTC), Korea Research Institute of Bioscience and Biotechnology (KRIBB)

TaxaScope is an integrated, GUI-driven bioinformatics toolkit designed for microbial genome analysis within the Windows ecosystem. It bridges complex command-line workflows and user-friendly research applications by combining workflow configuration, containerized execution, result preview, and reproducibility reporting in one desktop interface.

## Documentation

The maintained documentation is centralized in the `docs/` directory.

- [Documentation Index](docs/README.md)
- [TaxaScope User Manual](docs/TaxaScope_User_Manual.md)
- [HTML User Guide, English/Chinese/Korean, text-only workflow version](docs/TaxaScope_User_Guide.html)
- [Installation Guide](docs/Installation_Guide.md)
- [Software Availability](docs/Software_Availability.md)
- [Tool Reproducibility](docs/Tool_Reproducibility.md)

The user manual is the main reviewer-facing documentation. It now describes the actual desktop workflow implemented in TaxaScope: first-time environment setup, working directory selection, one-click database download, offline or online container image handling, NCBI or local input preparation, module parameter configuration, batch execution, result inspection, output directory structure, troubleshooting, and HTML/Markdown/JSON reproducibility reporting.

## Key Features

- **One-click analysis**: automated workflows for Prokka, BUSCO, CheckM2, dbCAN, antiSMASH, PhyloPhlAn, and ANI/AAI.
- **NCBI data acquisition**: batch genome retrieval using GCA/GCF accessions.
- **Containerized execution**: tools run in isolated Podman/Docker-compatible container environments.
- **Offline image handling**: users can import or export pre-packaged container images when network access is limited.
- **Batch workflow configuration**: users can combine modules into sequential workflows.
- **Result inspection**: output files, plots, reports, and trees can be inspected from the GUI.
- **Reproducibility reporting**: runs can export HTML, Markdown, and JSON reports containing software, database, parameter, timestamp, input, and output metadata.

## Architecture

TaxaScope uses a four-layer architecture to support stability and reproducibility:

1. **Presentation layer**: CustomTkinter-based graphical user interface.
2. **Orchestration layer**: Python and PowerShell scripts for task scheduling, parameter handling, and data flow.
3. **Analysis core**: containerized bioinformatics tools and local databases.
4. **Infrastructure layer**: Windows host system with WSL2 and Podman/Docker backend.

<img width="1916" height="1029" alt="Figure 1. TaxaScope architecture" src="https://github.com/user-attachments/assets/69093f22-e0cb-4a13-b01a-d653ad878088" />

Figure 1. TaxaScope architecture. The system operates on a four-layer model: user interface, orchestration engine, analysis core, and infrastructure. The presentation layer provides the GUI for parameter tuning and result visualization. The orchestration layer manages task scheduling and resource allocation. The analysis core executes bioinformatics tools within isolated container environments. The infrastructure layer handles Windows, WSL2, Podman/Docker, and data I/O.

## Included Tools

| Tool | Function |
| :--- | :--- |
| Prokka | Rapid genome annotation |
| ANI/AAI | Taxonomic identity and species delimitation |
| dbCAN3 | Carbohydrate-active enzyme identification |
| antiSMASH | Biosynthetic gene cluster analysis |
| CheckM2 | Machine learning-based quality assessment |
| BUSCO | Lineage-specific completeness assessment |
| PhyloPhlAn | Whole-genome phylogeny |
| Get Data | Batch NCBI genome downloader |

## GUI Workflow

TaxaScope GUI workflow. The workflow is operated as follows:

1. Open `TaxaScope.exe`; on first use, click `Env Setup` and wait until the interface reports `Env Ready`.
2. Click `Select Work Directory` and choose the project folder that will contain inputs, databases, intermediate files, outputs, and reports.
3. Click `Download DBs` to populate `TaxaScope_Databases` and write database provenance files.
4. Add input data through `Get Data` with GCA/GCF accessions, or place local FASTA/FA/FNA/FAA/GBK/GBFF files in the working directory.
5. Configure module parameters in `Genome Stats`, `Prokka`, `CheckM`, `BUSCO`, `dbCAN`, `antiSMASH`, `PhyloPhlAn`, and `AAI/ANI`.
6. Open `Batch`, use `Data Acquisition (Optional)` and `Analysis Sequence Setup`, keep report generation enabled if needed, and click `DEPLOY COMPLETE WORKFLOW`.
7. Use `Runtime`, `Console`, `File Browser`, and `Preview` to monitor progress, troubleshoot logs, inspect outputs, and review reports.

A complete explanation is provided in the [TaxaScope User Manual](docs/TaxaScope_User_Manual.md).

## System Requirements

| Component | Minimum | Recommended |
| :--- | :--- | :--- |
| Operating System | Windows 10 64-bit (build 19041+) | **Windows 11 64-bit** |
| RAM | 16 GB | **64 GB** |
| CPU | 4-core x86-64 | 16-core x86-64 |
| Disk | 200 GB free (SSD) | 1 TB free (NVMe SSD) |
| WSL2 | Required | Required |
| Container runtime | Podman or Docker Desktop | Podman (rootless) |

> **Note:** 64 GB RAM is strongly recommended when running memory-intensive modules such as CheckM2, BUSCO, and PhyloPhlAn concurrently on large genome sets. Analyses on datasets with more than 50 genomes may be significantly slower or fail on systems with less than 32 GB RAM.

## Getting Started

1. Download the latest TaxaScope release.
2. Run `TaxaScope.exe`.
3. Click `Env Setup` to initialize the execution environment on first use.
4. Click `Select Work Directory`, choose the project folder, then click `Download DBs`.
5. Read the [TaxaScope User Manual](docs/TaxaScope_User_Manual.md) for the complete GUI workflow tutorial, output structure, and reproducibility report documentation.

## Publication and Citation

If you use TaxaScope in your research, please cite:

> [Author List], TaxaScope: An Integrated Platform for Reproducible Microbial Genome Analysis. *Journal Name* (2025). [DOI]

## License

This software is provided for academic use. Please see the [LICENSE](LICENSE) file for full details regarding usage restrictions and attribution.

The KCTC logo is a trademark of KRIBB and is not included under the open-source grant.
