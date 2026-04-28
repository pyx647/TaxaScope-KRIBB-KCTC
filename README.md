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
- [HTML User Guide, English/Chinese/Korean](docs/TaxaScope_User_Guide.html)
- [Installation Guide](docs/Installation_Guide.md)
- [Software Availability](docs/Software_Availability.md)
- [Tool Reproducibility](docs/Tool_Reproducibility.md)

The user manual includes a complete end-to-end analysis case tutorial, Figure 2 GUI workflow explanation, working directory and input format guidance, database setup and reuse instructions, batch workflow configuration, result inspection, output directory structure, troubleshooting, and HTML/Markdown/JSON reproducibility report documentation.

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

![Figure 2. Graphical user interface of TaxaScope and workflow configuration](docs/assets/figure2_taxascope_gui_workflow.png)

Figure 2. Graphical user interface (GUI) of TaxaScope and workflow configuration. Numbered elements indicate key workflow steps: (1) environment setup, including WSL2 and the container engine (Podman/Docker); (2) working directory selection for input data, intermediate files, and outputs; (3) database download; (4) module parameter configuration; (5) optional NCBI data acquisition or local sequence input; (6) batch workflow selection; and (7) one-click workflow execution. A complete explanation is provided in the [TaxaScope User Manual](docs/TaxaScope_User_Manual.md).

## Getting Started

1. Download the latest TaxaScope release.
2. Run `TaxaScope.exe`.
3. Follow the [Installation Guide](docs/Installation_Guide.md) to set up the environment.
4. Read the [TaxaScope User Manual](docs/TaxaScope_User_Manual.md) for the complete GUI workflow tutorial, Figure 2 guide, output structure, and reproducibility report documentation.

## Publication and Citation

If you use TaxaScope in your research, please cite:

> [Author List], TaxaScope: An Integrated Platform for Reproducible Microbial Genome Analysis. *Journal Name* (2025). [DOI]

## License

This software is provided for academic use. Please see the [LICENSE](LICENSE) file for full details regarding usage restrictions and attribution.

The KCTC logo is a trademark of KRIBB and is not included under the open-source grant.
