# Data

This repository does not include raw TCGA methylation data.

To reproduce the analysis:

1. Visit the GDC Data Portal.
2. Download TCGA-BRCA DNA Methylation Beta Values.
3. Platform: Illumina Human Methylation 450.
4. Workflow: SeSAMe methylation beta estimation.
5. Place downloaded files inside:

data/
├── normal/
└── tumor/

# Download >5gb data using CLI

# Download the menifest.txt file for your selected datasets

1. wget https://gdc.cancer.gov/system/files/public/file/gdc-client_2.3_Ubuntu_x64-py3.8-ubuntu-20.04.zip
2. unzip gdc-client_2.3_Ubuntu_x64-py3.8-ubuntu-20.04.zip
3. unzip gdc-client_2.3_Ubuntu_x64.zip
4. chmod +x gdc-client
5. ./gdc-client --version
6. Download the gdc menifest.txt file
7. mkdir -p TCGA_tumor_beta_files
8. ./gdc-client download -m gdc_manifest.txt -d TCGA_tumor_beta_files
