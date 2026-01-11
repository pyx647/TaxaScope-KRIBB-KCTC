# TaxaScope Installation and Setup Guide

TaxaScope is designed to be a "Zero-Install" bioinformatics platform for the Windows environment. It leverages WSL2 and Podman to provide a consistent analysis environment without requiring manual installation of bioinformatics software on the host OS.

## System Requirements
- **OS**: Windows 10 (Build 19041+) or Windows 11(recommended).
- **CPU**: 4+ Cores recommended.
- **RAM**: 16GB+ (32GB+ recommended for antiSMASH/CheckM2).
- **Disk**: 50GB+ free space (for Docker images and databases).

## Installation Steps (One-Click Setup)
1. **Download**: Obtain the latest `TaxaScope_KRIBB_KCTC_v1.1.exe` from the official release page.
2. **First Run**: Launch the application.
3. **Environment Setup**:
   - Click the **"Env Setup"** button in the GUI.
   - The software will automatically:
     - Enable Windows WSL2 features (requires restart).
     - Install Podman (Container Desktop).
     - Configure the internal VM resources.
4. **Import Images (Optional/Offline)**:
   - If you have downloaded the `.tar` image packs, use the **"Import Images"** button. Otherwise, tools will automatically pull from Docker Hub on first use.

## Verification for Reviewers
To verify the installation:
1. Run the **"Genome Stats"** module on the provided example FASTA file.
2. If the progress bar completes and results appear in the "Preview" tab, the local Python environment is functional.
3. Run **"Prokka"** to verify the container runtime is correctly configured.
