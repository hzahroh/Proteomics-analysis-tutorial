# Running FragPipe

In this module, you will load the **LFQ-MBR** workflow, import the spectral files, assign the experimental design, verify the identification and quantification settings, and start the complete analysis.

> [!NOTE]
> The exact appearance and location of some options may differ slightly between FragPipe versions. Record the FragPipe and software versions used for the analysis.

---

## Learning Objectives

By the end of this module, you will be able to:

* Load the appropriate FragPipe workflow.
* Configure the main computational settings.
* Import RAW files and assign the correct data type.
* Select the protein FASTA database.
* Assign experiments and biological replicates.
* Verify the search, validation, and IonQuant settings.
* Start and monitor a complete DDA label-free proteomics analysis.
* Determine whether the workflow finished successfully.

---

# Workflow Overview

The overall procedure consists of the following steps:

```text
Load workflow
      ↓
Configure computational settings
      ↓
Import RAW files
      ↓
Verify DDA data type
      ↓
Select FASTA database
      ↓
Assign Experiment and BioReplicate
      ↓
Review search and validation settings
      ↓
Review IonQuant settings
      ↓
Choose output folder
      ↓
Run FragPipe
      ↓
Check log file and result folder
```

---

# Step 1. Load the Workflow

Open the **Workflow** tab.

From the **Select a workflow** drop-down menu, choose:

```text
LFQ-MBR
```

Click **Load**.

![FragPipe Choosing Workflow](https://github.com/hzahroh/Proteomics-analysis-tutorial/blob/main/images/FragPipe-choosing-workflow.png)

**Figure 1.** Choosing workflow in FragPipe

The LFQ-MBR workflow configures a closed MSFragger database search followed by identification validation, protein grouping, FDR filtering, and IonQuant label-free quantification with match-between-runs.

Loading the workflow automatically fills settings across several FragPipe tabs. You should still verify the settings that depend on your sample preparation and instrument.


---

# Step 2. Configure the Computational Settings

The **Workflow** tab contains settings that control the computational resources used by FragPipe.

## RAM

For a standard desktop analysis, leave:

```text
RAM (GB): 0
```

A value of `0` allows FragPipe to detect the available memory and allocate a safe amount automatically. On some high-performance computing systems, automatic memory detection may not work correctly, so the memory may need to be entered manually.

## Parallelism

The **Parallelism** or logical-core setting controls how much work FragPipe performs concurrently.

Increasing parallelism may reduce processing time, but it also increases the demand on:

* CPU cores
* system memory
* disk input/output

There is no universal parallelism value based only on the amount of RAM. The appropriate value also depends on:

* the number and size of the spectral files
* the complexity of the database search
* the number of variable modifications
* whether database splitting is used
* other programs running on the computer

For this tutorial, retain the value selected by FragPipe unless a memory-related error occurs.

> [!TIP]
> Setting parallelism to the highest available value does not always make the analysis faster. If the computer becomes unstable or the workflow fails because of insufficient memory, lower the parallelism and rerun the analysis.

## Instrument-data mode

Because this tutorial uses Orbitrap data, select:

```text
Regular MS
```

The **IM-MS** option is intended for Bruker timsTOF PASEF data. FragPipe recommends **Regular MS** for other data types, including Orbitrap and FAIMS data.

---

# Step 3. Import the RAW Files

In the **Workflow** tab, click **Add files** and select all the RAW files from the experiment.

You can also drag and drop files into the LC-MS files table.

If the files are distributed across several folders or subfolders, use:

```text
Add Folder Recursively
```

FragPipe will add compatible files found within the selected folder and its subfolders.

After importing the files, verify that:

* all expected RAW files are present
* no files have been added twice
* no samples, fractions, or technical injections are missing
* the file paths are correct

![Import RAW files](https://github.com/hzahroh/Proteomics-analysis-tutorial/blob/main/images/FragPipe-Import-raw-files.PNG)
**Figure 2.** RAW files loaded into the LC-MS files table.

In the **Experiment** column, assign each spectral file to its corresponding biological condition.

For this tutorial:

| Samples           | Experiment |
| ----------------- | ---------- |
| Healthy controls  | Healthy    |
| Dengue patients   | Dengue     |
| COVID-19 patients | COVID-19   |

Files belong to the same biological condition should use the same Experiment name.

Next, assign the **BioReplicate** values.

Each unrelated patient represents an independent biological replicate. Therefore, every patient should receive a unique identifier.

For example:

| RAW file       | Experiment | BioReplicate | Data type |
| -------------- | ---------- | -----------: | --------- |
| Healthy_01.raw | Healthy    |            1 | DDA       |
| Healthy_02.raw | Healthy    |            2 | DDA       |
| Dengue_01.raw  | Dengue     |            3 | DDA       |
| Dengue_02.raw  | Dengue     |            4 | DDA       |
| Covid_01.raw   | COVID-19   |            5 | DDA       |

---

# Step 4. Verify the Data Type

Check the **Data type** column for every imported file.

For this tutorial, each file should be assigned:

```text
DDA
```

FragPipe may automatically guess that the files contain DDA data, but the assignment should still be checked manually. The data-type setting controls how FragPipe uses each spectral file in the workflow.

Do not confuse the data type with the biological condition:

* **Data type** describes how the mass-spectrometry data were acquired or used.
* **Experiment** describes the biological condition or group.

---

# Step 5. Select the FASTA Database

Open the **Database** tab.

Click **Browse** and select the FASTA database prepared in Module 04.

The correct database depends on the objective of the tutorial.

Before continuing, confirm that:

* the intended target protein sequences are present
* common contaminant sequences are included
* decoy sequences have been added
* the decoy prefix displayed in FragPipe matches the database

> [!IMPORTANT]
> Do not add decoys to a database that already contains decoy sequences. Decoys should be added only once.

---

# Step 6. Review the Search and Validation Settings

Before starting the analysis, verify the settings reviewed in Module 05.

| Parameter                              | Tutorial setting                                        |
| -------------------------------------- | ------------------------------------------------------- |
| Workflow                               | LFQ-MBR                                                 |
| Enzyme                                 | Strict Trypsin, or Trypsin/P                            |
| Digestion specificity                  | Fully enzymatic                                         |
| Maximum missed cleavages               | 2                                                       |
| Initial precursor tolerance            | ±20 ppm                                                 |
| Initial fragment tolerance             | 20 ppm                                                  |
| Calibration and parameter optimization | Enabled                                                 |
| Fixed modification                     | Carbamidomethylation of cysteine                        |
| Variable modifications                 | Methionine oxidation and protein N-terminal acetylation |
| FDR                                    | 1% at the levels configured by the workflow             |

Check these settings in the **MSFragger** and **Validation** tabs.

If the settings match the experimental protocol and instrument described in this tutorial, no changes are required.

> [!IMPORTANT]
> Do not use these values automatically for a different enzyme, alkylation chemistry, acquisition method, or low-resolution MS/MS analyser.

---

# Step 7. Configure IonQuant

Open the **Quant (MS1)** tab.

For this tutorial, confirm that the following options are enabled:

```text
✓ Run MS1 Quant
✓ Match Between Runs (MBR)
✓ MaxLFQ
```

These options are enabled by default in the **LFQ-MBR** workflow.

### Run MS1 Quant

This option enables **IonQuant** to perform MS1-based label-free quantification. It should remain enabled for this tutorial.

### Match Between Runs (MBR)

Confirm that **Match Between Runs (MBR)** is enabled.

MBR helps reduce missing values by transferring peptide identifications between compatible LC-MS/MS runs. The underlying concept was introduced in **Module 02**.

### MaxLFQ

Confirm that **MaxLFQ** is enabled.

MaxLFQ calculates protein-level abundances from peptide intensities and produces the protein intensity values used in the downstream analyses in this tutorial.

> [!TIP]
> If you loaded the **LFQ-MBR** workflow, these options should already be selected. In most cases, no changes are required.

### Normalization

Leave the normalization setting selected by the **LFQ-MBR** workflow.

Normalization helps reduce systematic differences in signal intensity between LC-MS/MS runs. This makes protein abundances more comparable across samples.

For this tutorial, the default setting is appropriate and does not need to be changed.

> [!NOTE]
> The **Requantification** option is intended for certain isotope-labelled proteomics workflows (for example, SILAC). It is not used in this label-free tutorial, so leave the default setting unchanged.

---

# Step 8. Choose an Output Folder

Open the **Run** tab.

Click **Browse** and create or select a folder where the results will be saved. The official LFQ workflow instructs users to create the output folder before clicking RUN.

Keeping the output separate from the original spectral files helps keep the project organised.

For example:

```text
Proteomics_Project/
├── RAW/
├── FASTA/
├── Metadata/
└── FragPipe_Output/
```

Before running the analysis, confirm that:

* the folder path is correct
* sufficient free disk space is available
* results from a previous analysis will not be overwritten unintentionally


---

# Step 9. Perform a Final Review

Before clicking RUN, verify:

* the LFQ-MBR workflow is loaded
* Regular MS is selected
* all RAW files are present
* every file is assigned DDA
* Experiment names are correct
* BioReplicate identifiers are correct
* the intended FASTA database is selected
* contaminants and decoys are present
* search and validation parameters match the experiment
* Run MS1 quant is enabled
* MBR is enabled
* MaxLFQ is selected
* the output folder is correct


---

# Step 10. Start the Analysis

Click:

```text
RUN
```

FragPipe will execute the steps enabled by the LFQ-MBR workflow, including:

* MSFragger database searching
* feature prediction and rescoring
* peptide-spectrum match validation
* protein inference and grouping
* FDR filtering
* IonQuant MS1 quantification
* match-between-runs
* MaxLFQ protein quantification
* report generation

The exact tools and stages can vary between FragPipe versions and workflow configurations.

---

# Monitoring the Analysis

Progress is displayed in the console on the **Run** tab.

The console may show output from tools such as:

* MSFragger
* MSBooster
* Percolator
* ProteinProphet or related protein-grouping components
* Philosopher
* IonQuant

Do not close FragPipe, rename the input files, or move the FASTA database while the workflow is running.

Warnings do not always indicate that the workflow has failed. When troubleshooting, look for:

* `[ERROR]`
* a non-zero exit code
* an indication that a component stopped
* the absence of the final successful-completion message

---

# When Is the Analysis Finished?

When the run finishes successfully, FragPipe prints:

```text
ALL THE JOBS DONE
```

at the end of the console output.

![FragPipe RUN done](https://github.com/hzahroh/Proteomics-analysis-tutorial/blob/main/images/FragPipe-run-done.png)
**Figure 3.** Console showing the run done

Also verify that the output directory contains the expected files. Depending on the workflow configuration, these may include:

```text
psm.tsv
ion.tsv
peptide.tsv
protein.tsv
combined_ion.tsv
combined_peptide.tsv
combined_protein.tsv
MSstats.csv
log_[timestamp].txt
```

FragPipe saves a timestamped complete log when an analysis finishes successfully. If a run fails, the visible console can be saved using **Export Log** on the Run tab for troubleshooting.

Do not rely only on the presence of an output folder. A failed analysis may leave incomplete or intermediate files.

---

# Common Mistakes

| Problem                                                         | Corrective action                                                      |
| --------------------------------------------------------------- | ---------------------------------------------------------------------- |
| Parallelism set too high                                        | Reduce parallelism if memory-related failures occur                    |
| IonQuant not enabled                                            | Enable Run MS1 quant                                                   |
| MBR disabled unintentionally                                    | Enable MBR for this tutorial                                           |
| MaxLFQ not selected                                             | Select MaxLFQ if MaxLFQ protein values are required                    |
| Results saved with the RAW files                                | Use a dedicated output directory                                       |
| Output folder is present but the run failed                     | Check for `DONE` and inspect or export the complete log                |

---

