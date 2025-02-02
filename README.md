---
title: "Sample Document"
author: "Author Name"
date: "2025-02-01"
---

---

```
 ▄▄▄▄▄▄▄▄▄▄▄  ▄▄        ▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄  ▄▄▄▄▄▄▄▄▄▄▄ 
▐░░░░░░░░░░░▌▐░░▌      ▐░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌
▐░█▀▀▀▀▀▀▀▀▀ ▐░▌░▌     ▐░▌▐░█▀▀▀▀▀▀▀▀▀ ▐░█▀▀▀▀▀▀▀█░▌▐░█▀▀▀▀▀▀▀█░▌
▐░▌          ▐░▌▐░▌    ▐░▌▐░▌          ▐░▌       ▐░▌▐░▌       ▐░▌
▐░▌          ▐░▌ ▐░▌   ▐░▌▐░█▄▄▄▄▄▄▄▄▄ ▐░█▄▄▄▄▄▄▄█░▌▐░█▄▄▄▄▄▄▄█░▌
▐░▌          ▐░▌  ▐░▌  ▐░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌▐░░░░░░░░░░░▌
▐░▌          ▐░▌   ▐░▌ ▐░▌▐░█▀▀▀▀▀▀▀▀▀ ▐░█▀▀▀▀▀▀▀▀▀ ▐░█▀▀▀▀▀▀▀▀▀ 
▐░▌          ▐░▌    ▐░▌▐░▌▐░▌          ▐░▌          ▐░▌          
▐░█▄▄▄▄▄▄▄▄▄ ▐░▌     ▐░▐░▌▐░█▄▄▄▄▄▄▄▄▄ ▐░▌          ▐░▌          
▐░░░░░░░░░░░▌▐░▌      ▐░░▌▐░░░░░░░░░░░▌▐░▌          ▐░▌          
 ▀▀▀▀▀▀▀▀▀▀▀  ▀        ▀▀  ▀▀▀▀▀▀▀▀▀▀▀  ▀            ▀           
```                                                                 


# cNePP  
## Overview
### **Pipeline Name and Purpose**  

#### **Pipeline Name**:  
Neoantigen Prediction and Data Processing Pipeline  

#### **Purpose**:  

This repository contains a comprehensive pipeline for immuno-oncology neoepitope multipe feature analysis. The pipeline automates various tasks, from preparing data folders to processing and analyzing genomic data, including SNV (Single Nucleotide Variants), indels (insertions and deletions), fusions, HLA (Human Leukocyte Antigen) typing, neoantigen prediction, and more. It supports different types of genomic data and various steps in the analysis process.

This pipeline is designed for **neoepitope discovery** in cancer research. Its primary objectives include:  
- Integrating HLA typing, SNV analysis, expression data.  
- Identifying neoantigens rankings using advanced tools like NetMHCpan/netMHCIIpan/netMHCpanstab.  
- Performing fusion predictions to downstream neoepitope prediction.  
- Performing LOH analysis/CGI/hydrophibicity to downstream neoepitope prediction.  
- Preparing results in a user-friendly format (e.g., XLSX) for public sharing or further research.  
- Supporting clinical and research applications through robust workflows and modular execution of steps.  

### Features

    HLA typing: Process and analyze HLA typing data.
    SNV/Indel/Fusion: Analyze single nucleotide variants, indels, and fusion genes.
    Neoantigen Prediction: Predict potential neoantigens from genomic data.
    Excel Output: Convert results into XLSX format for easy reporting and sharing.
    Flexible Configuration: Customize various options like run IDs, steps, data type, and more via command-line arguments.

## Prerequisites

    Bash shell
    Access to the necessary genomic data files
    Required dependencies for each step of the pipeline (see individual steps below)

#### **System Requirements**  
To successfully run this pipeline, ensure the following system requirements are met:  
- **Operating System**: Linux/Unix-based system (preferred for compatibility with bioinformatics tools).  
- **Python Version**: Python 3.6 or above.  
- **Memory**: Minimum 16 GB of RAM (recommended: 32 GB or more for large datasets).  
- **Storage**: At least 50 GB of available disk space for intermediate files and results.  
- **Dependencies**:  
  - NetMHCpan (e.g., versions like `netMHCpan4_1`, `netMHCstabpan`) installed and configured.  
  - Required Python libraries (can be installed via `pip`): pandas, numpy, matplotlib, etc.  
  - STAR, Arriba, and other bioinformatics tools based on selected pipeline steps.  

## **Pipeline Workflow**  
The pipeline processes data step-by-step based on the selected options (`-s steps`). Below is the general workflow:  

- **Preparation**:  
   - **`s0`**: Set up folders and initialize the environment.  

- **HLA Typing**:  
   - **`s1a_HLA`**: Perform HLA typing (step 1a) in an older version.  
   - **`s1b_HLA`**: Perform HLA typing (step 1b).  

- **Variant Analysis**:  
   - **`s2_snv`**: Single Nucleotide Variant (SNV) based neoepitope prediction.  
   - **`i4a_indel_predict, i4b`**: Indel based neoepitope prediction.  

- **Expression Data Integration**:  
   - **`s3_add_expression`**: Add expression data to the analysis.  

- **Fusion Detection**:  
   - **`f1a`**: Run STAR and Arriba to detect gene fusions.  

- **Neoantigen Prediction**:  
   - **`f1-f4`**: fusion mutation calling and fusion based neoantigens prediction.  

- **Additional Predictions**:  
   - **`f5`**: Convert data to XLSX format for downstream analysis.  
   
- **Data Filtering and Formatting**:  
   - **`s8a_filter`**: Filter processed data.  
   - **`s8b_xlsx_to_public`**: Convert filtered data to a public format (e.g., XLSX).  


---
## Usage
To run the pipeline, use the following command:
bash <script_name>.sh -r <runID> -s <steps> [additional options]


## Options

    -r runID: Unique identifier for the run.
    -e netMHCpanID: NetMHCpan version (e.g., netMHCpan4_1, netMHCstabpan).
    -p patientID: Patient identifier, defaults to the value of runID if not provided.
    -t tcga: TCGA data type (e.g., RNAseq, TCGA-READ).
    -s steps: Specify the pipeline steps to execute. The available steps include:
        s0: Prepare folder
        s1a_HLA: HLA typing step 1a
        s1b_HLA: HLA typing step 1b
        s2_snv: SNV analysis
        s3_add_expression: Add expression data
        s8a_filter: Filter data
        s8b_xlsx_to_public: Convert data to public format
        i4a_indel_predict: Indel prediction
        f1a: Run STAR and Arriba (fusion detection)
        f2: Prepare HLA data
        f3: Neoantigen prediction
        f4: MER21 prediction
        f5: Convert to XLSX format
        More steps listed in the script.
    -d debug: Enable debug mode for troubleshooting.
    -h hlaID: Specify the HLA ID (e.g., NCT_IP for internal patient data).
    -a dataType: Specify the data type (e.g., RNAbamOpt).
    -c cgiTumorType: Specify the tumor type (e.g., CANCER).
    -b vcfOnly: Process only VCF files (e.g., origin, pathology, promise).
    -w wg: Data type (e.g., wes for exome sequencing, wgs for whole-genome sequencing).
    -o logDir: Directory to store log files.
    -l merlength: Set the MER length (e.g., 21, 27).




# **Pipeline Parameters and Configuration**

This section explains the parameters of the pipeline in detail, providing default values, valid options, and usage examples.

| **Parameter**      | **Description**                                                                                                  | **Default Value**     | **Example**                       |
|---------------------|------------------------------------------------------------------------------------------------------------------|-----------------------|-----------------------------------|
| `-r runID`          | Unique identifier for the run.                                                                                  | **(Required)**        | `-r run123`                      |
| `-e netMHCpanID`    | Specifies the NetMHCpan version to use for neoepitope prediction.                                               | **(Required)**        | `-e netMHCpan4_1`                |
| `-p patientID`      | Patient identifier. Defaults to the value of `runID` if not provided.                                           | `runID`               | `-p patient001`                  |
| `-t tcga`           | TCGA data type (e.g., RNAseq, TCGA-READ).                                                                       | None                  | `-t RNAseq`                      |
| `-s steps`          | Specifies the pipeline steps to execute. Steps include:                                                        | **(Required)**        | `-s s0,s1a_HLA,s3_add_expression` |
|                     | - `s0`: Prepare folder                                                                                         |                       |                                   |
|                     | - `s1a_HLA`: HLA typing step 1a                                                                                 |                       |                                   |
|                     | - `s1b_HLA`: HLA typing step 1b                                                                                 |                       |                                   |
|                     | - `s2_snv`: SNV analysis                                                                                        |                       |                                   |
|                     | - `s3_add_expression`: Add expression data                                                                      |                       |                                   |
|                     | - `s8a_filter`: Filter data                                                                                     |                       |                                   |
|                     | - `s8b_xlsx_to_public`: Convert data to public format                                                           |                       |                                   |
|                     | - `i4a_indel_predict`: Indel prediction                                                                         |                       |                                   |
|                     | - `f1a`: Run STAR and Arriba (fusion detection)                                                                 |                       |                                   |
|                     | - `f2`: Prepare HLA data                                                                                        |                       |                                   |
|                     | - `f3`: Neoantigen prediction                                                                                   |                       |                                   |
|                     | - `f4`: MER21 prediction                                                                                        |                       |                                   |
|                     | - `f5`: Convert to XLSX format                                                                                  |                       |                                   |
| `-d debug`          | Enables debug mode for troubleshooting.                                                                         | Disabled              | `-d`                             |
| `-h hlaID`          | Specifies the HLA ID (e.g., NCT_IP for internal patient data).                                                  | None                  | `-h NCT_IP`                      |
| `-a dataType`       | Specifies the data type (e.g., RNAbamOpt).                                                                      | None                  | `-a RNAbamOpt`                   |
| `-c cgiTumorType`   | Specifies the tumor type (e.g., CANCER).                                                                        | None                  | `-c CANCER`                      |
| `-b vcfOnly`        | Processes only VCF files (e.g., origin, pathology, promise).                                                    | None                  | `-b origin`                      |
| `-w wg`             | Specifies the data type for sequencing (e.g., `wes` for whole-exome sequencing, `wgs` for whole-genome sequencing). | None                  | `-w wes`                         |
| `-o logDir`         | Directory to store log files.                                                                                   | `./logs`              | `-o /path/to/logs`               |
| `-l merlength`      | Sets the MER length (e.g., 21, 27).                                                                             | 21                    | `-l 21`                          |

---

## **Usage Example**

This will run the pipeline with the specified steps: preparing the folder, processing HLA data (step s1b), SNV analysis, and converting the results to public XLSX format. Debug mode is enabled, and the output will be logged.

Here’s how the pipeline can be executed using the above parameters:
```bash
bash all_in_one_pipeline.sh \
  -r run123 \
  -e netMHCpan4_1 \
  -p patient001 \
  -t RNAseq \
  -s s0,s1a_HLA,s2_snv,s3_add_expression \
  -d \
  -h NCT_IP \
  -a RNAbamOpt \
  -c CANCER \
  -b origin \
  -w wes \
  -o ./logs \
  -l 21
```

---
## License

This project is licensed under the GNU3.0 License - see the LICENSE file for details.
Contact

For questions or issues, please contact the project maintainers or open an issue in this repository.

This README provides a comprehensive guide on how to use the pipeline, the available steps, and how to configure and run the analysis with different parameters.


--- 
## intermidiate file structure
      .
      ├── 1_hla_type
      │   ├── cgi
      │   │   ├── alterations.tsv
      │   │   ├── biomarkers.tsv
      │   │   ├── input01.tsv
      │   │   └── summary.txt
      │   ├── cgi_HNSC_9a37b5ab9224f77ca9a7.log
      │   ├── control_IPNCT_P013521_merged.mdup.bam
      │   ├── format_hla
      │   ├── hla_sab_P013521
      │   │   ├── Kourami
      │   │   │   └── control_DNA
      │   │   │       ├── hla_sab_P013521.log
      │   │   │       ├── hla_sab_P013521.result
      │   │   │       └── hla_sab_P013521.result_formatted.tsv
      │   │   ├── MHCII_typing.tsv
      │   │   ├── MHCI_typing.tsv
      │   │   ├── netMHCII_input.txt
      │   │   ├── netMHCI_input.txt
      │   │   ├── Optitype
      │   │   │   └── control_DNA
      │   │   │       ├── 2024_04_24_11_41_10
      │   │   │       │   ├── 2024_04_24_11_41_10_coverage_plot.pdf
      │   │   │       │   └── 2024_04_24_11_41_10_result.tsv
      │   │   │       └── 2024_04_24_11_41_10_result_formatted.tsv
      │   │   ├── stdout_extract_reads_control_DNA_25734363
      │   │   ├── stdout_format_HLA_types_25741019
      │   │   ├── stdout_run_kourami_control_DNA_25735093
      │   │   └── stdout_run_optitype_control_DNA_25735092
      │   ├── mutation.csv
      │   ├── mutation_germline.csv
      │   └── mutation.tsv
      ├── 2_SNVs_based_neoepitope_prediction
      │   ├── 1.vcf
      │   ├── 2.vcf
      │   ├── 2.vcf.annovar
      │   ├── 2.vcf.annovar.exonic_variant_function
      │   ├── 2.vcf.annovar.exonic_variant_function_multiple
      │   ├── 2.vcf.annovar.invalid_input
      │   ├── 2.vcf.annovar.log
      │   ├── 2.vcf.annovar.variant_function
      │   ├── netMHCpan4_1
      │   │   ├── headerMHCI
      │   │   ├── headerMHCII
      │   │   ├── headerVCF
      │   │   ├── map_NM_geneName
      │   │   ├── mut.fa
      │   │   ├── mut.fa_15
      │   │   ├── mut.fa_8
      │   │   ├── netMHCI_HLA-A01:01_mut
      │   │   ├── netMHCI_HLA-A01:01_mut_reformat
      │   │   ├── netMHCI_HLA-A01:01_ref
      │   │   ├── netMHCI_HLA-A01:01_ref_reformat
      │   │   ├── netMHCI_HLA-A01:01_summary
      │   │   ├── netMHCI_HLA-A02:01_mut
      │   │   ├── netMHCI_HLA-A02:01_mut_reformat
      │   │   ├── netMHCI_HLA-A02:01_ref
      │   │   ├── netMHCI_HLA-A02:01_ref_reformat
      │   │   ├── netMHCI_HLA-A02:01_summary
      │   │   ├── netMHCI_HLA-B08:01_mut
      │   │   ├── netMHCI_HLA-B08:01_mut_reformat
      │   │   ├── netMHCI_HLA-B08:01_ref
      │   │   ├── netMHCI_HLA-B08:01_ref_reformat
      │   │   ├── netMHCI_HLA-B08:01_summary
      │   │   ├── netMHCI_HLA-B40:01_mut
      │   │   ├── netMHCI_HLA-B40:01_mut_reformat
      │   │   ├── netMHCI_HLA-B40:01_ref
      │   │   ├── netMHCI_HLA-B40:01_ref_reformat
      │   │   ├── netMHCI_HLA-B40:01_summary
      │   │   ├── netMHCI_HLA-C03:04_mut
      │   │   ├── netMHCI_HLA-C03:04_mut_reformat
      │   │   ├── netMHCI_HLA-C03:04_ref
      │   │   ├── netMHCI_HLA-C03:04_ref_reformat
      │   │   ├── netMHCI_HLA-C03:04_summary
      │   │   ├── netMHCI_HLA-C07:01_mut
      │   │   ├── netMHCI_HLA-C07:01_mut_reformat
      │   │   ├── netMHCI_HLA-C07:01_ref
      │   │   ├── netMHCI_HLA-C07:01_ref_reformat
      │   │   ├── netMHCI_HLA-C07:01_summary
      │   │   ├── netMHCII_DRB1_0301_mut
      │   │   ├── netMHCII_DRB1_0301_mut_reformat
      │   │   ├── netMHCII_DRB1_0301_ref
      │   │   ├── netMHCII_DRB1_0301_ref_reformat
      │   │   ├── netMHCII_DRB1_0301_summary
      │   │   ├── netMHCII_DRB1_1302_mut
      │   │   ├── netMHCII_DRB1_1302_mut_reformat
      │   │   ├── netMHCII_DRB1_1302_ref
      │   │   ├── netMHCII_DRB1_1302_ref_reformat
      │   │   ├── netMHCII_DRB1_1302_summary
      │   │   ├── predictedProtein.fa
      │   │   ├── ref.fa
      │   │   ├── ref.fa_15
      │   │   ├── ref.fa_8
      │   │   ├── results_MHCI_epitopes.tab
      │   │   ├── results_MHCI_epitopes.tab.hydro
      │   │   ├── results_MHCI_epitopes.tab.hydro_splitGenes
      │   │   ├── results_MHCI_epitopes.tab_splitGenes
      │   │   ├── results_MHCII_epitopes.tab
      │   │   ├── results_MHCII_epitopes.tab.hydro
      │   │   ├── results_MHCII_epitopes.tab.hydro_splitGenes
      │   │   └── results_MHCII_epitopes.tab_splitGenes
      │   ├── snvs_IPNCT_P013521_germline_functional_snvs_conf_8_to_10.vcf
      │   └── snvs_IPNCT_P013521_somatic_functional_snvs_conf_8_to_10.vcf
      ├── 3_add_expression
      │   ├── addRNA1
      │   ├── addRNA2
      │   ├── addRNA3
      │   ├── fpkm_COL6A3_exon6.txt
      │   ├── MHCI_epitopes_TCGA-HNSC_RNAseq_netMHCpan4_1.tab
      │   ├── MHCII_epitopes_TCGA-HNSC_RNAseq.tab
      │   ├── past
      │   │   ├── MHCI_epitopes_RNAseq_netMHCpan4_1.tab
      │   │   └── MHCII_epitopes_RNAseq.tab
      │   ├── tumor_IPNCT_P013521.fpkm_tpm.featureCounts.tsv
      │   ├── tumor_IPNCT_P013521_merged.mdup.bam
      │   └── tumor_IPNCT_P013521_merged.mdup.bam.bai
      ├── 4_indel_based_prediction
      │   ├── indel_IPNCT_P013521_germline_functional_indels_conf_8_to_10.vcf
      │   ├── indel_IPNCT_P013521_somatic_functional_indels_conf_8_to_10.vcf
      │   └── result
      ├── 5_LOHHLA
      │   ├── data
      │   │   ├── example.patient.hlaFasta.fa
      │   │   ├── hlas
      │   │   └── HLAs
      │   ├── example-file
      │   │   └── bam
      │   └── example-out
      │       ├── Figures
      │       ├── running.hla.loh.exome@Mon_May_13_11-42-49_2024_log.txt
      │       ├── running.hla.loh.exome@Wed_Apr_24_16-26-50_2024_log.txt
      │       ├── running.hla.loh.exome@Wed_Apr_24_16-52-35_2024_log.txt
      │       └── running.hla.loh.exome@Wed_Dec_18_10-53-56_2024_log.txt
      ├── 8_chose_neoepitode
      │   ├── MHCI_epitopes_TCGA-HNSC_RNAseq_netMHCpan4_1.tab
      │   ├── MHCI_epitopes_TCGA-HNSC_RNAseq_netMHCpan4_1.tab_renameCol
      │   ├── MHCI_epitopes_TCGA-HNSC_RNAseq_netMHCpan4_1.tab_renameCol_wish
      │   ├── MHCII_epitopes_TCGA-HNSC_RNAseq.tab
      │   ├── MHCII_epitopes_TCGA-HNSC_RNAseq.tab_renameCol
      │   ├── MHCII_epitopes_TCGA-HNSC_RNAseq.tab_renameCol_wish
      │   └── wish_list_genes_expression.csv
      ├── 9_Fusion_gene_based_neoepitope_identification
      │   ├── 2_arriba_result_RNAbamOpt
      │   │   ├── fusions.discarded.tsv
      │   │   ├── fusions.tsv
      │   │   ├── fusions.tsv_splitGenes
      │   │   ├── netMHCII_input.txt
      │   │   └── netMHCI_input.txt
      │   └── 3_neoPrediction_RNAbamOpt
      │       ├── MHCI_filtered
      │       ├── MHCII_filtered
      │       ├── MHCII_reformat
      │       ├── MHCI_reformat
      │       ├── netMHCI_HLA-A01:01_fusion
      │       ├── netMHCI_HLA-A02:01_fusion
      │       ├── netMHCI_HLA-B08:01_fusion
      │       ├── netMHCI_HLA-B40:01_fusion
      │       ├── netMHCI_HLA-C03:04_fusion
      │       ├── netMHCI_HLA-C07:01_fusion
      │       ├── netMHCII_DQA1_0102_fusion
      │       ├── netMHCII_DQB1_0201_fusion
      │       ├── netMHCII_DQB1_0604_fusion
      │       ├── netMHCII_DRB1_0301_fusion
      │       ├── netMHCII_DRB1_1302_fusion
      │       ├── peptides_for_binding_prediction.fa
      │       ├── peptides_for_binding_prediction.fa_15
      │       ├── peptides_for_binding_prediction.fa_8
      │       ├── results_P013521_neoPrediction_MHCI_epitopes_filtered_ident.tsv
      │       ├── results_P013521_neoPrediction_MHCI_epitopes_filtered_ident.tsv_mer
      │       ├── results_P013521_neoPrediction_MHCII_epitopes_filtered_ident.tsv
      │       ├── stdout_extractProtein_fusion
      │       ├── stdout_netMHC_fusion
      │       ├── stdout_summary
      │       └── wild-type_peptides
      └── tmp_run_status

   25 directories, 151 files


## location: 1_hla_type
    HLA type prediction and CGI output basing on vcf file
    input:
        bam file from contrl (WGS/WES)

    output: 
        format_hla
            HLA type bassing on control bam file(WGS/WES)
        mutation_germline.csv
            part of the final output

    input:
        mutation.csv
            new mutations list generated from vcf file(somiac snv)
        mutation.tsv
            new mutations list generated from vcf file(somiac snv)


    output:
        cgi_ESCA_a9ea6ee6cd67bbdddde9.log
        cgi/input01.tsv
        cgi/alterations.tsv
        cgi/summary.txt
        cgi/biomarkers.tsv

### input01.tsv
| **Column** | **Description**                                        |
|-----------|--------------------------------------------------------|
| chr       | Chromosome number where the variant is located.       |
| pos       | Genomic position of the variant.                      |
| ref       | Reference nucleotide at the given position.           |
| alt       | Alternate nucleotide (mutation at the given position). |
| gene      | Gene associated with the variant.                     |


### alterations.tsv
| **Column**                      | **Description**                                                                 |
|--------------------------------|-----------------------------------------------------------------------------|
| Input ID                      | Unique identifier for the variant entry.                                    |
| CHROMOSOME                    | Chromosome number where the variant is located.                            |
| POSITION                      | Genomic position of the variant.                                           |
| REF                           | Reference nucleotide at the given position.                                |
| ALT                           | Alternate nucleotide (mutation at the given position).                     |
| chr                           | Chromosome number (duplicate of CHROMOSOME for consistency).               |
| pos                           | Position of the variant (duplicate of POSITION for consistency).           |
| ref                           | Reference nucleotide (duplicate of REF for consistency).                   |
| alt                           | Alternate nucleotide (duplicate of ALT for consistency).                   |
| gene                          | Gene associated with the variant.                                          |
| ALT_TYPE                      | Type of alteration (e.g., SNP, insertion, deletion).                      |
| STRAND                        | DNA strand where the variant is found (+ or -).                           |
| CGI-Sample ID                 | Sample ID from CGI (Cancer Genomics Initiative).                          |
| CGI-Gene                      | Gene name as per CGI.                                                     |
| CGI-Protein Change            | Protein-level amino acid change.                                          |
| CGI-Oncogenic Summary         | Summary of oncogenic potential.                                           |
| CGI-Oncogenic Prediction      | Predicted oncogenic classification (e.g., passenger, driver).             |
| CGI-External Oncogenic Annotation | External oncogenic classification from other sources.                  |
| CGI-Mutation                  | Mutation representation in CGI format.                                    |
| CGI-Consequence               | Functional consequence of the mutation (e.g., missense, nonsense).        |
| CGI-Transcript                | Transcript ID associated with the mutation.                               |
| CGI-STRAND                    | Strand orientation in CGI data.                                           |
| CGI-Type                      | Mutation type (e.g., SNV, insertion, deletion).                           |
| CGI-HGVS                      | HGVS-formatted mutation description.                                      |
| CGI-HGVSc                     | HGVS coding sequence-level description.                                   |
| CGI-HGVSp                     | HGVS protein-level description.                                           |

### biomarkers.tsv

| **Column**      | **Description**                                                                                       |
|----------------|---------------------------------------------------------------------------------------------------|
| Sample ID      | Unique identifier for the patient or sample.                                                      |
| Alterations    | Genetic alterations present in the sample (e.g., mutations, wild-type status).                     |
| Biomarker      | Specific biomarker associated with the alteration.                                                |
| Drugs         | Approved or experimental drugs targeting the biomarker.                                          |
| Diseases      | Cancer types or diseases associated with the biomarker-drug relationship.                         |
| Response      | Predicted or observed response to the drug (e.g., responsive, resistant).                         |
| Evidence      | Evidence level supporting the biomarker-drug association (e.g., A, B, C).                        |
| Match         | Indicates whether the alteration matches an actionable biomarker.                                 |
| Source        | Source of the information (e.g., FDA, PubMed ID, clinical trials).                               |
| BioM          | Biomarker classification status (e.g., complete, partial).                                       |
| Resist.       | Indicates resistance information (if applicable).                                                |
| Tumor type    | Specific tumor classification (e.g., PRAD for prostate cancer, COREAD for colorectal cancer).    |


## location: 2_SNVs_based_neoepitope_prediction/
    (check output examples at /omics/odcf/analysis/OE0422_projects/Immuno-Patients-NCT/yanhong/all_in_one_pipeline_result/P138167_tumor01/2_SNVs_based_neoepitope_prediction)

    input:
        format_hla
        snvs_IPNCT_P138167_somatic_functional_snvs_conf_8_to_10.vcf 
            somiatic snv mutations generated from ODCF mutation calling pipeline.
        snvs_IPNCT_P138167_germline_functional_snvs_conf_8_to_10.vcf




    output:
        E-2024-33511_DNA_79279.PASS.vcf.org
            The vcf file from pathology patients.
            If the vcf file is from cegat patients, there won't be org as suffix. (More details please check the source code)
        snv_somatic.vcf
            reformated/filtered mutation list from *vcf.org
        2.vcf
            reformated/filtered mutation list from *vcf.org
        1.vcf
            reformated/filtered mutation list from *vcf.org

        1.vcf
        2.vcf
        2.vcf.annovar
        2.vcf.annovar.variant_function
        2.vcf.annovar.exonic_variant_function
        2.vcf.annovar.invalid_input
        2.vcf.annovar.log
        2.vcf.annovar.exonic_variant_function_multiple
            intermediate output by ANNOVAR annoatation proce


        netMHCpan4_1/
            predictedProtein.fa
                proteins seq 
            map_NM_geneName
                information for mutated genes
            ref.fa
                long peptides which neoepitope originate, wild-type sequence
            mut.fa
                long peptides which neoepitope originate, with mutated position in the middle of the sequence
            mut.fa_8
                intermediate file from mut.fa, used for MHCI prediction
            mut.fa_15
                intermediate file from mut.fa, used for MHCII prediction
            ref.fa_8
                intermediate file from ref.fa, used for MHCI prediction
            ref.fa_15
                intermediate file from ref.fa, used for MHCII prediction
            netMHCI_HLA-C03:04_mut
            netMHCI_HLA-B35:03_mut
            netMHCI_HLA-B40:01_mut
            netMHCI_HLA-C04:01_mut
            netMHCI_HLA-A68:01_mut
            netMHCII_DRB1_0801_mut
            netMHCII_DRB1_0701_mut
            netMHCI_HLA-B40:01_ref
            netMHCI_HLA-A68:01_ref
            netMHCI_HLA-B35:03_ref
            netMHCI_HLA-C04:01_ref
            netMHCI_HLA-C03:04_ref
            netMHCII_DRB1_0801_ref
            netMHCII_DRB1_0701_ref
                output from netMHCpan/netMHCIIpan
            netMHCI_HLA-A68:01_mut_reformat
            netMHCI_HLA-A68:01_ref_reformat
            netMHCI_HLA-B35:03_mut_reformat
            netMHCI_HLA-B35:03_ref_reformat
            netMHCI_HLA-B40:01_mut_reformat
            netMHCI_HLA-B40:01_ref_reformat
            netMHCI_HLA-C03:04_mut_reformat
            netMHCI_HLA-C03:04_ref_reformat
            netMHCI_HLA-C04:01_mut_reformat
            netMHCI_HLA-C04:01_ref_reformat
            netMHCII_DRB1_0701_mut_reformat
            netMHCII_DRB1_0701_ref_reformat
            netMHCII_DRB1_0801_mut_reformat
            netMHCII_DRB1_0801_ref_reformat
                reformat for downstream processing
            netMHCI_HLA-A68:01_summary
            netMHCI_HLA-B35:03_summary
            netMHCI_HLA-B40:01_summary
            netMHCI_HLA-C03:04_summary
            netMHCI_HLA-C04:01_summary
            netMHCII_DRB1_0701_summary
            netMHCII_DRB1_0801_summary
                reformat for downstream processing
            headerVCF
                columns names from VCF file
            headerMHCI
            headerMHCII
                new column names for MHCI/MHCII tables
            results_MHCI_epitopes.tab
            results_MHCII_epitopes.tab
                formatted output after neoepitope prediciton
            results_MHCI_epitopes.tab.hydro
            results_MHCII_epitopes.tab.hydro
                tables with hydrophobicity values added
            results_MHCII_epitopes.tab.hydro_splitGenes
            results_MHCI_epitopes.tab.hydro_splitGenes
                tables with hydrophobicity values added, with mutation annotated by multple genes splited into seperate rows.


### An example annotation for 1.vcf 
    (Not from cegat patients processed by ODCF pipeline but from pathology patients.)

| **Column**                 | **Description**                                                                 |
|----------------------------|-------------------------------------------------------------------------------|
| CHROM                      | Chromosome number where the variant is located.                             |
| POS                        | Genomic position of the variant.                                            |
| ID                         | Variant identifier (if available).                                          |
| REF                        | Reference nucleotide(s) at the given position.                             |
| ALT                        | Alternative nucleotide(s) representing the mutation.                       |
| QUAL                       | Quality score of the variant call.                                          |
| FILTER                     | Filter status of the variant (e.g., PASS, LowQual).                        |
| INFO                       | Additional metadata about the variant (e.g., depth, allele frequency).     |
| FORMAT                     | Format specification for genotype data.                                     |
| omics                      | Omics data related to the variant.                                          |
| SEQUENCE_CONTEXT           | Surrounding nucleotide sequence for context.                               |
| INFO_control               | Variant allele fraction (VAF) and total variant supporting reads (TSR).    |
| ANNOTATION_control         | Variant annotation from control datasets.                                  |
| DBSNP                      | dbSNP identifier (if available).                                           |
| 1K_GENOMES                 | Presence of the variant in the 1000 Genomes Project database.              |
| ANNOVAR_FUNCTION           | Functional annotation of the variant (e.g., exonic, intronic).             |
| GENE                       | Gene affected by the variant.                                              |
| EXONIC_CLASSIFICATION      | Classification of exonic variants (e.g., missense, nonsense).              |
| ANNOVAR_TRANSCRIPTS        | Specific transcript(s) affected by the variant.                            |
| SEGDUP                     | Segmental duplication information.                                         |
| CYTOBAND                   | Cytogenetic band where the variant is located.                             |
| REPEAT_MASKER              | Presence in repetitive regions.                                            |
| DAC_BLACKLIST              | Whether the variant is in DAC blacklisted regions.                        |
| DUKE_EXCLUDED              | Indicates exclusion based on Duke University mappability scores.           |
| HISEQDEPTH                 | High sequencing depth information.                                         |
| SELFCHAIN                  | Self-chain duplication annotation.                                         |
| MAPABILITY                 | Genomic mappability score.                                                 |
| SIMPLE_TANDEMREPEATS       | Presence in simple tandem repeat regions.                                 |
| CONFIDENCE                 | Confidence score for variant calling.                                      |
| RECLASSIFICATION           | Variant reclassification information.                                      |
| PENALTIES                  | Any penalties applied during variant calling.                             |
| seqBiasPresent_1/2         | Sequence bias presence in dataset 1 and 2.                                |
| seqingBiasPresent_1/2      | Sequencing bias information in dataset 1 and 2.                           |
| Enhancers                  | Presence of the variant in enhancer regions.                              |
| CpGislands                 | Overlap with CpG islands.                                                  |
| TFBScons                   | Transcription factor binding sites conservation.                          |
| ENCODE_DNASE               | DNase hypersensitivity site annotation from ENCODE.                       |
| miRNAs_snoRNAs             | Association with miRNAs or snoRNAs.                                        |
| miRBase18                  | miRNA annotation from miRBase database.                                   |
| COSMIC                     | Presence in the COSMIC (cancer mutations) database.                      |
| miRNAtargets               | miRNA target sites related to the variant.                                |
| CgiMountains               | CGI methylation status and regions.                                       |
| phastConsElem20bp          | Conservation scores from phastCons (20bp window).                        |
| ENCODE_TFBS                | Overlap with transcription factor binding sites from ENCODE.              |
| geneID                     | Unique gene identifier.                                                   |
| ex1/ex2                    | Additional exonic information (e.g., exon numbers affected).              |

## location: 3_add_expression

    ├── 3_add_expression
    │   ├── addRNA1
    │   ├── addRNA2
    │   ├── addRNA3
    │   ├── fpkm_COL6A3_exon6.txt
    │   ├── MHCI_epitopes_TCGA-HNSC_RNAseq_netMHCpan4_1.tab
    │   ├── MHCII_epitopes_TCGA-HNSC_RNAseq.tab
    │   ├── past
    │   │   ├── MHCI_epitopes_RNAseq_netMHCpan4_1.tab
    │   │   └── MHCII_epitopes_RNAseq.tab
    │   ├── tumor_IPNCT_P013521.fpkm_tpm.featureCounts.tsv
    │   ├── tumor_IPNCT_P013521_merged.mdup.bam
    │   └── tumor_IPNCT_P013521_merged.mdup.bam.bai

### addRNA1
    (addRNA* files: intermediate steps for reads information extraction and gene annotation)
| **Column** | **Description**                                          |
|------------|----------------------------------------------------------|
| chr        | Chromosome number where the variant is located.         |
| loc        | Genomic position of the variant.                        |
| ref        | Reference nucleotide at the given position.             |
| A          | Count of adenine (A) reads at this position.            |
| T          | Count of thymine (T) reads at this position.            |
| C          | Count of cytosine (C) reads at this position.           |
| G          | Count of guanine (G) reads at this position.            |


## location: 4_indel_based_prediction
    indel_IPNCT_P138167_somatic_functional_indels_conf_8_to_10.vcf 
    indel_IPNCT_P138167_germline_functional_indels_conf_8_to_10.vcf 
    indel_long_peptides.tsv
    indel_wildType_MHCII.tsv
    indel_wildType_MHCI.tsv
    indel_mutant_MHCII.tsv
    indel_mutant_MHCI.tsv
        formatted output 
    indel_mutant_MHCI.tsv_wish
    indel_mutant_MHCII.tsv_wish
    indel_wildType_MHCI.tsv_wish
    indel_wildType_MHCII.tsv_wish
        formatted output with information whether a gene exist on the in-house wish-list

    result
        NF1.tab
        NF1_targeted.fa
        NF1_refPeptide.fa
        NF1_targeted.fa_8
        NF1_targeted.fa_15
        NF1_refPeptide.fa_8
        NF1_refPeptide.fa_15
            peptide for neoepitope prediction
        netMHCI_HLA-C04:01_mutated
        netMHCI_HLA-B35:03_mutated
        netMHCI_HLA-B40:01_mutated
        netMHCI_HLA-C03:04_mutated
        netMHCI_HLA-A68:01_mutated
        netMHCI_HLA-C04:01_ref
        netMHCI_HLA-C03:04_ref
        netMHCI_HLA-B35:03_ref
        netMHCI_HLA-B40:01_ref
        netMHCI_HLA-A68:01_ref
        netMHCII_DRB1_0701_mutated
        netMHCII_DRB1_0801_mutated
        netMHCII_DRB1_0701_ref
        netMHCII_DRB1_0801_ref
        NF1_neoepitope_indel_mutation
        NF1_epitope_indel_wildtype
        NF1_binding
            raw output from netMHCpan/netMHCIIpan 


## location: 5_LOHHLA
    data/
        hlas
            hla type
        HLAs
            hla type
        example.patient.hlaFasta.fa
            DNA seq of HLA

## location:8_chose_neoepitode
    wish_list_genes_expression.csv
        wish-gene expression profile from RNAseq data
    MHCI_epitopes_TCGA-PAAD_RNAseq_netMHCpan4_1.tab
    MHCII_epitopes_TCGA-PAAD_RNAseq.tab
        tables that integarated RNAseq/TCGA-based gene expression profile
    MHCI_epitopes_TCGA-PAAD_RNAseq_netMHCpan4_1.tab_renameCol
    MHCII_epitopes_TCGA-PAAD_RNAseq.tab_renameCol
        tables with renamed column names
    MHCI_epitopes_TCGA-PAAD_RNAseq_netMHCpan4_1.tab_renameCol_wish
    MHCII_epitopes_TCGA-PAAD_RNAseq.tab_renameCol_wish
        tables with CGI-related information

## location: 9_Fusion_gene_based_neoepitope_identification
    2_arriba_result_RNAbamOpt/
        fusions.tsv
            fusion called by Arriba
        fusions.discarded.tsv
            discarded positions by Arriba
        netMHCI_input.txt
            HLA type (MHCI) for fusion-based neoepitope prediction
        netMHCII_input.txt
            HLA type (MHCII) for fusion-based neoepitope prediction
        fusions.tsv_splitGenes
            Fusion genes from more than 1 annnoated genes are wrote to seperate lines.

### fusion.tsv

| **Column**                     | **Description**                                                        |
|--------------------------------|------------------------------------------------------------------------|
| gene1                          | First gene involved in the fusion or structural variant.               |
| gene2                          | Second gene involved in the fusion or structural variant.              |
| strand1 (gene/fusion)          | Strand orientation of gene1 in the fusion.                            |
| strand2 (gene/fusion)          | Strand orientation of gene2 in the fusion.                            |
| breakpoint1                    | Chromosomal location of the breakpoint in gene1.                      |
| breakpoint2                    | Chromosomal location of the breakpoint in gene2.                      |
| site1                          | Type of site affected in gene1 (e.g., CDS, intron, splice-site).      |
| site2                          | Type of site affected in gene2 (e.g., CDS, intron, splice-site).      |
| type                           | Type of structural variant (e.g., deletion, translocation).           |
| split_reads1                   | Number of split reads supporting the fusion in gene1.                 |
| split_reads2                   | Number of split reads supporting the fusion in gene2.                 |
| discordant_mates               | Number of discordant mate pairs supporting the fusion.                |
| coverage1                      | Read coverage at the breakpoint in gene1.                             |
| coverage2                      | Read coverage at the breakpoint in gene2.                             |
| confidence                     | Confidence level of the fusion call (e.g., high, medium).             |
| reading_frame                  | Indicates whether the fusion causes an in-frame or out-of-frame shift. |
| tags                           | Additional annotations or comments.                                   |
| retained_protein_domains       | Retained protein domains in the fusion event.                        |
| closest_genomic_breakpoint1    | Closest genomic breakpoint to gene1.                                  |
| closest_genomic_breakpoint2    | Closest genomic breakpoint to gene2.                                  |
| gene_id1                       | Gene ID corresponding to gene1.                                       |
| gene_id2                       | Gene ID corresponding to gene2.                                       |
| transcript_id1                 | Transcript ID corresponding to gene1.                                |
| transcript_id2                 | Transcript ID corresponding to gene2.                                |
| direction1                     | Direction of gene1 in relation to the fusion event (e.g., upstream).  |
| direction2                     | Direction of gene2 in relation to the fusion event (e.g., downstream). |
| filters                        | Quality control or filtering criteria applied to the fusion call.     |
| fusion_transcript              | Sequence of the predicted fusion transcript.                         |
| peptide_sequence               | Predicted peptide sequence of the fusion.                            |
| read_identifiers               | List of read IDs supporting the fusion event.                        |


    3_neoPrediction_RNAbamOpt/
        peptides_for_binding_prediction.fa
            peptides of fusion genes for neoepitope prediction 
        stdout_extractProtein_fusion
            log of the process of extracting proteins
        peptides_for_binding_prediction.fa_8
            peptides for MHCI prediction
        peptides_for_binding_prediction.fa_15
            peptides for MHCII prediction
        netMHCI_HLA-A11:01_fusion
        netMHCI_HLA-A02:17_fusion
        netMHCI_HLA-B44:02_fusion
        netMHCI_HLA-B51:01_fusion
        netMHCI_HLA-C15:02_fusion
        netMHCI_HLA-C07:04_fusion
        netMHCII_DQA1_0102_fusion
        netMHCII_DQA1_0301_fusion
        netMHCII_DQB1_0502_fusion
        netMHCII_DQB1_0303_fusion
        netMHCII_DRB1_0901_fusion
        netMHCII_DRB1_1601_fusion
            output by netMHCpan/netMHCIIpan
        stdout_netMHC_fusion
            log of netMHCpan/netMHCIIpan running
        MHCI_reformat
        MHCII_reformat
            formatted output 
        wild-type_peptides
        MHCI_filtered
        MHCII_filtered
        results_P143091_neoPrediction_MHCI_epitopes_filtered_ident.tsv
        results_P143091_neoPrediction_MHCII_epitopes_filtered_ident.tsv
            further formatted output
        stdout_summary
            log
        results_P143091_neoPrediction_MHCI_epitopes_filtered_ident.tsv_mer
        results_P143091_neoPrediction_MHCII_epitopes_filtered_ident.tsv_mer
            further formatted output

## tmp_run_status
    status file generated by all_in_one_pipeline_0_update.sh


---

# Final output:
├── Epitope_prediction
│   ├── indel_based (output of indel-based neoepitopes)
│   │   ├── indel_long_peptides.xlsx
│   │   ├── indel_mutant_MHCII.xlsx
│   │   ├── indel_mutant_MHCI.xlsx
│   │   ├── indel_wildType_MHCII.xlsx
│   │   └── indel_wildType_MHCI.xlsx
│   └── snv_based (output of snv-based neoepitopes)
│       ├── MHCI_epitopes_TCGA-PAAD_RNAseq_netMHCpan4_1.xlsx
│       └── MHCII_epitopes_TCGA-PAAD_RNAseq.xlsx
├── Gene_Expression 
│   ├── fpkm_COL6A3_exon6.txt (Reads information for COL6A3_exon6)
│   ├── tumor01_IPNCT_P143091.fpkm_tpm.featureCounts.tsv.xlsx (gene expression info by ODCF pipeline)
│   └── wish_list_genes_expression.csv.xlsx (Wish-list from D120)
├── HLA
│   └── In_silico (predicted by appotitype and korami)
│       └── format_hla
├── Mutation_analysis
│   ├── CGI (Cancer Genome Interpreter output, more details [here](https://www.cancergenomeinterpreter.org/analysis?msg=Malformated%20entry:%20ACAP2%20KCNAB1&value=ACAP2%09KCNAB1%0AACAP2%09KCNAB1%0ASTAT3%09RNU7-97P%0ARSRC1%09RP11-23D24.2%0AMUC4%09RSRC1%0ALTBP1%09BIRC6%0ABCL2L2-PABPN1%09PPP1R3E%0AHIC2%09TMEM191C%0ASTAG1%09KCNAB1%0AZFYVE19%09RPS3AP23%0ABABAM1%09BABAM1%0ASCAF1%09SCAF1%0AVRK2%09FANCL%0AELF1%09TPTE2P5%0AELF1%09TPTE2P5%0AHAP1%09ABHD15%0ASTAT3%09ATP6V0A1))
│   │   ├── alterations.tsv
│   │   ├── biomarkers.tsv
│   │   ├── input01.tsv
│   │   └── summary.txt
│   ├── fusion (fusion mutations called by arriba)
│   │   └── fusions_splitGenes.tsv
│   ├── indel (somatic/germline functional indel mutations called by ODCF pipeline)
│   │   ├── indel_IPNCT_P143091_germline_functional_indels_conf_8_to_10.vcf
│   │   └── indel_IPNCT_P143091_somatic_functional_indels_conf_8_to_10.vcf
│   └── snv (somatic/germline functional snv mutations called by ODCF pipeline)
│       ├── snvs_IPNCT_P143091_germline_functional_snvs_conf_8_to_10.vcf
│       └── snvs_IPNCT_P143091_somatic_functional_snvs_conf_8_to_10.vcf
└── P143091_tumor01.zip

# SNV
## snv MHCI column annotation
| **Column Name**                      | **Annotation**                                                                                      |
|--------------------------------------|------------------------------------------------------------------------------------------------------|
| **Ensembl_Gene_ID**                  | Unique identifier for the gene in the Ensembl database.                                              |
| **Official_Gene_Symbol**             | The standardized gene symbol (name) according to official nomenclature (e.g., "TP53").               |
| **MHC_allele**                       | The MHC (Major Histocompatibility Complex) allele associated with antigen presentation.              |
| **Mutant_epitope**                   | The peptide sequence that is presented by the mutant form of the protein.                            |
| **aaChange**                         | The amino acid change resulting from the mutation (e.g., "p.Glu6Val").                               |
| **Mutant_epitope_length**            | The length (in amino acids) of the mutant epitope.                                                   |
| **Mut_pos_epitope**                  | The position of the mutation within the epitope sequence.                                            |
| **Score_EL_Mut**                     | The score representing the predicted binding affinity of the mutant epitope to the MHC molecule, based on netMHCpan 4.1 algorithm("EL" score). |
| **Rank_EL_Mut**                      | The rank of the mutant epitope’s binding affinity (higher or lower rank based on predicted affinity). |
| **Score_BA_Mut**                     | The binding affinity score for the mutant epitope. |
| **Rank_BA_Mut**                      | The rank of the binding affinity for the mutant epitope according to the BA score.                   |
| **Aff.nM_Mut**                       | The binding affinity (in nanomolar concentration) for the mutant epitope.                           |
| **BindLevel_Mut**                    | The classification or level of binding strength for the mutant epitope (e.g., strong, weak).         |
| **Wildtype_peptide**                 | The peptide sequence corresponding to the wild-type (non-mutated) form of the protein.               |
| **Score_EL_Wt**                      | The binding affinity score of the wild-type epitope to the MHC molecule using the EL method.         |
| **Rank_EL_Wt**                       | The rank of the wild-type epitope’s binding affinity according to the EL score.                      |
| **Score_BA_Wt**                      | The binding affinity score for the wild-type epitope.                            |
| **Rank_BA_Wt**                       | The rank of the wild-type epitope’s binding affinity based on the BA score.                          |
| **Aff.nM_Wt**                        | The binding affinity (in nanomolar) for the wild-type epitope.                                       |
| **BindLevel_Wt**                     | The classification or level of binding strength for the wild-type epitope.                           |
| **Epi_pos_in_longpep**               | The position of the epitope within the full-length peptide sequence.                                 |
| **WildType_long_peptide**            | The full-length peptide sequence of the wild-type (non-mutated) form.                               |
| **RefSeq**                           | The reference sequence identifier for the gene (from RefSeq database).                               |
| **TPM**                              | Transcripts Per Million; a measure of gene expression, normalized by sequencing depth and gene length. |
| **FPKM**                             | Fragments Per Kilobase of transcript per Million mapped reads; another metric of gene expression.   |
| **Mean_TCGA**                        | The mean gene expression level in TCGA (The Cancer Genome Atlas) dataset.                           |
| **Median_TCGA**                      | The median gene expression level in TCGA dataset.                                                   |
| **sumReads**                         | Total number of reads mapping to the gene.                                                           |
| **numOfBaseExp**                     | Number of bases (nucleotides) expressed in the gene.                                                 |
| **rna_freRef**                       | Frequency of the reference allele in RNA expression data.                                            |
| **rna_freAlt**                       | Frequency of the alternative (mutant) allele in RNA expression data.                                 |
| **rna_expAlt**                       | Expression level of the alternative allele in RNA data.                                              |
| **rna_freAlt.FPKM**                  | FPKM (Fragments Per Kilobase Million) for the alternative allele in RNA data.                        |
| **dna_freAlt**                       | Frequency of the alternative allele in DNA sequence data.                                            |
| **dna_cov**                          | Coverage of DNA sequencing data for the gene (e.g., depth of sequencing).                           |
| **CHROM**                            | Chromosome number where the gene is located.                                                         |
| **POS**                              | The position of the mutation in the chromosome.                                                      |
| **CGI.Oncogenic.Summary**            | Summary of oncogenic potential of the mutation (e.g., benign, pathogenic).                           |
| **CGI.Oncogenic.Prediction**         | Predicted oncogenicity of the mutation (e.g., likely pathogenic).                                    |
| **CGI.Consequence**                  | The biological consequence of the mutation (e.g., missense, nonsense).                              |
| **wishList**                         | A specific list of genes or mutations of interest for further study or investigation from d120.                |
| **Hydrophobic_GRAVY**                | The GRAVY (Grand Average of Hydropathy) score, a measure of the hydrophobicity of the protein.        |
| **ANNOVAR_TRANSCRIPTS**              | Information on the annotated transcripts from the ANNOVAR tool (genetic variant annotation).         |
| **hydro_frac_mut**                   | The fraction of hydrophobic amino acids in the mutant peptide.                                       |
| **hydro_frac_wild**                  | The fraction of hydrophobic amino acids in the wild-type peptide.                                    |
| **hydro_mut_wild_ratio**             | The ratio of hydrophobic amino acids between the mutant and wild-type peptides.                      |

## snv MHCII column annotation

| **Column Name**                      | **Annotation**                                                                                      |
|--------------------------------------|------------------------------------------------------------------------------------------------------|
| **Ensembl_Gene_ID**                  | Unique identifier for the gene in the Ensembl database.                                              |
| **Official_Gene_Symbol**             | The standardized gene symbol (name) according to official nomenclature (e.g., "TP53").               |
| **MHC_allele**                       | The MHC (Major Histocompatibility Complex) allele associated with antigen presentation.              |
| **Mutant_epitope**                   | The peptide sequence that is presented by the mutant form of the protein.                            |
| **aaChange**                         | The amino acid change resulting from the mutation (e.g., "p.Glu6Val").                               |
| **Mutant_epitope_length**            | The length (in amino acids) of the mutant epitope.                                                   |
| **Mut_pos_epitope**                  | The position of the mutation within the epitope sequence.                                            |
| **9mer_core_Mut**                    | The core 9-mer peptide sequence of the mutant epitope, typically the minimal binding region for MHC.  |
| **Aff.nM_Mut**                       | The binding affinity (in nanomolar concentration) for the mutant epitope.                           |
| **Rank_Mut**                         | The rank of the mutant epitope’s binding affinity, based on predicted affinity.                      |
| **BindLevel_Mut**                    | The classification or level of binding strength for the mutant epitope (e.g., strong, weak).         |
| **Wildtype_peptide**                 | The peptide sequence corresponding to the wild-type (non-mutated) form of the protein.               |
| **9mer_core_Wt**                     | The core 9-mer peptide sequence of the wild-type epitope, typically the minimal binding region for MHC. |
| **Aff.nM_Wt**                        | The binding affinity (in nanomolar) for the wild-type epitope.                                       |
| **Rank_Wt**                          | The rank of the wild-type epitope’s binding affinity, based on predicted affinity.                   |
| **BindLevel_Wt**                     | The classification or level of binding strength for the wild-type epitope (e.g., strong, weak).      |
| **WildType_lng_peptide**             | The full-length peptide sequence of the wild-type (non-mutated) form.                                |
| **Mutant_long_peptide**              | The full peptide sequence with the mutation incorporated.                                            |
| **Epi_pos_in_longpep**               | The position of the epitope within the full-length peptide sequence.                                 |
| **RefSeq**                           | The reference sequence identifier for the gene (from RefSeq database).                               |
| **TPM**                              | Transcripts Per Million; a measure of gene expression, normalized by sequencing depth and gene length. |
| **FPKM**                             | Fragments Per Kilobase of transcript per Million mapped reads; another metric of gene expression.   |
| **Mean_TCGA**                        | The mean gene expression level in TCGA (The Cancer Genome Atlas) dataset.                           |
| **Median_TCGA**                      | The median gene expression level in TCGA dataset.                                                   |
| **sumReads**                         | Total number of reads mapping to the gene.                                                           |
| **numOfBaseExp**                     | Number of bases (nucleotides) expressed in the gene.                                                 |
| **rna_freRef**                       | Frequency of the reference allele in RNA expression data.                                            |
| **rna_freAlt**                       | Frequency of the alternative (mutant) allele in RNA expression data.                                 |
| **rna_expAlt**                       | Expression level of the alternative allele in RNA data.                                              |
| **rna_freAlt.FPKM**                  | FPKM (Fragments Per Kilobase Million) for the alternative allele in RNA data.                        |
| **dna_freAlt**                       | Frequency of the alternative allele in DNA sequence data.                                            |
| **dna_cov**                          | Coverage of DNA sequencing data for the gene (e.g., depth of sequencing).                           |
| **CHROM**                            | Chromosome number where the gene is located.                                                         |
| **POS**                              | The position of the mutation in the chromosome.                                                      |
| **CGI.Oncogeic.Summary**             | Summary of oncogenic potential of the mutation (e.g., benign, pathogenic).                           |
| **CGI.Oncogenic.Prediction**         | Predicted oncogenicity of the mutation (e.g., likely pathogenic).                                    |
| **CGI.Consequence**                  | The biological consequence of the mutation (e.g., missense, nonsense).                              |
| **wishList**                         | A specific list of genes or mutations of interest for further study or investigation from d120.                |
| **Hydrophobic_GRAVY**                | The GRAVY (Grand Average of Hydropathy) score, a measure of the hydrophobicity of the protein.        |
| **ANNOVAR_TRANSCRIPTS**              | Information on the annotated transcripts from the ANNOVAR tool (genetic variant annotation).         |
| **hydro_frac_mut**                   | The fraction of hydrophobic amino acids in the mutant peptide.                                       |
| **hydro_frac_wild**                  | The fraction of hydrophobic amino acids in the wild-type peptide.                                    |
| **hydro_mut_wild_ratio**             | The ratio of hydrophobic amino acids between the mutant and wild-type peptides.                      |

# INDEL
## indel: indel_long_peptides.xlsx

| **Column Name**       | **Annotation**                                                                 |
|-----------------------|---------------------------------------------------------------------------------|
| **Official_Gene_Symbol** | The standardized gene symbol (name) according to official nomenclature (e.g., "APC"). |
| **splice_state**        | The splice status of the mRNA; indicates whether the gene transcript is spliced or unspliced. |
| **ref.mut**             | Indicates whether the sequence corresponds to the reference (ref) or mutant (mut) form. |
| **sequence**            | The peptide or nucleotide sequence corresponding to either the reference or mutant form. |


## indel: indel_mutant_MHCI.xlsx
| **Column**              | **Annotation / Description**                                                                                                                                           |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ensembl_gene_id         | Ensembl gene identifier.                                                                                                                                               |
| Official_Gene_Symbol    | The official gene symbol (e.g., APC).                                                                                                                                  |
| MHC_allele              | The MHC/HLA allele used for epitope binding predictions (e.g., HLA-A*02:01).                                                                                           |
| Mutant_epitope          | The amino acid sequence of the mutant epitope.                                                                                                                         |
| Core                    | The core epitope sequence used for binding prediction.                                                                                                               |
| Of                      | **netMHCpan 4.1 output:** A parameter (e.g., offset or other metric) defined by netMHCpan 4.1; see the tool's documentation for specific details.                   |
| Gp                      | **netMHCpan 4.1 output:** A prediction metric provided by netMHCpan 4.1; refer to its documentation for a detailed explanation.                                       |
| Gl                      | **netMHCpan 4.1 output:** Likely represents a metric related to ligand properties (e.g., ligand length or a related score); check netMHCpan 4.1 documentation.         |
| Ip                      | **netMHCpan 4.1 output:** An internal prediction score or parameter from netMHCpan 4.1.                                                                                 |
| Il                      | **netMHCpan 4.1 output:** Another parameter from netMHCpan 4.1 reflecting aspects of the peptide–MHC interaction; refer to the tool’s documentation for details.     |
| Icore                   | **netMHCpan 4.1 output:** The predicted binding core sequence of the peptide as determined by netMHCpan 4.1.                                                               |
| Score_EL_Mut            | Eluted ligand (EL) score for the mutant epitope.                                                                                                                       |
| Rank_EL_Mut             | Percentile rank of the mutant epitope’s EL score (lower value indicates stronger binding).                                                                             |
| Score_BA_Mut            | Binding affinity (BA) score for the mutant epitope.                                                                                                                  |
| Rank_BA_Mut             | Percentile rank of the mutant epitope’s BA score (lower value indicates stronger binding).                                                                             |
| Aff.nM                  | Predicted binding affinity (in nanomolar, nM) for the mutant epitope.                                                                                                |
| BindLevel_mutant        | Qualitative binding level for the mutant epitope (e.g., SB for strong binder).                                                                                       |
| chr                     | Chromosome where the mutation is located.                                                                                                                            |
| pos                     | Genomic position (base pair coordinate) of the mutation.                                                                                                             |
| reference               | The reference allele at the mutation position.                                                                                                                       |
| mutation                | The mutant allele observed.                                                                                                                                           |
| genomic_location        | Genomic context or region of the variant (e.g., exonic).                                                                                                             |
| ANNOVAR_TRANSCRIPTS     | Transcript annotations provided by ANNOVAR, detailing exon and mutation information.                                                                                 |
| Hydrophobic_GRAVY       | GRAVY (Grand Average of Hydropathy) score, indicating the overall hydrophobicity of the peptide.                                                                       |
| CGI.Oncogenic.Summary   | Summary from the Cancer Genome Interpreter regarding the oncogenic potential of the mutation.                                                                          |
| CGI.Oncogenic.Prediction| Oncogenic prediction from the Cancer Genome Interpreter (e.g., “driver” as predicted by oncodriveMUT).                                                                   |
| CGI.Consequence         | Predicted functional consequence of the mutation (e.g., frameshift_variant).                                                                                         |
| CGI.Transcript          | The specific transcript ID used in the CGI analysis.                                                                                                                 |
| wishList                | A flag indicating if the gene/variant is of special interest (e.g., “TRUE” if on the wish list).                                                                       |
| hydro_frac_mut          | The fraction of hydrophobic residues in the mutant epitope.                                                                                                          |

## indel: indel_mutant_MHCII.xlsx

| **Column**                | **Annotation / Description**                                                                                                                                              |
|---------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| ensembl_gene_id           | Ensembl gene identifier.                                                                                                                                                  |
| Official_Gene_Symbol      | The official gene symbol (e.g., APC).                                                                                                                                     |
| MHC_allele                | The MHC/HLA allele used for epitope binding predictions (e.g., HLA-A*03:01).                                                                                              |
| Mutant_epitope            | The amino acid sequence of the mutant epitope.                                                                                                                            |
| Core                      | The core epitope sequence used for binding prediction.                                                                                                                  |
| Of                        | A parameter value from the prediction tool; refer to its documentation for details.                                                                                       |
| Gp                        | A metric from the prediction tool indicating a specific property of the peptide.                                                                                        |
| Gl                        | A score or parameter related to ligand characteristics from the prediction tool.                                                                                       |
| Ip                        | An internal prediction score or parameter; see the tool's documentation for further explanation.                                                                         |
| Il                        | A value reflecting aspects of the peptide–MHC interaction; refer to the tool's documentation for details.                                                                 |
| Icore                     | The predicted binding core sequence as determined by the prediction tool.                                                                                                |
| Score_EL_Mut              | Eluted ligand (EL) score for the mutant epitope.                                                                                                                          |
| Rank_EL_Mut               | Percentile rank of the mutant epitope’s EL score (lower values indicate stronger binding).                                                                               |
| Score_BA_Mut              | Binding affinity (BA) score for the mutant epitope.                                                                                                                       |
| Rank_BA_Mut               | Percentile rank of the mutant epitope’s BA score (lower values indicate stronger binding).                                                                               |
| Aff.nM                    | Predicted binding affinity (in nanomolar, nM) for the mutant epitope.                                                                                                     |
| BindLevel_wildType        | Qualitative binding level for the wild-type epitope.                                                                                                                      |
| chr                       | Chromosome where the mutation is located.                                                                                                                               |
| pos                       | Genomic position (base pair coordinate) of the mutation.                                                                                                                |
| reference                 | The reference allele at the mutation position.                                                                                                                          |
| mutation                  | The mutant allele observed.                                                                                                                                              |
| genomic_location          | Genomic context or region of the variant (e.g., exonic).                                                                                                                 |
| ANNOVAR_TRANSCRIPTS       | Transcript annotations provided by ANNOVAR, detailing exon and mutation information.                                                                                     |
| Hydrophobic_GRAVY         | GRAVY (Grand Average of Hydropathy) score, indicating the overall hydrophobicity of the peptide.                                                                           |
| CGI.Oncogenic.Summary     | Summary from the Cancer Genome Interpreter regarding the oncogenic potential of the mutation.                                                                              |
| CGI.Oncogenic.Prediction  | Oncogenic prediction from the Cancer Genome Interpreter (e.g., predicted as driver by oncodriveMUT).                                                                        |
| CGI.Consequence           | Predicted functional consequence of the mutation (e.g., frameshift_variant).                                                                                             |
| CGI.Transcript            | The specific transcript ID used in the CGI analysis.                                                                                                                   |
| wishList                  | A flag indicating if the gene/variant is of special interest (e.g., "TRUE" if on the wish list).                                                                          |
| hydro_frac_mut            | The fraction of hydrophobic residues in the mutant epitope.                                                                                                              |

## indel: indel_wildType_MHCI.xlsx, indel_wildType_MHCII.xlsx
    Similar annotation but for wild type peptides.

# FUSION
## MHCI_RNAbamOpt.xlsx
| **Column**                         | **Annotation / Description**                                                                                                                                                                      |
|------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Position                           | An identifier or index for the fusion event (e.g., row number).                                                                                                                                    |
| MHC_allele                         | The MHC/HLA allele used for epitope binding predictions (e.g., HLA-A*02:01).                                                                                                                       |
| Mutant_epitope                     | The amino acid sequence of the mutant epitope derived from the fusion event.                                                                                                                      |
| Core                               | The core epitope sequence used for binding prediction.                                                                                                                                             |
| Of                                 | A parameter value from the prediction tool; refer to the tool’s documentation for details.                                                                                                         |
| Gp                                 | A metric indicating a specific peptide property as provided by the prediction tool.                                                                                                                 |
| Gl                                 | A score or parameter related to ligand characteristics as output by the prediction tool.                                                                                                           |
| Ip                                 | An internal prediction score or parameter from the prediction tool.                                                                                                                                |
| Il                                 | A value reflecting aspects of the peptide–MHC interaction; see the tool’s documentation for details.                                                                                               |
| Icore                              | The predicted binding core sequence as determined by the prediction tool.                                                                                                                           |
| Identity                           | A label or identifier for the fusion event (e.g., "fusion14").                                                                                                                                     |
| Score_EL_Mut                       | Eluted ligand (EL) score for the mutant epitope.                                                                                                                                                   |
| Rank_EL_Mut                        | Percentile rank of the mutant epitope’s EL score (lower values indicate stronger binding).                                                                                                         |
| Score_BA_Mut                       | Binding affinity (BA) score for the mutant epitope.                                                                                                                                                |
| Rank_BA_Mut                        | Percentile rank of the mutant epitope’s BA score (lower values indicate stronger binding).                                                                                                         |
| Aff.nM_Mut                         | Predicted binding affinity for the mutant epitope, measured in nanomolar (nM).                                                                                                                     |
| BindLevel_Mut                      | Qualitative binding level for the mutant epitope (e.g., strong binder, weak binder).                                                                                                               |
| Official_Gene_Symbol_1             | The official gene symbol for the first gene involved in the fusion.                                                                                                                                |
| Official_Gene_Symbol_2             | The official gene symbol for the second gene involved in the fusion.                                                                                                                                |
| strand1.gene.fusion.               | Fusion strand orientation for the first gene (indicating the gene’s direction in the fusion).                                                                                                      |
| strand2.gene.fusion.               | Fusion strand orientation for the second gene.                                                                                                                                                   |
| breakpoint1                        | Genomic breakpoint for the first gene in the fusion event.                                                                                                                                       |
| breakpoint2                        | Genomic breakpoint for the second gene in the fusion event.                                                                                                                                      |
| site1                              | Genomic site annotation (e.g., CDS/splice-site) for the breakpoint in the first gene.                                                                                                              |
| site2                              | Genomic site annotation for the breakpoint in the second gene.                                                                                                                                    |
| type                               | The type of fusion event (e.g., inversion, translocation).                                                                                                                                        |
| split_reads1                       | Number of split reads supporting the fusion for the first gene.                                                                                                                                    |
| split_reads2                       | Number of split reads supporting the fusion for the second gene.                                                                                                                                   |
| discordant_mates                   | Number of discordant mate pairs supporting the fusion event.                                                                                                                                     |
| coverage1                          | Read coverage at the breakpoint for the first gene.                                                                                                                                              |
| coverage2                          | Read coverage at the breakpoint for the second gene.                                                                                                                                             |
| confidence                         | Confidence level of the fusion call (e.g., low, medium, high).                                                                                                                                     |
| reading_frame                      | Reading frame annotation of the fusion (e.g., in-frame, out-of-frame).                                                                                                                             |
| tags                               | Additional tags or annotations associated with the fusion event.                                                                                                                                 |
| retained_protein_domains           | Protein domains retained in the fusion product, with percentage matches where applicable.                                                                                                         |
| closest_genomic_breakpoint1        | The closest genomic breakpoint near the first gene’s fusion breakpoint.                                                                                                                           |
| closest_genomic_breakpoint2        | The closest genomic breakpoint near the second gene’s fusion breakpoint.                                                                                                                          |
| Ensembl_Gene_ID_1                  | Ensembl gene identifier for the first gene involved in the fusion.                                                                                                                               |
| Ensembl_Gene_ID_2                  | Ensembl gene identifier for the second gene involved in the fusion.                                                                                                                              |
| Ensembl_Transcript_ID_1            | Ensembl transcript identifier for the first gene.                                                                                                                                               |
| Ensembl_Transcript_ID_2            | Ensembl transcript identifier for the second gene.                                                                                                                                              |
| direction1                         | Genomic direction for the first gene relative to the fusion breakpoint.                                                                                                                          |
| direction2                         | Genomic direction for the second gene relative to the fusion breakpoint.                                                                                                                         |
| filters                            | Filters applied to the fusion call (e.g., duplicate filtering criteria).                                                                                                                         |
| fusion_transcript                  | The predicted fusion transcript sequence or identifier.                                                                                                                                         |
| peptide_sequence                   | The full predicted peptide sequence resulting from the fusion event.                                                                                                                            |
| peptide_sequence_short             | A shortened version of the predicted peptide sequence.                                                                                                                                           |
| Split_reads_criteria_met           | Indicates whether the criteria for split reads were met (Yes/No).                                                                                                                                  |
| Epitope_spanning_breakpoint        | Indicates whether the predicted epitope spans the fusion breakpoint (Yes/No).                                                                                                                    |
| Distance_bp_breakspoints           | The distance in base pairs between the two fusion breakpoints.                                                                                                                                    |
| hydro_frac_mut                     | The fraction of hydrophobic residues in the mutant epitope.                                                                                                                                       |

## MHCII_RNAbamOpt.xlsx

| **Column**                     | **Annotation / Description**                                                                                                                                                                 |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Position                       | Identifier or index for the fusion event (e.g., a row number).                                                                                                                               |
| MHC_allele                     | The MHC/HLA allele used for epitope binding predictions (e.g., DRB1_1501).                                                                                                                   |
| Mutant_epitope                 | The predicted mutant epitope sequence derived from the fusion event.                                                                                                                         |
| Of                             | A parameter value from the binding prediction tool; refer to its documentation for details.                                                                                                  |
| Core                           | The core epitope sequence used for binding prediction.                                                                                                                                       |
| Core_Rel                       | A relative measure or score associated with the core epitope (e.g., reflecting its binding relevance).                                                                                       |
| Identity                       | A label or identifier for the fusion event (e.g., fusion5).                                                                                                                                  |
| Score_EL_Mut                   | The eluted ligand (EL) score for the mutant epitope.                                                                                                                                         |
| Rank_EL_Mut                    | The percentile rank of the mutant epitope’s EL score (lower values indicate stronger binding).                                                                                               |
| Exp_Bind                       | Expected binding metric or an experimental binding parameter; see associated documentation for details.                                                                                     |
| Score_BA_Mut                   | The binding affinity (BA) score for the mutant epitope.                                                                                                                                      |
| Aff.nM_Mut                     | The predicted binding affinity for the mutant epitope, expressed in nanomolar (nM).                                                                                                          |
| Rank_BA_Mut                    | The percentile rank of the mutant epitope’s binding affinity score (lower values indicate stronger binding).                                                                                 |
| BindLevel_Mut                  | Qualitative binding level for the mutant epitope (e.g., WB for weak binder).                                                                                                                 |
| Official_Gene_Symbol_1         | The official gene symbol for the first gene involved in the fusion.                                                                                                                          |
| Official_Gene_Symbol_2         | The official gene symbol for the second gene involved in the fusion.                                                                                                                         |
| strand1.gene.fusion.           | The strand orientation of the first gene in the fusion (e.g., -/-).                                                                                                                          |
| strand2.gene.fusion.           | The strand orientation of the second gene in the fusion (e.g., +/-).                                                                                                                         |
| breakpoint1                    | The genomic breakpoint position for the first gene in the fusion event.                                                                                                                     |
| breakpoint2                    | The genomic breakpoint position for the second gene in the fusion event.                                                                                                                    |
| site1                          | The genomic site annotation (e.g., CDS, intron, splice-site) for the breakpoint in the first gene.                                                                                          |
| site2                          | The genomic site annotation for the breakpoint in the second gene.                                                                                                                          |
| type                           | The type of fusion event (e.g., deletion/5'-5').                                                                                                                                            |
| split_reads1                   | The number of split reads supporting the fusion call for the first gene.                                                                                                                   |
| split_reads2                   | The number of split reads supporting the fusion call for the second gene.                                                                                                                  |
| discordant_mates               | The number of discordant mate pairs supporting the fusion event.                                                                                                                           |
| coverage1                      | The read coverage at the breakpoint for the first gene.                                                                                                                                    |
| coverage2                      | The read coverage at the breakpoint for the second gene.                                                                                                                                   |
| confidence                     | The confidence level of the fusion call (e.g., medium).                                                                                                                                     |
| reading_frame                  | The reading frame of the fusion product (e.g., out-of-frame).                                                                                                                               |
| tags                           | Additional tags or annotations associated with the fusion event.                                                                                                                          |
| retained_protein_domains       | Protein domains retained in the fusion product, including percentage matches where applicable.                                                                                             |
| closest_genomic_breakpoint1    | The closest genomic breakpoint near the first gene’s fusion breakpoint.                                                                                                                    |
| closest_genomic_breakpoint2    | The closest genomic breakpoint near the second gene’s fusion breakpoint.                                                                                                                   |
| Ensembl_Gene_ID_1              | Ensembl gene identifier for the first gene involved in the fusion.                                                                                                                         |
| Ensembl_Gene_ID_2              | Ensembl gene identifier for the second gene involved in the fusion.                                                                                                                        |
| Ensembl_Transcript_ID_1        | Ensembl transcript identifier for the first gene.                                                                                                                                         |
| Ensembl_Transcript_ID_2        | Ensembl transcript identifier for the second gene.                                                                                                                                        |
| direction1                     | The genomic direction for the first gene relative to the fusion breakpoint (e.g., upstream, downstream).                                                                                     |
| direction2                     | The genomic direction for the second gene relative to the fusion breakpoint.                                                                                                               |
| filters                        | Filters applied to the fusion call (e.g., duplicate criteria).                                                                                                                             |
| fusion_transcript              | The predicted fusion transcript sequence or its identifier.                                                                                                                               |
| peptide_sequence               | The full predicted peptide sequence resulting from the fusion event.                                                                                                                       |
| peptide_sequence_short         | A shortened version of the predicted peptide sequence.                                                                                                                                    |
| Split_reads_criteria_met       | Indicator of whether the split read criteria for fusion detection were met (Yes/No).                                                                                                         |
| Epitope_spanning_breakpoint    | Indicator of whether the predicted epitope spans the fusion breakpoint (Yes/No).                                                                                                             |
| Distance_bp_breakspoints       | The distance between the two fusion breakpoints, measured in base pairs.                                                                                                                     |
| hydro_frac_mut                 | The fraction of hydrophobic residues in the mutant epitope.                                                                                                                                 |

## fusions.tsv_splitGenes.xlsx

| **Column**                     | **Description**                                                                                                                                          |
|--------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|
| Official_Gene_Symbol_1         | The official gene symbol for the first gene involved in the fusion.                                                                                |
| Official_Gene_Symbol_2         | The official gene symbol for the second gene involved in the fusion.                                                                               |
| strand1.gene.fusion.           | The strand orientation of the first gene in the fusion event (e.g., +/+, -/-).                                                                     |
| strand2.gene.fusion.           | The strand orientation of the second gene in the fusion event.                                                                                      |
| breakpoint1                    | The genomic breakpoint position for the first gene in the fusion event.                                                                            |
| breakpoint2                    | The genomic breakpoint position for the second gene in the fusion event.                                                                           |
| site1                          | The genomic region where the breakpoint occurs in the first gene (e.g., CDS, 3'UTR, splice-site).                                                  |
| site2                          | The genomic region where the breakpoint occurs in the second gene.                                                                                 |
| type                           | The type of fusion event (e.g., inversion, deletion, read-through).                                                                               |
| split_reads1                   | The number of split reads supporting the fusion call for the first gene.                                                                          |
| split_reads2                   | The number of split reads supporting the fusion call for the second gene.                                                                         |
| discordant_mates               | The number of discordant mate pairs supporting the fusion event.                                                                                  |
| coverage1                      | The read coverage at the breakpoint for the first gene.                                                                                           |
| coverage2                      | The read coverage at the breakpoint for the second gene.                                                                                          |
| confidence                     | The confidence level of the fusion call (e.g., medium, low).                                                                                      |
| reading_frame                  | The reading frame of the fusion product (e.g., in-frame, out-of-frame, stop-codon).                                                              |
| tags                           | Additional tags or annotations associated with the fusion event.                                                                                  |
| retained_protein_domains       | Protein domains retained in the fusion product, including percentage matches where applicable.                                                    |
| closest_genomic_breakpoint1    | The closest genomic breakpoint near the first gene’s fusion breakpoint.                                                                           |
| closest_genomic_breakpoint2    | The closest genomic breakpoint near the second gene’s fusion breakpoint.                                                                          |
| Ensembl_Gene_ID_1              | Ensembl gene identifier for the first gene involved in the fusion.                                                                                |
| Ensembl_Gene_ID_2              | Ensembl gene identifier for the second gene involved in the fusion.                                                                               |
| Ensembl_Transcript_ID_1        | Ensembl transcript identifier for the first gene.                                                                                                 |
| Ensembl_Transcript_ID_2        | Ensembl transcript identifier for the second gene.                                                                                                |
| direction1                     | The genomic direction of the first gene relative to the fusion breakpoint (e.g., upstream, downstream).                                           |
| direction2                     | The genomic direction of the second gene relative to the fusion breakpoint.                                                                      |
| filters                        | Filters applied to the fusion call (e.g., duplicates).                                                                                            |
| fusion_transcript              | The predicted fusion transcript sequence or its identifier.                                                                                      |
| peptide_sequence               | The full predicted peptide sequence resulting from the fusion event.                                                                             |
| read_identifiers               | List of read identifiers supporting the fusion event.                                                                                             |


# Gene expression
## \*.fpkm_tpm.featureCounts.tsv.xlsx

| **Column**         | **Description**                                                                                   |
|--------------------|-------------------------------------------------------------------------------------------------|
| X.chrom           | Chromosome number where the gene is located.                                                     |
| chromStart        | Start position of the gene on the chromosome.                                                    |
| chromEnd          | End position of the gene on the chromosome.                                                      |
| gene_id           | Ensembl gene identifier with version number.                                                     |
| score             | Score field (if applicable, otherwise represented as ".").                                       |
| strand            | The strand orientation of the gene ("+" for forward, "-" for reverse).                          |
| Official_Gene_Symbol | Official gene symbol corresponding to the gene.                                              |
| exonic_length     | The total length of exonic regions for the gene.                                                 |
| num_reads         | The total number of reads mapped to the gene.                                                    |
| num_reads_fw      | The number of forward-strand reads mapped to the gene.                                          |
| num_reads_rv      | The number of reverse-strand reads mapped to the gene.                                          |
| FPKM              | Fragments Per Kilobase of transcript per Million mapped reads (overall).                         |
| FPKM_fw           | FPKM value for forward-strand reads.                                                             |
| FPKM_rv           | FPKM value for reverse-strand reads.                                                             |
| TPM               | Transcripts Per Million (overall expression level).                                              |
| TPM_fw            | TPM value for forward-strand reads.                                                              |
| TPM_rv            | TPM value for reverse-strand reads.                                                              |
| FPKM_legacy       | Legacy FPKM value, calculated with an older method.                                             |
| FPKM_legacy_fw    | Legacy FPKM for forward-strand reads.                                                           |
| FPKM_legacy_rv    | Legacy FPKM for reverse-strand reads.                                                           |
| TPM_legacy        | Legacy TPM value, calculated with an older method.                                              |
| TPM_legacy_fw     | Legacy TPM for forward-strand reads.                                                             |
| TPM_legacy_rv     | Legacy TPM for reverse-strand reads.                                                             |

## wish_list_genes_expression.csv.xlsx
    Same column as .fpkm_tpm.featureCounts.tsv.xlsx but only for genes in wish-list.
## fpkm_COL6A3_exon6.txt
    FPKM and reads information only for gene COLA3's specific exon exon6.


