# Human GO Biological Process GSEA

This repository runs Gene Set Enrichment Analysis (GSEA) on a
differential-expression results file containing human gene symbols,
log fold changes, and p-values.

## Before you start

Install R and RStudio on your computer.

Download this repository using:
Code → Download ZIP

Unzip the downloaded folder.

## First-time setup

1. Open RStudio.
2. Select File → New Project → Existing Directory.
3. Select the unzipped repository folder.
4. In the RStudio Console, run:

```r
source("install_packages.R")
```

Package installation requires an internet connection and may take a while.

## Prepare your input

Download your differential-expression file to your computer.

The input must be a tab-separated `.txt` file with these exact columns:

- PG.Genes: human gene symbols
- logFC: numeric log fold changes
- P.Value: numeric p-values

Other columns are allowed.

Example format:

```text
PG.Genes	logFC	P.Value
GENE_A	1.2	0.003
GENE_B	-0.8	0.020
```

The example above illustrates formatting only; it is not an analysis dataset.

Use one gene symbol per row. If your file contains protein IDs or
multiple gene symbols in one cell, ask your supervisor before running.

Use the full differential-expression table, not only significant genes.

## Run an analysis

In the RStudio Console, run:

```r
source("run_analysis.R")
```

A file-selection window will open. Select your input `.txt` file.

## Outputs

Two files are saved in the same folder as the input file:

- A PDF dot plot of GO Biological Process enrichment
- A tab-separated GSEA results table

The input file is not changed.

To analyze another input file, run:

```r
source("run_analysis.R")
```

again and select the new file.

Rerunning the same input will overwrite its previous outputs.

## How genes are ranked

Ranking score:

R = -log10(P.Value) × sign(logFC)

Positive log fold changes receive positive scores.
Negative log fold changes receive negative scores.
Smaller p-values produce larger absolute scores.

Duplicate gene symbols are reduced to the first row encountered.

## Interpreting the plot

The x-axis shows normalized enrichment score (NES).
Dot color shows adjusted p-value.

Positive NES indicates enrichment toward the positive-logFC end
of the ranked list.

Negative NES indicates enrichment toward the negative-logFC end.

Check how your original experimental comparison defines logFC
before interpreting these directions.

The pipeline uses pvalueCutoff = 1, so plotted pathways are not
necessarily statistically significant. Check p.adjust in the results.

## Troubleshooting

“Cannot open GSEA_batch_pipeline.R”:
Make sure you opened the repository folder as your RStudio project.

“There is no package called ...”:
Run source("install_packages.R") and check for installation errors.

Missing PG.Genes, logFC, or P.Value:
Check that the input has the required column names exactly.

If another error appears:
Send your supervisor the full Console error and the input filename.
