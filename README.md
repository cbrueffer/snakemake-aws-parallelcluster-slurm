[![Snakemake](https://img.shields.io/badge/snakemake-≥7.0.0-brightgreen.svg)](https://snakemake.github.io)

# Snakemake Profile for Running on AWS ParallelCluster with the Slurm Scheduler

This is a [Snakemake](https://snakemake.github.io/) profile for running on [AWS ParallelCluster](https://docs.aws.amazon.com/parallelcluster) with the [Slurm](https://slurm.schedmd.com/documentation.html) scheduler.
It is heavily based on [John Blischak's smk-simple-slurm profile](https://github.com/jdblischak/smk-simple-slurm) and as such this repository uses the same license.

Default ParallelCluster Slurm installations have two peculiarities that make them differ from most other Slurm installations:
- The `--mem` argument to `sbatch` is not supported, and if used sends nodes into the `DRAINED` state.
- The `sacct` accounting system is not installed by default.

This profile accomodates these peculiarities.


## Usage

Given a workflow `my-workflow`, copy the `aws-parallelcluster-slurm` directory to `my-workflow/profiles`.
Make sure the `status-scontrol.sh` script is executable, and in `config.yaml`change the parameter `partition`
in section `default-resources` to the name of a queue in your cluster.

From `my-workflow`, execute Snakemake as `snakemake --profile profiles/aws-parallelcluster-slurm`.
