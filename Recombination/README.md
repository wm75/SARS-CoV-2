# Recombinaton analysis

## Whats the point?

[Wu et al.](https://doi.org/10.1038/s41586-020-2008-3) showed recombination between COVID-19 and bat coronoviruses located within the *S*-gene. We wanted to confirm this observation and provide a publicly accessible workflow for recombination detection.

## Outline

We employed recombination detection algorithm developed by [Kosakovsky Pond et al.](http://mbe.oxfordjournals.org/cgi/content/full/23/10/1891) and implemented in `hyphy` package. To select a representative set of *S*-genes we performed a blast search using *S*-gene CDS from [NC_045512](https://www.ncbi.nlm.nih.gov/nuccore/NC_045512) as a query against the `nr` database. We selected coding regions corresponding to the *S*-gene from a number of COVID-19 genomes, original SARS isolates. This set of sequences can be found in [this repository](S_nt.fna)

We then generated a codon-based alignment using workflow shown below and performed analysis using `gard` tool from `hyphy` package. 

## Inputs

A set of unaligned CDS sequences for the *S*-gene.

## Outputs

A recombination report:

![](dm_report.png)

and a map of possible recombination hotspots:

![](dm_chart.png)

## History and workflow

Galaxy workspace (history) containing the most current analysis can be imported from [here](https://usegalaxy.org/u/aun1/h/ncov-comp).

The [workflow](https://test.galaxyproject.org/u/anton/h/ncov-recomb) is available at Galaxy public site and can downloaded and installed on any Galaxy instance. It contains version information for all tools used in this analysis. 

![](rec_wf.png)

The workflow takes unaligned CDS sequences, translates them with `EMBOSS:tanseq`, aligns translations using `mafft`, realigns original CDS input using mafft alignment as a guide and sends this codon-based alignment to `gard`.

## BioConda

Tools used in this analysis are also available from BioConda:

| Name | Link |
|------|----------------|
| `emboss` | [![Anaconda-Server Badge](https://anaconda.org/bioconda/emboss/badges/version.svg)](https://anaconda.org/bioconda/emboss) |
| `mafft` | [![Anaconda-Server Badge](https://anaconda.org/bioconda/mafft/badges/version.svg)](https://anaconda.org/bioconda/mafft) |
| `hyphy` | [![Anaconda-Server Badge](https://anaconda.org/bioconda/hyphy/badges/version.svg)](https://anaconda.org/bioconda/hyphy) |