
# {targets} pipeline to process amplicon sequencing data with dada2

This [{targets}](https://books.ropensci.org/targets/) reproducible
pipeline contains amplicon sequencing data processing using
[{dada2}](https://benjjneb.github.io/dada2/). It also generates a Quarto report detailing the
steps of the pipeline.

## Package versions

Package versions are recorded using
[{renv}](https://rstudio.github.io/renv/) and can be restored using
`renv::restore()`.

## Raw data

Raw data can be downloaded at **link** and should be placed in
`data/01_raw_data`. The MD5 for the raw data can be checked from
`data/01_raw_data/MD5.txt`.

## How to run the pipeline

### Environment set up
1. `git clone git@github.com:marccamb/dada2_targets.git .` to clone the repository on your machine
1. `install.packages("renv")` to install {renv} from CRAN
2. `renv::activate()` to activate the {renv} environment  
2. `renv::restore()` to install all packages and dependancies for the pipeline
1.  `library(targets)` to load the {targets} package

### Data download and paths setting

1. Download your raw, demultiplexed, fastq data into 'data/02_sample_demultiplexing' (see [Sample demultiplexing](#sample-demultiplexing) on how to demultiplex your samples)
2. Create a CSV file containing the sample name / tag correspondance following `data/00_metadata/sample_tags.csv`
3. **Reference database in the dada2 format**
4. Update paths in the `_targets.R` file:
    - `taxo_db_path` :
    - `run_values` : 

### Checking and running the pipeline 

2.  `tar_manifest()` and `tar_visnetwork()` to check the pipeline for correctness.
3.  `tar_make()` similar to run the pipeline.
4.  `tar_read()` to read target output.

### Files

-   `R/` contains the custom function used in the pipeline
-   `_targets.R` contains the pipeline configuration and definition
-   `data/00_metadata/` contains the metadata files used for sequence
    processing
-   `data/00_taxonomy_DB/` a dada2 formatted reference database should be saved in this folder before running the pipeline.
-   `data/01_raw_data` contains the MD5 hash for the raw data file. The
    raw data file should be saved in this folder before running the
    pipeline.
-   `data/0[23]*` contain outputs of the pipeline

## Sample demultiplexing

The demultiplexing of samples is not part of the pipeline but the steps are as follows:

1. Download and decompress your raw multiplexed fastq files in `data/01_raw_data`