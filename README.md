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

The user manual includes a complete end-to-end analysis case tutorial, text-only Figure 2 GUI workflow explanation, working directory and input format guidance, database setup and reuse instructions, batch workflow configuration, result inspection, output directory structure, troubleshooting, and HTML/Markdown/JSON reproducibility report documentation.

## Key Features

- **One-click analysis**: automated workflows for Prokka, BUSCO, CheckM2, dbCAN, antiSMASH, PhyloPhlAn, and ANI/AAI.
- **NCBI data acquisition**: batch genome retrieval using GCA/GCF accessions.
- **Containerized execution**: tools run in isolated Podman/Docker-compatible container environments.
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

Figure 2. Graphical user interface (GUI) workflow of TaxaScope. The workflow is operated from left to right in the desktop interface:

1. Open `TaxaScope.exe`. On first use, click `Env Setup` to install or initialize WSL2 and the Podman/Docker container environment.
2. After the interface shows `Env Ready`, click `Select Work Directory` and choose the project folder where input files, intermediate files, databases, reports, and outputs will be stored.
3. Click `Download DBs` to download the required reference databases into `TaxaScope_Databases` under the selected working directory.
4. Add input data by pasting GCA/GCF accessions in `Get Data`, or by placing local FASTA/FA/FNA/FAA files in the working directory.
5. Configure parameters in module tabs such as Prokka, CheckM, BUSCO, dbCAN, antiSMASH, PhyloPhlAn, and AAI/ANI.
6. Open `Batch`, select the modules to run sequentially, and keep report generation enabled when a summary report is needed.
7. Click `Deploy Complete Workflow`. Progress is shown in `Runtime`, command logs are shown in `Console`, and generated results can be selected from the left file browser and inspected in `Preview`.

A complete explanation is provided in the [TaxaScope User Manual](docs/TaxaScope_User_Manual.md).

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
