# Software and Code Availability

## Software Information
- **Software Name**: TaxaScope (KRIBB-KCTC Bioinformatics Toolkit)
- **Version**: 1.0
- **Platform**: Windows 10/11 (via WSL2 and Podman/Docker)
- **Programming Language**: Python 3.10+ (GUI: CustomTkinter)
- **Containerization**: Podman/Docker (Linux-based microbial analysis images)

## Code Availability
The source code for the TaxaScope GUI and orchestration engine is available at [GitHub Repository URL - Placeholder]. The toolkit is released under a custom **Academic Use Only License**. 

To ensure computational reproducibility, all analysis tools integrated into TaxaScope are executed within standardized container environments. A complete list of container images and their respective versions is provided in the documentation and the supplementary materials of this paper.

## Reproducibility Statement
TaxaScope is designed with 'Container-based Reproducibility' as a core principle. By bundling specific versions of bioinformatics tools (e.g., Prokka, CheckM2, antiSMASH) within Docker/Podman containers, TaxaScope eliminates 'environment drift' and dependency conflicts across different user systems. Every analysis run uses the same underlying binary versions and database environments as specified in the metadata.

## Contact
For software-related inquiries or technical support, please contact the corresponding author(s) at [Author Email].

