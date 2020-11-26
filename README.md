[![depends](https://img.shields.io/badge/depends%20from-bioconda-brightgreen.svg)](http://bioconda.github.io/)
[![snakemake](https://img.shields.io/badge/snakemake-5.3-brightgreen.svg)](https://snakemake.readthedocs.io/en/stable/)

# RiDE
This is a fork of **[RiDE](https://github.com/solida-core/ride)** (RNA Differential Expression), a [Snakemake](https://snakemake.readthedocs.io/en/stable/)-based pipeline for Next-Generation Sequencing RNA-Seq differential expression analysis, developed at [CRS4 Next Generation Sequencing Core Facility](http://next.crs4.it). Software dependencies are directly managed by Snakemake using [Conda](https://docs.conda.io/en/latest/miniconda.html), ensuring the reproducibility of the workflow according to [FAIR](https://www.go-fair.org/fair-principles/) principles.

## Running RiDE
 * Clone the repository from git-hub:
```bash
git clone https://github.com/igg-bioinfo/ride.git
```

 * Rename the folder, from `ride` to your PROJECT_NAME:
```bash
mv ride PROJECT_NAME
```

 * cd into the newly created folder:
```bash
cd PROJECT_NAME
```

 * Edit the configuration files in **conf** subfolder:
   * config.yaml - paths to your reference files: genome, target regions, etc.
   * samples.tsv - associate samples to FASTQ files
   * units.tsv - paths to FASTQ files

 * Edit the **Snakefile** and uncomment the output files you need

 * If conda package manager is not available, install [miniconda](https://docs.conda.io/en/latest/miniconda.html).

 * Create a virtual environment containing snakemake, as suggested [here](https://snakemake.readthedocs.io/en/stable/getting_started/installation.html). First install mamba as a replacement of the default conda solver:
```bash
conda install -c conda-forge mamba
```

 * Then, install snakemake:
```bash
mamba env create --name snakemake --file environment.yaml
```

 * Activate the enviroment:
```bash
conda activate snakemake
```

 * Run snakemake in dry-run mode to check if everything is fine. **YOUR_WORKING_DIR** could follow the format: **YYYY-MM-DD**.
```bash
snakemake --cores 32 --use-conda --configfile conf/config.yaml --printshellcmds -d YOUR_WORKING_DIR --rerun-incomplete --keep-going --dryrun
```

 * For verbose output:
```bash
snakemake --cores 32 --use-conda --configfile conf/config.yaml --printshellcmds -d YOUR_WORKING_DIR --rerun-incomplete --keep-going --verbose --reason --dryrun
```

 * If you are happy with the --dryrun, run snakemake:
```bash
snakemake --cores 32 --use-conda --configfile conf/config.yaml --printshellcmds -d YOUR_WORKING_DIR --rerun-incomplete --keep-going
```

**Tip:** For large projects, we suggest to run snakemake in a [screen](https://linux.die.net/man/1/screen) session.

