# Cognitive models and Bayesian data analysis models in WebPPL

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

- `syllogisms-bda.wppl`: Data analysis model for inferring model parameters given cognitive models and syllogistic reasoning data
- `syllogisms-ais.wppl`: Data analysis model for computing marginal likelihood of data using Annealed Importance Sampling
