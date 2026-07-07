## Introduction
Mass spectrometry-based proteomics generates large and information-rich datasets, but computational analysis is required to convert raw mass spectra into peptide identifications and protein abundances. 
In this tutorial, you will learn how to analyse label-free data-dependent acquisition (DDA) proteomics data using FragPipe 24.0. You will identify peptides and proteins, quantify protein abundances, and generate output files that can be used for statistical analysis in MetaboAnalyst.

## What is FragPipe?
FragPipe is an open source software developed by [Alexey Nesvizhskii's proteome bioinformatics group](https://github.com/Nesvilab) that integrates several software tools into a single workflow for shotgun proteomics analysis. 
It is one of the most widely used software platforms for bottom-up proteomics data analysis. It provides a graphical interface that integrates several tools into one workflow.

Below are the tools and their functions:
| Tool | Function |
| :--- | :--- |
| **MSFragger** | Identifies peptides by matching MS/MS spectra to peptide sequences in a protein database. |
| **MSBooster** | Uses deep learning predictions to improve peptide-spectrum match confidence. |
| **Philosopher** | Performs database management, false discovery rate (FDR) estimation, and result filtering. |
| **ProteinProphet** | Infers protein groups from identified peptides. |
| **IonQuant** | Performs label-free protein quantification, including Match Between Runs (MBR) and MaxLFQ. |

## Bottom-up vs Top-down proteomics
Proteomics aims to identify and quantify proteins present in a biological sample. There are two main analytical strategies: **bottom-up proteomics** and **top-down proteomics**. They differ in how samples are prepared, analyzed, and interpreted.

## Bottom-up Proteomics

Bottom-up proteomics is the most widely used approach in biological and clinical research. Instead of analyzing intact proteins directly, proteins are first enzymatically digested into smaller peptides, which are then analyzed by liquid chromatography coupled with tandem mass spectrometry (LC-MS/MS).

Because peptides are much smaller and easier to separate and fragment than intact proteins, this approach enables the identification and quantification of thousands of proteins in a single experiment.

### Typical workflow

1. Protein extraction
2. Protein digestion (typically with trypsin)
3. Peptide separation by liquid chromatography (LC)
4. Tandem mass spectrometry (LC-MS/MS)
5. Computational analysis using software such as FragPipe
6. Statistical analysis and biological interpretation

### Advantages

- High protein identification coverage
- Suitable for complex biological samples
- Robust and reproducible
- Compatible with label-free and isobaric quantification
- Well-supported by software such as FragPipe, MaxQuant, and Proteome Discoverer

### Limitations

- Proteins are inferred indirectly from peptide sequences.
- Some protein isoforms cannot be distinguished because they share identical peptides.
- Information about combinations of post-translational modifications (proteoforms) may be lost.

### Common applications

- Biomarker discovery
- Disease proteomics
- Clinical plasma proteomics
- Cancer proteomics
- Host-pathogen interaction studies
- Differential protein expression analysis

---

## Top-down Proteomics

Top-down proteomics analyzes **intact proteins** without prior enzymatic digestion. Instead of identifying peptides, the mass spectrometer directly measures whole proteins and their fragment ions.

Because intact proteins are analyzed, top-down proteomics can accurately distinguish protein isoforms and characterize post-translational modifications occurring on the same protein molecule.

### Typical workflow

1. Protein extraction
2. Intact protein separation
3. High-resolution mass spectrometry
4. Fragmentation of intact proteins
5. Protein identification and proteoform characterization


### Advantages

- Direct analysis of intact proteins
- Identification of protein isoforms
- Characterization of complete proteoforms
- Accurate mapping of post-translational modifications

### Limitations

- Lower throughput than bottom-up proteomics
- More technically challenging
- Requires specialized instrumentation and computational methods
- Less suitable for highly complex biological samples

### Common applications

- Proteoform analysis
- Post-translational modification (PTM) characterization
- Structural biology
- Biopharmaceutical quality control
- Protein isoform identification

---

Comparison between bottom-up proteomics vs top-down proteomics

| Feature | Bottom-up Proteomics | Top-down Proteomics |
|----------|----------------------|---------------------|
| Analyte | Peptides | Intact proteins |
| Digestion required | Yes | No |
| Typical sample complexity | High | Low to moderate |
| Protein identification | Indirect (via peptides) | Direct |
| Proteoform characterization | Limited | Excellent |
| Throughput | High | Lower |
| Clinical applications | Very common | Limited |
| Data analysis software | FragPipe, MaxQuant, Proteome Discoverer | ProSight, TopPIC, TDPortal |

---



