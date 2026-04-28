# TaxaScope User Manual

TaxaScope is a Windows desktop GUI for microbial genome analysis. It wraps containerized bioinformatics tools, working-directory management, database tracking, batch execution, result preview, and reproducibility reporting into a single workflow.

This manual reflects the current TaxaScope GUI and local implementation. The main user path is:

```text
Open TaxaScope.exe
-> Env Setup
-> Select Work Directory
-> Download DBs
-> Get Data or add local files
-> configure modules
-> Batch
-> Deploy Complete Workflow
-> inspect Runtime, Console, Preview, and reports
```

## 1. System Requirements

Recommended environment:

- Windows 10 or Windows 11
- WSL2 enabled
- Podman, or Docker Desktop configured for Linux containers
- At least 16 GB RAM for small bacterial genome batches
- 32 GB RAM or higher for CheckM2, antiSMASH, PhyloPhlAn, and larger batch workflows
- Sufficient disk space for container images, reference databases, intermediate files, and output reports

TaxaScope uses Podman by default on Windows. Docker can be used as a fallback when Docker Desktop is installed and running.

## 2. First-Time Setup

### 2.1 Start TaxaScope

Run `TaxaScope.exe`. The upper control bar contains the buttons used to initialize and manage the environment:

- `Env Setup`: installs or initializes the WSL2 and container execution environment.
- `Env Ready`: shown when TaxaScope detects that the execution environment is available.
- `Win10 WSL2`: shown only on Windows 10 when the WSL2 helper setup is needed.
- `VM Config`: adjusts or recreates the Podman VM when memory, CPU allocation, or VM repair is needed.
- `Low Perf Mode`: reduces resource usage for memory-limited machines.

### 2.2 Install the Environment

On first use, click `Env Setup`.

Windows 10 users may also see a `Win10 WSL2` button. Use it when WSL2 kernel support or required Windows features are not yet enabled. After WSL2 setup, reboot the computer. After the computer restarts, open TaxaScope again and confirm that the button changes to `Env Ready`.

Do not use `VM Config` as the normal first step. Use it only when Podman was installed manually, the VM needs more memory or CPU, or the VM needs to be recreated.

## 3. Working Directory

Click `Select Work Directory` and choose a project folder. TaxaScope treats this folder as the source of truth for the whole analysis:

- input genome or protein files
- NCBI-downloaded assemblies and metadata
- reference databases
- intermediate files
- module-specific result folders
- final HTML, Markdown, and JSON reports

Recommended layout:

```text
project_folder/
|-- genome_1.fasta
|-- genome_2.fasta
|-- metadata.json
|-- TaxaScope_Databases/
|   |-- database_sources.json
|   |-- DATABASE_SOURCES.md
|   |-- prokka/
|   |-- dbcan/
|   |-- busco/
|   |-- checkm2/
|   |-- antismash/
|   `-- phylophlan/
|-- genome_stats.xlsx
|-- 2026xxxx_Prokka_Results/
|-- 2026xxxx_checkm2_results/
|-- 2026xxxx_busco_results/
|-- 2026xxxx_dbCAN2_Results/
|-- 2026xxxx_antiSMASH_Results/
|-- 2026xxxx_phylophlan_results/
|-- 2026xxxx_ANI-AAI/
|-- .runtimes.json
|-- TaxaScope_Run_Manifest.json
|-- TaxaScope_Run_Report.md
`-- TaxaScope_Report.html
```

## 4. Database Setup

After selecting the working directory, click `Download DBs`. This downloads the reference databases into:

```text
<working directory>/TaxaScope_Databases
```

The database downloader records fixed source and version information in:

```text
TaxaScope_Databases/database_sources.json
TaxaScope_Databases/DATABASE_SOURCES.md
TaxaScope_Databases/LICENSE_CONFIRMATION.txt
```

These files are used by the reproducibility reports. Database download may take a long time because several databases are large.

The current database plan includes:

| Database | Used by | Current source/version recorded by TaxaScope |
| --- | --- | --- |
| Prokka database package | Prokka | Prokka v1.14.6 database package |
| dbCAN fixed bundle | dbCAN | `db_v5-2_9-13-2025` |
| BUSCO bacterial lineages | BUSCO | `bacteria_odb12.2025-05-14` and `bacteria_odb10.2024-01-08` |
| CheckM2 database | CheckM | Zenodo record 14897628 |
| antiSMASH databases | antiSMASH | standalone-lite 8.0.4 databases |
| PhyloPhlAn marker database | PhyloPhlAn | `phylophlan.tar` marker database |

If a module reports that a database is missing, return to the same working directory and run `Download DBs` again. Already completed databases are skipped when readiness markers are present.

## 5. Container Images and Offline Use

TaxaScope modules run through Podman or Docker-compatible container images. Users can choose either online image pulling or offline image import.

### 5.1 Offline Image Import

Use this route when the target computer has limited access to Docker Hub or international networks.

1. Prepare the exported image archive folder, usually named `BioToolkit_Images` or `TaxaScope_Images`, containing `.tar` image files.
2. Open TaxaScope.
3. Click `Import Images`.
4. Select the folder containing the image `.tar` files.
5. TaxaScope imports the images into Podman or Docker and writes progress to the `Console` tab.

### 5.2 Online Image Pulling

If the computer can access Docker Hub, manual image import is not required. When a module is executed and the required image is not available locally, TaxaScope attempts to pull the corresponding image automatically.

The first run of a module may therefore take longer because both container images and reference databases may need to be downloaded.

### 5.3 Image Export and Disk Cleanup

- `Export Images`: exports installed container images into `.tar` files for offline transfer to another computer.
- `Uninstall [tool name] (Free Space)`: removes a tool image from the local Podman/Docker image store. The tool can be used again later by re-importing or re-pulling the image.

### 5.4 Container Image Specifications

Table S1. Container image specifications for TaxaScope modules.

| Module | Tool version | Database version* | Container image (release tag) | Image digest (SHA256, linux/amd64) |
| --- | --- | --- | --- | --- |
| Prokka | 1.14.6 | v1.14.6 | `docker.io/pyx07/prokka:v1-nodb-release` | `sha256:6b0c6e6e8b330858c9764690ead2b9d8a4160109474c2401f6eddf2347fb4e82` |
| dbCAN | 4.2.0-rc2 | db_v5_2_9-13-2025 | `docker.io/pyx07/dbcan:v5-nodb-release` | `sha256:46e1790f026fa5a33f7d6a65c6c3c437b9122a59c2e46c62e79806db942c2dc7` |
| BUSCO | 5.8.2 | bacteria_odb12 (2025-05-14) | `docker.io/pyx07/busco:v5-nodb-release` | `sha256:c73e3c9a4b837ed7f216fc024721593ac44290d904d1567bb9582b7984158845` |
| CheckM2 | 1.1.0 | Zenodo record 14897628 | `docker.io/pyx07/checkm2:v2-nodb-release` | `sha256:c9a9ed455a39d26041b9a8d30edf144c02c7360190be8d06888edfb897c48134` |
| PhyloPhlAn | 3.0.67 | Zenodo record 4005620 | `docker.io/pyx07/phylophlan:v3-nodb-release` | `sha256:8cc55c91b5a79f2df4dba8be7128e00953bb298569d1c4a4225d599f12191277` |
| antiSMASH | 8.0.4 | standalone-lite 8.0.4 databases | `docker.io/pyx07/antismash:latest-nodb-release` | `sha256:864038983edb0c19caf45cbfcdf5bb01156da7aafb0ae73a27bbbce7e128234c` |

* External databases are not distributed inside the container images. They are downloaded into the selected working directory through `Download DBs`.

## 6. Input Data

TaxaScope accepts either local files or NCBI accession-based downloads.

### 5.1 NCBI Download

Open the `Get Data` tab and enter one GCA or GCF accession per line. The NCBI downloader can retrieve:

- genome sequences in FASTA format
- protein sequences in FAA format
- GenBank records in GBFF format
- annotation features in GFF3 format
- assembly data reports in JSON format

TaxaScope organizes downloaded files into the selected working directory and preserves NCBI metadata as `metadata.json` where available.

### 5.2 Local Files

Alternatively, place local files directly in the working directory before running modules.

| Module | Expected input | Notes |
| --- | --- | --- |
| Genome Stats | `.fasta`, `.fa`, `.fna` | Calculates assembly length, contigs, GC content, and N50. |
| Prokka | `.fasta`, `.fa`, `.fna` | Produces genome annotation and protein outputs. |
| CheckM | `.fasta`, `.fa`, `.fna` | Runs CheckM2 quality assessment. |
| BUSCO | `.fasta`, `.fa`, `.fna` | Runs bacterial lineage completeness assessment. |
| dbCAN | `.faa` | Uses protein FASTA. Run Prokka first or download FAA files from NCBI. |
| antiSMASH | `.fasta`, `.fa`, `.fna`, `.gbk`, `.gbff` | GenBank input is recommended when annotation is available. |
| PhyloPhlAn | `.faa` | Uses protein FASTA. At least five genomes are recommended. |
| AAI/ANI | `.fasta`, `.fa`, `.fna` | Computes genome similarity and heatmaps. |

## 7. GUI Panels

The main window is organized into three working areas:

- Left panel: `File Browser`. It shows the selected working directory. Click a file to preview it; click the folder label to open the folder in Windows Explorer.
- Center panel: module tabs. These include `Get Data`, `Genome Stats`, `Prokka`, `CheckM`, `BUSCO`, `dbCAN`, `antiSMASH`, `PhyloPhlAn`, `AAI/ANI`, and `Batch`.
- Right panel: `Runtime`, `Console`, and `Preview`.

The right panel is important for troubleshooting:

- `Runtime`: task status, progress, and elapsed time.
- `Console`: command-line logs from PowerShell, Podman, Docker, and tool wrappers.
- `Preview`: compatible results including images, SVG files, PDFs, text files, tables, Excel files, and Newick/tree files.

## 8. Complete Analysis Workflow

This is the recommended end-to-end workflow for a typical bacterial genome project.

### Step 1. Open the Software

Run `TaxaScope.exe`. If the environment is not configured, click `Env Setup`. Wait until the interface reports `Env Ready`.

### Step 2. Select a Project Folder

Click `Select Work Directory` and choose the folder for this analysis. Do not scatter inputs and outputs across multiple locations; TaxaScope expects the working directory to contain the data, databases, outputs, and reports.

### Step 3. Download Databases

Click `Download DBs`. Confirm the license notice and allow the downloader to populate `TaxaScope_Databases`.

This step is usually performed once for a working directory. The database folder can be reused by copying `TaxaScope_Databases` into another project folder.

### Step 4. Add Genome Data

Use one of two routes:

- For NCBI data, open `Get Data`, paste GCA/GCF accessions, choose the desired file types, and click `Start Download`.
- For local data, copy `.fasta`, `.fa`, `.fna`, `.faa`, `.gbk`, or `.gbff` files into the working directory.

### Step 5. Configure Module Parameters

Open module tabs and adjust settings before execution.

Important examples:

- `dbCAN`: select at least two methods such as HMMER, DIAMOND, and dbCAN-S for more reliable CAZyme prediction.
- `antiSMASH`: select strictness and optional analyses carefully; some options increase memory usage.
- `Low Perf Mode`: enable this for systems with limited RAM, especially for antiSMASH and CheckM2.
- `PhyloPhlAn`: provide `.faa` files and ensure enough genomes are included for a meaningful tree.

### Step 6. Run Batch Mode

Open `Batch`. The Batch page has two functional areas:

- `Data Acquisition (Optional)`: paste GCA/GCF accessions if the workflow should download genomes before analysis.
- `Analysis Sequence Setup`: select modules to run sequentially.

Keep `Auto-generate Interactive HTML Research Report` enabled if an aggregated report is needed.

Click `DEPLOY COMPLETE WORKFLOW` to start the selected workflow. TaxaScope asks for confirmation and then runs modules sequentially.

### Step 7. Monitor and Inspect

During execution:

- use `Runtime` to check progress
- use `Console` to inspect command logs and errors
- use `File Browser` to see newly generated files
- use `Preview` to inspect plots, tables, reports, and tree files

After completion, review:

- `TaxaScope_Report.html`
- `TaxaScope_Run_Report.md`
- `TaxaScope_Run_Manifest.json`

## 9. Module Outputs

| Module | Main outputs |
| --- | --- |
| Genome Stats | `genome_stats.xlsx` |
| Prokka | `*_Prokka_Results/`, sample-level GFF/GBK/FNA/FAA files, `final_result.tsv`, merged Excel tables, genome circle plots |
| CheckM | `*_checkm2_results/`, `quality_report.tsv`, `CheckM_Plot.svg` |
| BUSCO | `*_busco_results/`, short summaries, `busco_summary_report_v2.svg`, `busco_summary_report_v2.png` |
| dbCAN | `*_dbCAN2_Results/`, overview files, merged Excel results, `dbCAN_HMMER_Summary.svg`, `dbCAN_DIAMOND_Summary.svg` |
| antiSMASH | `*_antiSMASH_Results/`, antiSMASH HTML/JSON outputs, summary plots when available |
| PhyloPhlAn | `*_phylophlan_results/`, tree files such as `.contree`, `.treefile`, `.tre`, `.nwk`, and optional RAxML bootstrap trees |
| AAI/ANI | `*_ANI-AAI/`, ANI and AAI tables, heatmap SVG/PNG files |

## 10. Reproducibility Reports

TaxaScope writes structured run metadata for reproducible taxonomy workflows.

### `TaxaScope_Run_Manifest.json`

Machine-readable manifest containing:

- TaxaScope version
- working directory
- database root
- database source records
- operating system and runtime information
- tool names and software versions
- container images
- parameters
- timestamps and duration
- input files
- detected output files
- run status

### `TaxaScope_Run_Report.md`

Human-readable Markdown summary containing the same provenance information. This file is suitable for supplementary materials, internal records, and reviewer responses.

### `TaxaScope_Report.html`

Interactive HTML report aggregating result tables, plots, module outputs, runtime summaries, and a reproducibility section. Timestamped HTML copies may also be created during report generation, while `TaxaScope_Report.html` is the stable latest report name.

## 11. Exiting TaxaScope

When closing TaxaScope, the software asks whether WSL backends should be shut down.

- Choose `Yes` to run `wsl --shutdown`. This releases memory used by WSL and Podman, but the next TaxaScope startup may take longer because the VM must start again.
- Choose `No` to close only the GUI. WSL and Podman remain running in the background, which makes the next startup faster.
- Choose `Cancel` to return to the application.

During a running task, use the red `Stop Current Task` button at the bottom of the GUI if a module becomes unresponsive. This attempts to stop the current process and associated containers.

## 12. Troubleshooting

### `Env Ready` does not appear

Start Podman or Docker Desktop and reopen TaxaScope. If Podman was installed manually or the VM is broken, use `VM Config`.

### A module says the database is missing

Confirm that the selected working directory contains `TaxaScope_Databases`. Then click `Download DBs` again. Confirm that `database_sources.json` and the relevant database subfolder exist.

### No files are detected

Confirm that the selected working directory contains files with supported extensions. For dbCAN and PhyloPhlAn, `.faa` protein files are required.

### NCBI download fails

Try a smaller accession batch, for example 5 to 8 genomes. NCBI bundle generation can fail or return invalid ZIP archives during busy periods.

### A module fails because of memory

Enable `Low Perf Mode`, reduce the number of input genomes, or increase the Podman VM memory allocation through `VM Config`.

### Cannot connect to Podman

This usually means the Podman VM or WSL backend is not running. Reopen TaxaScope, click `VM Config`, or restart the computer. On Windows 10, complete the `Win10 WSL2` setup if the button is shown.

### Disk space is low

Container images and reference databases can be large. Remove unused images with `Uninstall [tool name] (Free Space)` from the relevant module tab, or move old working directories and database folders to external storage.

### The software freezes during analysis

Click `Stop Current Task`. If the GUI cannot recover, close TaxaScope and choose `Yes` when asked to shut down WSL backends.

### PhyloPhlAn tree files are confusing

TaxaScope may produce several tree outputs. IQ-TREE `.treefile` labels can contain SH-aLRT/UFBoot paired support values, while `.contree` is preferred when bootstrap-only support labels are needed. Optional RAxML bootstrap output may also be exported when the concatenated alignment is available.

## 13. Reviewer-Facing Statement

The following wording can be adapted for manuscript revision or reviewer response:

```text
A GitHub-accessible TaxaScope user manual and multilingual HTML guide were updated to provide a complete end-to-end workflow. The documentation now describes first-time environment setup, working directory selection, one-click database download with database source manifests, NCBI or local input preparation, module parameter configuration, batch workflow execution, result inspection, output directory structure, and HTML/Markdown/JSON reproducibility reports containing software, database, parameter, timestamp, input, and output metadata.
```
