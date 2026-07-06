# FragPipe Tutorial

## FragPipe General Workflow
1. Prepare LC-MS/MS RAW files
2. Download a protein sequence database (FASTA)
3. Configure FragPipe search parameters
4. Perform peptide-spectrum matching (PSM) with MSFragger
5. Infer proteins using ProteinProphet
6. Quantify proteins using IonQuant
7. Export quantitative protein abundance tables
8. Import the results into MetaboAnalyst

## Tutorial Contents
1. [Introduction](01-introduction.md)
2. [Understanding the FragPipe Workflow](02-workflow.md)
3. [Installation](03-installation.md)
4. [Preparing Input Files](04-input-files.md)
5. [Search Parameters](05-search-parameters.md)
6. [Running FragPipe](06-running-fragpipe.md)
7. [Output Files](07-output-files.md)
8. [Quality Control](08-quality-control.md)
9. [Troubleshooting](09-troubleshooting.md)
10. [Exercises](10-exercises.md)

## Output Files
After completing this tutorial, you should obtain
- Peptide-spectrum matches (PSMs)
- Identified peptides
- Protein groups
- Label-free protein intensities
- MaxLFQ protein abundance matrix (`combined_protein.tsv`)

The `combined_protein.tsv` file will be used in the **MetaboAnalyst Tutorial**.

## How to Start
Start with Chapter 1: [Introduction](01-introduction.md)
Once you complete with FragPipe Tutorial, continue to MetaboAnalyst Tutorial. 

## Citation
If you use this tutorial in teaching or workshop, please cite this GitHub repository, FragPipe, MSFragger, IonQuant and the PRIDE dataset (PXD072757). 

## Acknowledgments
We acknowledge the developers of
- FragPipe
- MSFragger
- Philosopher
- IonQuant
- PRIDE Archive
- UniProt
- MetaboAnalyst



