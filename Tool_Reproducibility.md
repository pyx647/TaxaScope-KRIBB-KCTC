# Containerized Tool Metadata & Reproducibility

To ensure transparency and reproducibility, TaxaScope uses fixed container images. Below are the specific versions and parameters for each module as of version 1.1.

| Module | Core Tool | Container Image | Version/Tag |
| :--- | :--- | :--- | :--- |
| **Genome Stats** | Python/Biopython | Native Python (GUI) | v1.1 |
| **Prokka** | Prokka v1.14.6 | `pyx07/prokka` | `:latest` |
| **CheckM2** | CheckM2 v1.0.1 | `pyx07/checkm2` | `:v2-with-db` |
| **BUSCO** | BUSCO v5.8.2 | `pyx07/busco` | `:v5-with-db` |
| **dbCAN** | dbCAN3 (dbCAN 5.x) | `pyx07/dbcan` | `:v5-with-db` |
| **antiSMASH** | antiSMASH 7.0 | `pyx07/antismash` | `:latest` |
| **PhyloPhlAn** | PhyloPhlAn 3.0 | `pyx07/phylophlan` | `:v3-with-db` |
| **AAI/ANI** | pyani / FastANI | `pyx07/aanani` | `:latest` |

## Analysis Logic (Workflow Sequencing)
In 'Batch Mode', TaxaScope enforces a specific dependency-aware execution order to ensure data integrity:
1. **Genome Stats**: Validates input FASTA file integrity and calculates baseline metrics.
2. **Prokka**: Performs structural and functional annotation (Generates `.faa` and `.gbk` for downstream tools).
3. **CheckM2 / BUSCO**: Assesses genome quality and completeness.
4. **Functional Modules**: Runs dbCAN and antiSMASH (using Prokka-generated files).
5. **Phylogeny / ANI**: Performs comparative genomic analyses.

## Parameter Management
Most tools are executed with standardized clinical/research parameters. Users can modify specific flags (e.g., CPU allocation, database paths) through the GUI interface, which are then passed to the container runtime via PowerShell orchestration scripts included in the 'scripts' directory.
