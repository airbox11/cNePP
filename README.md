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

This pipeline is designed for **neoepitope discovery** and **comprehensive data processing** in cancer research. Its primary objectives include:  
1. Identifying neoantigens using advanced tools like NetMHCpan.  
2. Integrating HLA typing, SNV analysis, expression data, and other omics data.  
3. Performing variant and indel predictions to enhance downstream analysis.  
4. Preparing results in a user-friendly format (e.g., XLSX) for public sharing or further research.  
5. Supporting both clinical and research applications through robust workflows and modular execution of steps.  

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

1. **Preparation**:  
   - **`s0`**: Set up folders and initialize the environment.  

2. **HLA Typing**:  
   - **`s1a_HLA`**: Perform HLA typing (step 1a).  
   - **`s1b_HLA`**: Perform HLA typing (step 1b).  

3. **Variant Analysis**:  
   - **`s2_snv`**: Single Nucleotide Variant (SNV) analysis.  
   - **`i4a_indel_predict`**: Indel prediction.  

4. **Expression Data Integration**:  
   - **`s3_add_expression`**: Add expression data to the analysis.  

5. **Neoantigen Prediction**:  
   - **`f3`**: Predict potential neoantigens.  

6. **Fusion Detection**:  
   - **`f1a`**: Run STAR and Arriba to detect gene fusions.  

7. **Data Filtering and Formatting**:  
   - **`s8a_filter`**: Filter processed data.  
   - **`s8b_xlsx_to_public`**: Convert filtered data to a public format (e.g., XLSX).  

8. **Additional Predictions**:  
   - **`f4`**: MER21 prediction.  
   - **`f5`**: Convert data to XLSX format for downstream analysis.  

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