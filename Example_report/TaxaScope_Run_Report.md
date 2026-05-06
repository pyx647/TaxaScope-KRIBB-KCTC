# TaxaScope KRIBB-KCTC Pro — Run Report

| | |
| :--- | :--- |
| **Version** | 1.5 |
| **Work directory** | E:\Experimental_data\Published\taxascope manuscript\taxascope_test_data\test |
| **Database root** | E:\Experimental_data\Published\taxascope manuscript\taxascope_test_data\test\TaxaScope_Databases |
| **Report generated** | 2026-05-06T17:08:17+09:00 |

---

## Run Overview

| # | Module | Status | Duration | Input files | Output |
| :-: | :--- | :---: | ---: | ---: | :--- |
| 1 | **Genome Stats** | ✅ Completed | 3.7 s | 6 | — |
| 2 | **Prokka** | ✅ Completed | 1 h 21 min | 6 | 20260506_1436_prokka_* (1 folders) |
| 3 | **CheckM** | ✅ Completed | 4 min 31 s | 6 | 20260506_1558_checkm2_results |
| 4 | **BUSCO** | ✅ Completed | 2 min 7 s | 6 | 20260506_1602_busco_results |
| 5 | **dbCAN** | ✅ Completed | 8 min 50 s | 6 | 20260506_1605_dbCAN2_Results |
| 6 | **antiSMASH** | ✅ Completed | 12 min 57 s | 6 | 20260506_1613_antiSMASH_Results |
| 7 | **PhyloPhlAn** | ✅ Completed | 30 min 59 s | 6 | 20260506_1626_phylophlan_results (+1) |
| 8 | **AAI/ANI** | ✅ Completed | 10 min 27 s | 6 | 20260506_1657_ANI-AAI |

---

## Run Details

### 1. Genome Stats ✅

| Field | Value |
| :--- | :--- |
| Software | TaxaScope Genome Stats 1.5 |
| Database version | Not applicable |
| Container image | — |
| Input files | 6 |
| Started | 2026-05-06T14:36:21+09:00 |
| Finished | 2026-05-06T14:36:25+09:00 |
| Duration | 3.7 s |
| Output files | 2 |
| Result folders | — |
| Parameters | batch_mode = True |

### 2. Prokka ✅

| Field | Value |
| :--- | :--- |
| Software | Prokka 1.14.6 |
| Database version | v1.14.6 |
| Container image | docker.io/pyx07/prokka:v1-nodb-release |
| Input files | 6 |
| Started | 2026-05-06T14:36:25+09:00 |
| Finished | 2026-05-06T15:58:20+09:00 |
| Duration | 1 h 21 min |
| Output files | 146 |
| Result folders | 20260506_1436_prokka_* (1 folders) |
| Parameters | batch_mode = True |

### 3. CheckM ✅

| Field | Value |
| :--- | :--- |
| Software | CheckM2 1.1.0 |
| Database version | Zenodo record 14897628 |
| Container image | docker.io/pyx07/checkm2:v2-nodb-release |
| Input files | 6 |
| Started | 2026-05-06T15:58:21+09:00 |
| Finished | 2026-05-06T16:02:53+09:00 |
| Duration | 4 min 31 s |
| Output files | 13 |
| Result folders | 20260506_1558_checkm2_results |
| Parameters | batch_mode = True  
LowPerf = false |

### 4. BUSCO ✅

| Field | Value |
| :--- | :--- |
| Software | BUSCO 5.8.2 |
| Database version | bacteria_odb12 (2025-05-14) |
| Container image | docker.io/pyx07/busco:v5-nodb-release |
| Input files | 6 |
| Started | 2026-05-06T16:02:53+09:00 |
| Finished | 2026-05-06T16:05:00+09:00 |
| Duration | 2 min 7 s |
| Output files | 2213 |
| Result folders | 20260506_1602_busco_results |
| Parameters | batch_mode = True |

### 5. dbCAN ✅

| Field | Value |
| :--- | :--- |
| Software | dbCAN 4.2.0-rc2 |
| Database version | db_v5_2_9-13-2025 |
| Container image | docker.io/pyx07/dbcan:v5-nodb-release |
| Input files | 6 |
| Started | 2026-05-06T16:05:00+09:00 |
| Finished | 2026-05-06T16:13:51+09:00 |
| Duration | 8 min 50 s |
| Output files | 30 |
| Result folders | 20260506_1605_dbCAN2_Results |
| Parameters | batch_mode = True  
DbMethods = hmmer,diamond |

### 6. antiSMASH ✅

| Field | Value |
| :--- | :--- |
| Software | antiSMASH 8.0.4 |
| Database version | standalone-lite 8.0.4 databases |
| Container image | docker.io/pyx07/antismash:latest-nodb-release |
| Input files | 6 |
| Started | 2026-05-06T16:13:52+09:00 |
| Finished | 2026-05-06T16:26:49+09:00 |
| Duration | 12 min 57 s |
| Output files | 979 |
| Result folders | 20260506_1613_antiSMASH_Results |
| Parameters | batch_mode = True  
Strictness = relaxed  
cb_knownclusters = true  
cb_general = false  
cb_subclusters = false  
cc_mibig = true  
asf = true  
rre = true  
… 4 more parameters |

### 7. PhyloPhlAn ✅

| Field | Value |
| :--- | :--- |
| Software | PhyloPhlAn 3.0.67 |
| Database version | Zenodo record 4005620 |
| Container image | docker.io/pyx07/phylophlan:v3-nodb-release |
| Input files | 6 |
| Started | 2026-05-06T16:26:50+09:00 |
| Finished | 2026-05-06T16:57:49+09:00 |
| Duration | 30 min 59 s |
| Output files | 0 |
| Result folders | 20260506_1626_phylophlan_results, 44/20260430_2256_phylophlan_results |
| Parameters | batch_mode = True |

### 8. AAI/ANI ✅

| Field | Value |
| :--- | :--- |
| Software | pyANI (ANIb) / EzAAI pyANI 0.3.0-alpha; EzAAI 1.2.4 |
| Database version | Not applicable |
| Container image | docker.io/pyx07/aanani:latest |
| Input files | 6 |
| Started | 2026-05-06T16:57:49+09:00 |
| Finished | 2026-05-06T17:08:17+09:00 |
| Duration | 10 min 27 s |
| Output files | 6 |
| Result folders | 20260506_1657_ANI-AAI |
| Parameters | batch_mode = True |

> Full commands and detailed file lists are recorded in `TaxaScope_Run_Manifest.json`.

---

## Software Environment

| Component | Version |
| :--- | :--- |
| Platform | Windows-11-10.0.26200-SP0 |
| Python Version | 3.13.13 |
| Powershell Version | 5.1.26100.7920 |
| Wsl Version | WSL version: 2.6.1.0 \| Kernel version: 6.6.87.2-1 \| WSLg version: 1.0.66 \| MSRDC version: 1.2.6353 \| Direct3D version: 1.611.1-81528511 \| DXCore version: 10.0.26100.1-240331-1435.ge-release \| Windows version: 10.0.26200.8039 |
| Podman Version | podman version 5.7.0 |

---

## Module Reference Versions

| Module | Tool version | Database version |
| :--- | :--- | :--- |
| Prokka | 1.14.6 | v1.14.6 |
| dbCAN | 4.2.0-rc2 | db_v5_2_9-13-2025 |
| BUSCO | 5.8.2 | bacteria_odb12 (2025-05-14) |
| CheckM | 1.1.0 | Zenodo record 14897628 |
| PhyloPhlAn | 3.0.67 | Zenodo record 4005620 |
| antiSMASH | 8.0.4 | standalone-lite 8.0.4 databases |
| Genome Stats | 1.5 | Not applicable |
| AAI/ANI | pyANI 0.3.0-alpha; EzAAI 1.2.4 | Not applicable |

---

## Methods

> The following descriptions are provided to assist with manuscript preparation.
> Copy and adapt the relevant paragraphs for your Methods section.

### Genome Statistics

Basic genome statistics (total length, GC content, N50, number of contigs) were computed for all 6 genome assemblies using the built-in Genome Stats module of TaxaScope v1.5.

### Genome Annotation (Prokka)

Genome annotation was performed using Prokka v1.14.6 (Seemann, 2014) for all 6 genome assemblies. Prokka was executed via the container image `docker.io/pyx07/prokka:v1-nodb-release` with default parameters (kingdom: Bacteria, genetic code 11). Output files include GFF3 annotation, GenBank format, protein FASTA (.faa), and a summary statistics table.

### Genome Completeness Assessment (BUSCO)

Genome completeness was assessed using BUSCO v5.8.2 (Manni et al., 2021) with the `bacteria_odb12` lineage dataset ((2025-05-14)). BUSCO was run in genome mode (`--mode genome`) for all 6 assemblies via the container image `docker.io/pyx07/busco:v5-nodb-release`. Completeness is reported as percentages of complete single-copy (C/S), complete duplicated (C/D), fragmented (F), and missing (M) BUSCOs.

### Genome Quality Assessment (CheckM2)

Genome quality (completeness and contamination) was evaluated using CheckM2 v1.1.0 (Chklovski et al., 2023) with the reference database from Zenodo record 14897628. CheckM2 was executed for all 6 genome bins via the container image `docker.io/pyx07/checkm2:v2-nodb-release` using the default diamond-based workflow.

### Carbohydrate-Active Enzyme Annotation (dbCAN)

Carbohydrate-active enzyme (CAZyme) annotation was performed using dbCAN v4.2.0-rc2 (Zhang et al., 2018; Zheng et al., 2023) with the CAZyme database version `db_v5_2_9-13-2025`. Three complementary methods were applied simultaneously: HMMER-based domain search (dbCAN-HMM), DIAMOND-based BLAST search (dbCAN-DIAMOND), and dbCAN-sub signature search. CAZyme families were annotated for 6 proteome(s) via the container image `docker.io/pyx07/dbcan:v5-nodb-release`.

### Secondary Metabolite Biosynthetic Gene Cluster Prediction (antiSMASH)

Secondary metabolite biosynthetic gene clusters (BGCs) were identified using antiSMASH v8.0.4 (Blin et al., 2023) with the standalone-lite database (standalone-lite 8.0.4 databases). Analysis was performed for 6 genome(s) via the container image `docker.io/pyx07/antismash:latest-nodb-release` with default parameters (`--genefinding-tool prodigal`). Detected BGC types include NRPS, PKS, terpene, siderophore, and others.

### Whole-Genome Phylogenetic Tree Reconstruction (PhyloPhlAn)

Whole-genome phylogenetic trees were constructed using PhyloPhlAn v3.0.67 (Asnicar et al., 2020) with the PhyloPhlAn marker database (Zenodo record 4005620). Protein sequences from 6 genome(s) were mapped against the marker database using DIAMOND (`--diversity medium`), aligned with MAFFT, and trimmed with trimAl. Phylogenetic inference was performed with IQ-TREE using the LG+G4 substitution model, 100 standard non-parametric bootstrap replicates (`-b 100`), and SH-aLRT branch support test with 1000 replicates (`-alrt 1000`). Bootstrap support values shown on the tree are true non-parametric bootstrap percentages (0–100%). All analyses were executed via the container image `docker.io/pyx07/phylophlan:v3-nodb-release`.

### Average Nucleotide Identity and Average Amino Acid Identity (ANI/AAI)

Average Nucleotide Identity (ANI) was calculated using pyANI v0.3.0-alpha (Pritchard et al., 2016) with the ANIb method (BLAST-based). Average Amino Acid Identity (AAI) was calculated using EzAAI v1.2.4 (Kim et al., 2021). All pairwise ANI and AAI comparisons were performed among 6 genome(s) via the container image `docker.io/pyx07/aanani:latest`. Species boundary thresholds of ANI ≥ 95% and AAI ≥ 95% were applied for species delineation.

---

*This report was generated automatically by TaxaScope. For complete provenance data including full command lines and file lists, see `TaxaScope_Run_Manifest.json`.*
