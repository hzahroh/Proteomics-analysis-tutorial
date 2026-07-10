# Configuring Search and Validation Parameters

FragPipe includes several built-in workflows that automatically configure most of the required settings. In practice, you only need to review a small number of parameters before running the analysis.

This module explains the key parameters used in this tutorial and why they were selected.

## 1. Choosing a Workflow

A workflow is simply a predefined set of settings for database searching, validation, protein inference, quantification, and report generation.
For this tutorial, we use the LFQ-MBR workflow. FragPipe describes this workflow as a closed database search followed by label-free quantification and match-between-runs using IonQuant.

The default LFQ-MBR workflow is well suited for:

- bottom-up proteomics
- enzymatically digested samples
- unlabelled experiments
- DDA data
- MS1 intensity-based quantification
- relative protein-abundance comparisons across samples or biological groups

The LFQ-MBR workflow is not appropriate for every experiment. Different workflows or settings should be used for applications such as:

- DIA analysis
- TMT or iTRAQ quantification
- SILAC or other MS1-labelling experiments
- open searches for unexpected modifications
- specialised phosphoproteomic or glycoproteomic analyses
- endogenous plasma peptidomics

FragPipe provides separate workflows for many of these applications, including DIA, TMT, SILAC, open-search, phosphoproteomic, glycoproteomic, and nonspecific peptidome analyses.

Workflow settings may change between FragPipe releases. After loading the workflow, verify the displayed settings and record the FragPipe and software versions used for the analysis.

## 2. Enzyme and Digestion Settings

The enzyme setting tells FragPipe how the proteins were digested before LC-MS/MS analysis. This is an important setting because it determines which peptide sequences are generated from the FASTA database and included in the database search.

In this tutorial, the proteins were digested with **trypsin**, so we use:

```text
Strict Trypsin
```

In FragPipe, the **Strict Trypsin** digestion rule is implemented as **Trypsin/P**. Unlike the conventional trypsin rule, which does not cleave when lysine (K) or arginine (R) is followed by proline (P), Trypsin/P allows cleavage at these sites. Therefore, it is best to use the workflow default rather than replacing it with another trypsin rule unless your experimental protocol requires a different enzyme or digestion specificity.

As a general rule, always choose the enzyme setting that matches your sample preparation. Only change the workflow default if your proteins were digested using a different enzyme, such as Lys-C or chymotrypsin, or if your experiment requires a semi-enzymatic or nonspecific search.

---

### Fully Enzymatic Search

The LFQ-MBR workflow performs a fully enzymatic search.

This means both ends of an internal peptide are expected to follow the cleavage pattern of the selected enzyme. The natural N-terminus and C-terminus of a protein are also accepted as peptide boundaries.

For most trypsin-digested bottom-up proteomics experiments, a fully enzymatic search is the appropriate choice because it reflects how the peptides were generated during sample preparation.

Semi-enzymatic or nonspecific searches should only be used when there is a clear experimental or biological reason to do so. Since these searches consider many more candidate peptides, they substantially increase the search space, memory requirements, and processing time.

---

### Missed Cleavages

Protein digestion is rarely perfect. Occasionally, trypsin misses a cleavage site, producing a longer peptide than expected. These are known as **missed cleavages**.

For this tutorial, allow a maximum of:

```text
2
```

missed cleavages.

Allowing up to two missed cleavages is the standard setting for FragPipe's default fully tryptic closed-search workflow. It provides a good balance between identifying peptides from incomplete digestion and keeping the database search efficient.

Increasing the number of allowed missed cleavages may improve peptide identification when digestion is incomplete, but it also:

- increases the number of candidate peptides
- enlarges the search space
- increases memory usage
- lengthens the analysis time

## 3. Mass Tolerances

Mass tolerances define how closely the measured masses must match the theoretical peptide masses during the database search.

Two mass tolerances are used:

| Parameter | Purpose |
|-----------|---------|
| **Initial precursor tolerance** | Matches the measured precursor-ion (MS1) mass to the theoretical peptide mass |
| **Initial fragment tolerance** | Matches the measured fragment-ion (MS/MS) masses to the theoretical fragment-ion masses |

For this tutorial, use:

| Parameter | Value |
|-----------|------:|
| Initial precursor tolerance | ±20 ppm |
| Initial fragment tolerance | 20 ppm |

These are the recommended starting values for high-resolution Orbitrap data.

> [!IMPORTANT]
> A fragment mass tolerance of **20 ppm** is appropriate only when the MS/MS spectra were acquired at **high resolution**, such as on an Orbitrap. If the fragment ions were measured using a low-resolution analyser, such as an ion trap, a wider tolerance expressed in **daltons (Da)** should be used instead.

---

## 4. Peptide and Protein Modifications

Chemical and biological modifications change the mass of peptides, so they must be considered during database searching.

FragPipe classifies modifications into two types:

- **Fixed modifications**
- **Variable modifications**

---

### Fixed Modifications

A fixed modification is applied to every occurrence of a specified amino acid or protein terminus during the database search.

For this tutorial, use:

```text
Carbamidomethylation of cysteine
C +57.02146 Da
```

This modification is appropriate when cysteines have been alkylated during sample preparation using reagents such as **iodoacetamide**, which produces carbamidomethylated cysteine.

Do **not** use this fixed modification if:

- cysteines were not alkylated
- a different alkylating reagent was used
- your experiment is investigating incomplete or differential cysteine modification

The standard FragPipe closed-search workflow includes **C +57.02146** as a fixed modification because it assumes cysteine alkylation during sample preparation.

### Variable Modifications

Unlike a fixed modification, a **variable modification** may or may not be present on a peptide.

During the database search, MSFragger considers both the modified and unmodified forms of a peptide and determines which one better matches the experimental MS/MS spectrum.

For this tutorial, use the following variable modifications:

```text
Methionine oxidation
M +15.9949 Da
```

and

```text
Protein N-terminal acetylation
Protein N-term +42.0106 Da
```

These are included in FragPipe's standard closed-search workflow and are commonly used for bottom-up proteomics experiments.

> [!NOTE]
> **Protein N-terminal acetylation** applies only to the N-terminus of the intact protein. It is different from peptide N-terminal acetylation, which allows acetylation at the N-terminus of every peptide.

Only include modifications that are expected based on your sample preparation or are directly relevant to your biological question. If your goal is to search for unexpected mass shifts, an open search is usually a better choice than adding many variable modifications to a closed search.

---

## 5. Identification Validation and False Discovery Rate

A database search does not guarantee that every peptide-spectrum match (PSM) is correct. Some matches occur by chance, especially when searching large protein databases.

To improve confidence in the results, FragPipe validates the identifications and filters them using a **false discovery rate (FDR)**.

For this tutorial, use an FDR threshold of:

```text
1%
```

The exact reporting levels depend on the selected workflow.

An FDR of **1%** means that, on average, about 1% of the accepted identifications at a given reporting level are expected to be incorrect.

It does **not** mean that:

- every accepted identification has exactly a 1% chance of being incorrect
- exactly one out of every 100 accepted identifications must be false
- a 1% FDR at the PSM level automatically gives a 1% FDR at the peptide or protein level

FragPipe can estimate and apply FDR independently at several levels, including:

- peptide-spectrum matches (PSMs)
- peptide ions
- peptides
- proteins

The workflow determines which levels are filtered. After loading a workflow, it is good practice to review the settings in the **Validation** tab.

---

### Target-Decoy Strategy

FragPipe estimates the false discovery rate using a **target-decoy** strategy.

During database preparation, the FASTA file contains two types of protein sequences:

- **Target sequences**, representing the proteins that may be present in the sample.
- **Decoy sequences**, artificial protein sequences used to estimate the number of false identifications.

During the search, peptide-spectrum matches are generated against both target and decoy sequences. Because decoy proteins are not expected to be present in the sample, matches to these sequences provide an estimate of how many incorrect target matches are likely to pass a given score threshold.

As the score threshold becomes more stringent, fewer target and decoy matches are accepted. FragPipe uses this information to determine the score threshold that achieves the selected FDR.

An FDR of **1%** is widely used in discovery proteomics because it provides a good balance between identification sensitivity and confidence.

# Summary

For this tutorial, we will use the **LFQ-MBR** workflow because it is designed for **label-free quantification of DDA data**. Most of the default settings are appropriate for our dataset, only a few parameters need to be reviewed before starting the analysis.

Use the checklist below to confirm that your search settings match your experiment.

| Parameter | Setting |
|-----------|---------|
| Workflow | LFQ-MBR |
| Data type | DDA |
| Enzyme | Strict Trypsin (Trypsin/P) |
| Digestion specificity | Fully enzymatic |
| Maximum missed cleavages | 2 |
| Initial precursor tolerance | ±20 ppm |
| Initial fragment tolerance | 20 ppm |
| Mass Calibration and Parameter Optimization | Enabled |
| Fixed modification | Carbamidomethylation of cysteine |
| Variable modifications | Methionine oxidation, Protein N-terminal acetylation |
| False discovery rate (FDR) | 1% |

For most experiments similar to this tutorial, the remaining settings can be left at their default values.

---

## Checkpoint

Before moving to the next module, make sure you can answer the following questions:

- [ ] Why is the **LFQ-MBR** workflow suitable for this tutorial?
- [ ] Why should the enzyme setting match your sample preparation?
- [ ] What is a fully enzymatic search?
- [ ] Why are missed cleavages allowed?
- [ ] What is the difference between **fixed** and **variable** modifications?
- [ ] What does an FDR of **1%** mean?

