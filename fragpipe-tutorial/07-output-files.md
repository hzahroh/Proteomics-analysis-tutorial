# Understanding FragPipe Output

When FragPipe finishes successfully, the output folder contains many files and subfolders. At first glance, this can seem overwhelming.

Fortunately, you do not need to understand every file immediately. Most downstream protein-level analyses use only a small number of outputs.

In this module, you will learn how to:

- confirm that the workflow completed successfully
- identify the main output files
- understand what each file contains
- choose the appropriate file for downstream analysis

---

# Output Folder Structure

After the workflow finishes, your output directory will contain several folders and text files.

A simplified example is shown below.

```text
FragPipe_Output/
│
├── psm.tsv
├── ion.tsv
├── peptide.tsv
├── protein.tsv
├── combined_ion.tsv
├── combined_peptide.tsv
├── combined_protein.tsv
├── MSstats.csv
├── log_[timestamp].txt
└── reports/
```

The exact contents depend on the selected workflow and FragPipe version.

---

# Did the Analysis Finish Successfully?

Before looking at the results, first confirm that the workflow completed without errors.

Check that:

- the console ends with **DONE**
- no error messages are reported
- the output folder contains the expected files
- a complete log file has been generated

If the workflow stopped unexpectedly, inspect the log for troubleshooting.

---

# Understanding the Output Files

FragPipe generates results at several different levels.

```text
PSM
    ↓
Peptide ion
    ↓
Peptide
    ↓
Protein
```

These levels are related, but they are not identical.

- A PSM assigns a peptide sequence to an MS/MS spectrum.
- A peptide ion is defined by its peptide sequence, modification state, and charge.
- A peptide report collapses different charge states and modified forms into a stripped peptide sequence.
- A protein group is inferred from the available peptide evidence, including unique and shared peptides.

Protein-level results therefore involve protein inference rather than simply adding together all rows from the peptide report.

---

# Which File Should I Use?

Different research questions require different output files.

| Goal | Recommended file |
|------|------------------|
| Inspect peptide identifications | `psm.tsv` |
| Study peptide ions | `ion.tsv` |
| Study peptides | `peptide.tsv` |
| Compare protein abundance | `combined_protein.tsv` |

For this tutorial, we will use **combined_protein.tsv** as the starting point for statistical analysis.

---

# Preparing for MetaboAnalyst

Although `combined_protein.tsv` contains protein abundance data, it is **not** yet ready for direct import into MetaboAnalyst.

Before importing the data, we will:

- remove unnecessary columns
- retain protein identifiers
- prepare the abundance matrix
- check for missing values

These steps are covered in the MetaboAnalyst module.

---

# Common Beginner Questions

### Why are there so many output files?

Different files summarize the data at different stages of the workflow, from peptide-spectrum matches to protein-level quantification.

---

### Which file should I analyse?

For most protein-level differential abundance studies, start with **combined_protein.tsv**.

---

### Do I need every output file?

No.

Most projects only use a small subset of the outputs, while the remaining files provide supporting information for quality control, troubleshooting, or more detailed analyses.

---
