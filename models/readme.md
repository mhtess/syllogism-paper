# Cognitive models and Bayesian data analysis models in WebPPL

All models were written in the probabilistic programming language WebPPL. For information, see [webppl.org](http://webppl.org/). Cognitive models were run from R using the [`rwebppl package`](https://github.com/mhtess/rwebppl). Bayesian data analysis were run via the command line on a computing cluster, using Slurm/sbatch to run multiple models and replicant chains in parallel.

## Cognitive models

Wrapper scripts intended to be run from R using the [`rwebppl package`](https://github.com/mhtess/rwebppl). Scripts can be modified to run from the command line. Cognitive models are found in `node_modules/vennUtils_oneShot/src/` and accessed as a [WebPPL package](https://webppl.readthedocs.io/en/master).

### Rational Speech Act models: Generate (posterior) distribution on Conclusions given syllogism
- File: `syllogisms-r.wppl`
- Description: Run RSA model(s) for different syllogisms. File runs a loop over syllogisms and different RSA models.

### Literal interpretation: Generate (posterior) distribution on States given syllogism (Fig. 5)
- File: `syllogisms-literalListener-r.wppl`
- Description: Literal interpretation model to produce distribution on states given syllogism (Fig. 5 in paper)
- Code to run from R found in `diagrams.Rmd`

## Bayesian Data Analysis models

These models are intended to be run for long MCMC chains, taking on the order 12 - 72 hours on a CPU depending on the number of iterations. These models were run on a computing cluster using an [`sbatch`](https://slurm.schedmd.com/sbatch.html) script.

In addition to the internal WebPPL package `vennUtils` (found in `node_modules`), these scripts require two external WebPPL packages:
- [`webppl-csv`](https://github.com/mhtess/webppl-csv): Read and write CSV files
- [`webppl-sample-writer`](https://github.com/mhtess/webppl-sample-writer): To stream posterior samples to file

The scripts to run the data analysis models are:
- `syllogisms-bda.wppl`: Data analysis model for inferring model parameters given cognitive models and syllogistic reasoning data
- `syllogisms-ais.wppl`: Data analysis model for computing marginal likelihood of data using Annealed Importance Sampling


# WebPPL packages containing different RSA models and helper scripts

The RSA model variants are written in individual files grouped together as a WebPPL package.
There is one package for running models as one-off demos `vennUtils_oneShot`. There is another package for running the BDA models, which run the RSA models for many iterations: (`vennUtils`).
Both packages can be found inside `node_modules/`
To learn more about WebPPL packages, [read the docs](https://webppl.readthedocs.io/en/master/packages.html)

The `src/` folder inside of the package folder inside of `node_modules` contains RSA models and helper scripts.

## RSA Models

The `src/` folder contains 9 versions of the RSA model published in the paper. The three `M0` models are the ones reported in the main text (Literal Speaker, State Communication, Belief Alignment). The `M1` and `M2` models include a pragmatic interpretation component, where the premises of the syllogisms are interpreted pragmatically as coming from a rational speaker. The `M1` models define the speaker utility with respect to the state (Venn diagram). The `M2` models define the speaker utility with respect to a QUD, which is assumed to include the regions of the state that refer to the A and C properties (the conclusion of the syllogism). The `M2` models are discussed in the Appendix of the paper.


- `M00_LIT_LIT`: *Literal Speaker* -- Literal interpretation, literal production
- `M01_LIT_PRAG_BELIEF`: *Belief Alignment* -- Literal interpretation, pragmatic production (KL utility)
- `M02_LIT_PRAG_STATE`: *State Communication* -- Literal interpretation, pragmatic production (state surprisal utility)
- `M10_PRAG_STATE_LIT`: Pragmatic interpretation (state), literal production
- `M11_PRAG_STATE_PRAG_BELIEF`: Pragmatic interpretation (state), pragmatic production (KL utility)
- `M12_PRAG_STATE_PRAG_STATE`: Pragmatic interpretation (state), pragmatic production (state surprisal utility)
- `M20_PRAG_QUD_LIT`: Pragmatic interpretation (QUD), literal production
- `M21_PRAG_QUD_PRAG_BELIEF`: Pragmatic interpretation (QUD), pragmatic production (KL utility)
- `M22_PRAG_QUD_PRAG_STATE`: Pragmatic interpretation (QUD), pragmatic production (state surprisal utility)

The `M0_LIT.wppl` contains only the literal interpretation component of the model, which produces a distribution on states given a syllogism (Fig. 5 in paper).

## Other files

- `data.wppl`: Process the data file from Ragni et al. found in `analysis/ccobra_data/ragni2016.csv`
- `utils.wppl`: Helper functions
