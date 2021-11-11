# Cognitive models and Bayesian data analysis models in WebPPL

All models were written in the probabilistic programming language WebPPL. For information, see [webppl.org](http://webppl.org/). Cognitive models were run from R using the [`rwebppl package`](https://github.com/mhtess/rwebppl). Bayesian data analysis were run via the command line on a computing cluster, using Slurm/sbatch to run multiple models and replicant chains in parallel.

## Cognitive models

Wrapper scripts intended to be run from R using the [`rwebppl package`](https://github.com/mhtess/rwebppl). Scripts can be modified to run from the command line. Cognitive models are found in `node_modules/vennUtils_oneShot/src/` and accessed as a [WebPPL package](https://webppl.readthedocs.io/en/master).

### Rational Speech Act models: Generate (posterior) distribution on Conclusions given syllogism
- File: `syllogisms-r.wppl`
- Description: Run RSA models for different syllogisms. File runs a loop over syllogisms, and different RSA models.

### Literal interpretation: Generate (posterior) distribution on States given syllogism (Fig. 5)
- File: `syllogisms-literalListener-r.wppl`
- Description: Literal interpretation model to produce distribution on states given syllogism (Fig. 5 in paper)
- Code to run from R found in `diagrams.Rmd`

## Bayesian Data Analysis models

These models are intended to be run for long MCMC chains, taking on the order 12 - 72 hours on a CPU. These models were run a cluster using an [`sbatch`](https://slurm.schedmd.com/sbatch.html) script.

In addition to the internal WebPPL package `vennUtils` (found in `node_modules`), these scripts require two external WebPPL packages:
- [`webppl-csv`](https://github.com/mhtess/webppl-csv): Read and write CSV files
- [`webppl-sample-writer`](https://github.com/mhtess/webppl-sample-writer): To stream posterior samples to file

- `syllogisms-bda.wppl`: Data analysis model for inferring model parameters given cognitive models and syllogistic reasoning data
- `syllogisms-ais.wppl`: Data analysis model for computing marginal likelihood of data using Annealed Importance Sampling
