
# Spatially-explicit hierarchical modelling for applied population and community ecology

### 24-27 June 2024, Swiss Ornithological Institute, Sempach, Switzerland

### [Jeffrey W. Doser](https://www.jeffdoser.com/) and [Marc Kéry](https://www.mbr-pwrc.usgs.gov/pubanalysis/roylebook/)

### Teaching Assistant: [Gesa von Hirschheydt](https://www.wsl.ch/en/staff/vonhirsc/)

### [Workshop Schedule and Overview](https://doserjef.github.io/Switzerland24-Spatial-Workshop/)

### [spOccupancy website](https://www.jeffdoser.com/files/spoccupancy-web/) and [spAbundance website](https://www.jeffdoser.com/files/spabundance-web/)

------------------------------------------------------------------------

## Software installation

To participate in the exercises, you will need to have R installed. You
will need to have at least R v3.5.0, but it would be better to have a
more recent version installed ($\geq 4.2.0$). We will use RStudio for
most of the demonstrations, but this is not a requirement.

The focus of this course is on using the R packages `spOccupancy` and
`spAbundance` to fit a variety of different spatial models for answering
applied questions in population and community ecology. These packages
can be installed from CRAN by running
`install.packages(c("spOccupancy", "spAbundance"))`.

In the exercises, we will use a variety of other R packages for
exploratory data analysis, visualizations, and summarizing the results
from our models. You will need to install these packages to fully
participate in the exercises. The code below can be run in R to only
install those packages that don’t currently exist on your system.

``` r
required.packages <- c('MCMCvis', 'ggplot2', 'stars', 'pals', 'patchwork', 'MBA', 
                       'geoR', 'corrplot', 'dplyr', 'tidyr', 'coda', 'abind', 'unmarked')
new.packages <- required.packages[!(required.packages %in% installed.packages()[, 'Package'])]
if (length(new.packages) > 0) {
  install.packages(new.packages)
}
```

## Repository Directory

This repository includes all code, exercises, and associated lectures
covered in the workshop.

### [code](./code)

Contains the R scripts (and associated files) for all exercises
throughout the workshop. The number at the beginning of the file names
of the scripts is the same number for the corresponding lecture material
that is available in the [lectures](./lectures) directory.

- `00a-intro-hm.R`: code for introduction to hierarchical models in
  ecology.
- `00b-trend-example-simNpC2.R`: an example of how ignoring detection
  probability can lead to bias in trend estimates.
- `01-swiss-european-goldfinch.R`: fits a single-species occupancy model
  using data on the European goldfinch from the Switzerland Breeding
  Bird Survey (Swiss MHB) in 2014. This script also serves as our
  introduction to `spOccupancy`.
- `02-spatial-linear-model-wef.R`: an introductory script to fitting
  spatial models and looking at associated geostatistical techniques. To
  introduce spatial statistics concepts, we will use a data set
  consisting of a survey of trees in a 10ha forest stand in Oregon, USA,
  with the goal of predicting diameter at breast height DBH) across the
  stand. The script also serves as our introduction to `spAbundance`.
- `03a-gp-sim-example.R`: this script fits a spatial occupancy model
  using a full Gaussian Process with a simulated data set for direct
  comparison with a spatial occupancy model that uses an NNGP. Note we
  will not run this script during the workshop (since it takes over 7
  hours to run!), but rather it is used to showcase an example discussed
  in the lecture.
- `03b-nngp-sim-example.R`: this script fits a spatial occupancy model
  using a Nearest Neighbor Gaussian Process with a simulated data set
  for direct comparison with a spatial occupancy model that uses a full
  GP. Similar to `03a-gp-sim-example.R`, we will not run this script
  during the workshop, but it is availailable to see how an example
  discussed in lecture is generated.
- `03c-summary-sim-example.R`: script to summarize the simulation
  results from `03a-gp-sim-example.R` and `03b-gp-sim-example.R` and
  generate a plot to compare the NNGP model results to the full GP model
  results.
- `04a-spatial-european-goldfinch-ex.R`: this script builds on
  `01-swiss-european-goldfinch.R` by extending our occupancy model to a
  spatial occupancy model that is used to predict the distribution of
  the European goldfinch across Switzerland.
- `04b-spOccupancy-ubms-rock-buntings.R`: A script providing a detailed
  work through of fitting spatial occupancy models in `spOccupancy` to
  predict the distribution of rock buntings in Ticino.
- `05-occupancy-model-survey-design-simulation.R`: this script shows how
  to assess the number of sites/visits in single-season occupancy model
  analyses using simulated data.
- `06-amphibian-multi-species-occ.R`: this script showcases how to fit
  multi-species occupancy models in spOccupancy. Here we focus on a
  community of tropical amphibians and how their occupancy relates to
  agriculture and topography. These data come from Ribeiro Jr. et
  al. (2018) *Ecological Applications*. We fit a standard multi-species
  occupancy model as well as a multi-species occupancy model that
  accounts for residual correlations between species in a joint species
  distribution modelling framework.
- `07-plant-spatial-multi-species-occ.R`: this script shows how to fit a
  multi-species spatial factor occupancy model to a simulated data set
  of 10 plant species. The objective here is to explore the contribution
  of elevation as a niche partitioning mechanism.
- `08-bat-multi-season-occ.R`: this script fits multiple multi-season
  occupancy models to estimate the distribution of the spotted bat
  across Oregon and Washington, USA. These data were collected as part
  of the North American Bat Monitoring Program (NABAT) and were part of
  the lovely analysis in Wright et al. (2021) *Ecology and Evolution*.
- `09-wood-thrush-spatial-trend-occ.R`: this script fits a multi-season
  spatially-varying occupancy model to estimate a spatially varying
  trend in occupancy probability of the wood thrush across the eastern
  US from 2000-2009. The data used here are a subset of data from the
  North American Breeding Bird Survey.
- `10a-spatial-glmm-northern-cardinal.R`: script to fit a variety of
  spatial and nonspatial GLMMs to estimate relative abundance of the
  Northern Cardinal in North Carolina, USA. These data come from the
  North American Breeding Bird Survey.
- `10b-spatial-multi-species-glmm.R`: this script fits a multi-species
  spatial GLMM to estimate relative abundance of 88 bird species across
  the state of North Carolina, USA in 2019. We will not run this script
  during the workshop, but it is just provided as an example
  multi-species GLMM. Using predictions of abundance across the state
  for each species, we showcase how to generate a map of Shannon’s
  diversity across the state as a derived quantity from the
  multi-species Bayesian model. These data come from the North American
  Breeding Bird Survey.
- `11a-crimson-mantled-woodpecker-nmix.R`: script to fit a
  single-species N-mixture model to estimate how abundance of the
  crimson-mantled woodpecker varies across an elevation gradient in the
  Andes mountain in western Bolivia. These data are part of a very nice
  study by Montaño‐Centellas et al. (2021) that looks at drivers of
  avian community assembly across a tropical elevation gradient.
- `11b-sim-spatial-nmix.R`: script to fit a single-species spatial
  N-mixture model to predict the abundance of a simulated species across
  a simulated landscape.
- `11c-european-goldfinch-spatial-nmix.R`: in the previous exercise, we
  used simulated data to show how to fit spatial N-mixture models, and
  saw that everything went very smoothly. Here we will work with a real
  data set (the same European Goldfinch data we worked with in our
  occupancy modelling section but now using the raw counts). We will see
  how spatial (and non-spatial) N-mixture models can be difficult to
  estimate in practice.
- `11d-nmix-demo.R`: demo from Marc that gives an example of fitting an
  N-mixture model with some simulated data on vipers using both
  `unmarked` and `spAbundance`.
- `12a-get-inits.R`: script to fit a multi-species spatial N-mixture
  model with data from the Hubbard Brook Experimental Forest. Here our
  goal is to predict abundance of four species across the forest. In
  this script, we will fit an initial multi-species spatial N-mixture
  model for 1 chain and a fairly small number of iterations to extract
  starting values for use in a larger model run.
- `12b-hbef-main-sfMsNMix.R`: script to fit multi-species spatial
  N-mixture models with data from the Hubbard Brook Experimental Forest.
  This script is used to run models with initial values that were
  obtained from a shorter model fit in `12a-get-inits.R`. This script
  also shows one way (which I use very often) to run multiple MCMC
  chains in parallel using `spAbundance`/`spOccupancy`. In particular,
  we will see how to run three separate instances of this R script
  simultaneously by running the scripts through the command line. We can
  access the command line via the “Terminal” window of RStudio or some
  other terminal interface.
- `12c-compile`: simple text file that we will use to run multiple
  chains of `12b-hbef-main-sfMsNMix.R` in parallel.
- `12d-combine-chains.R`: this script combines the three chains that are
  run in parallel into a single `spAbundance` model object, such that
  the object can subsequently be used with all `spAbundance` model
  functions. This is not necessary to do when running chains separately,
  but it can be helpful to make working wiith the objects a bit simpler.
- `12e-summary-hbef-sfMsNMix.R`: script to summarize the results from
  the spatial multi-species N-mixture model with four species in the
  Hubbard Brook Experimental Forest. There isn’t much done in this
  script, it is more so just to show the workflow for fitting models
  with multiple chains in this way.
- `13-spatial-hds-issj.R`: script to fit single-species spatial and
  non-spatial hierarchical distance sampling models to estimate the
  density of the island scrub jay.
- `14-multi-species-hds-harv-forest.R`: script to compare the three
  types of multi-species HDS models in `spAbundance` to estimate density
  of 20 bird species across 90 point count locations in Harvard Forest
  in 2022. Harvard Forest is a long term ecological research center in
  the northeastern USA.

### [lectures](./lectures)

Contains the lectures used throughout the workshop. The number at the
beginning of the file names of the scripts is the same number for the
corresponding lecture material that is available in the
[lectures](./lectures) directory.

- `00-intro-to-hms.pdf`: a broad introduction to hierarchical modelling
  and its use in population and community ecology.
- `01-occupancy.pdf`: introduction to occupancy modelling, the
  `spOccupancy` package, and a very short introduction to Bayesian
  Markov chain Monte Carlo (MCMC) methods.
- `02-intro-to-spatial-models.pdf`: introduction to spatial modelling
  and classical geostatistics concepts.
- `03-big-spatial.pdf`: discussion of the computational challenges that
  big spatial data present, approaches to mitigate the effects, and
  details on the Nearest Neighbor Gaussian Process (NNGP) approach used
  in `spOccupancy` and `spAbundance` to make such models more efficient.
- `04a-spatial-occupancy-models.pdf`: lecture on merging the spatial
  techniques discussed in `02-intro-to-spatial-models.pdf` and the
  occupancy modelling approaches in `01-occupancy.pdf` to form spatial
  occupancy models.
- `04b-spOccupancy-ubms-rock-buntings.pdf`: associated documentation for
  the modelling of the rock bunting across southeastern Switzerland.
- `05-occupancy-model-survey-design.pdf`: lecture discussing survey
  design for single-species occupancy models.
- `06-multi-species-occupancy.pdf`: lecture on non-spatial multi-species
  occupancy models, including latent factor multi-species occupancy
  models (i.e., joint species distribution models that account for
  imperfect detection).
- `07-spatial-multi-species-occupancy.pdf`: lecture on spatial
  multi-species occupancy models, with a particular focus on the use of
  spatial factor multi-species occupancy models.
- `08-multi-season-occupancy-models.pdf`: an introduction to
  multi-season occupancy models to assess occupancy patterns over space
  and/or time. This includes discussion of both non-spatial and spatial
  multi-season occupancy models in `spOccupancy`.
- `09-svc-occupancy-models.pdf`: a brief introduction to
  spatially-varying coefficient occupancy models, which can be used to
  estimate spatially-varying trends or spatial variation in
  species-environment relationships.
- `10-spatial-glmms.pdf`: lecture on the use of spatial generalized
  linear mixed models for relative abundance estimation and prediction
  using `spAbundance`.
- `11-spatial-nmix.pdf`: lecture discussing spatial N-mixture models for
  abundance estimation. This lecture also includes a brief discussion of
  posterior predictive checks and WAIC. We also focus pretty intensely
  on the difficulties that spatial N-mixture models can present in
  practice.
- `12-spatial-multi-species-nmix.R`: a brief lecture discussing the
  three multi-species N-mixture model types (regular, latent factor,
  spatial factor) that can currently be fit in `spAbundance`.
- `13-hierarchical-distance-sampling.pdf`: lecture providing a brief
  overview of hierarchical distance sampling for abundance/density
  estimation, including both nonspatial and spatial forms.
- `14-multi-species-HDS.pdf`: a brief lecture discussing the three
  multi-species HDS model types (regular, latent factor, spatial factor)
  that can currently be fit in `spAbundance`.

### [data](./data)

Contains data sets that are used in the exercises.

### [results](./results)

Directory including some results that we will save when running models
for the spatial multi-species N-mixture models.

### [literature](./literature)

Literature for the software, methods, and concepts we discuss throughout
the workshop.

#### `spOccupancy` and `spAbundance` core references

- `doser-2022-spOccupancy-MEE.pdf`: introduces the `spOccupancy` package
  and single-species, multi-species, and integrated spatial occupancy
  models.
- `doser-2023-jsdm-Ecology.pdf`: develops the spatial factor
  multi-species occupancy models included in `spOccupancy`.
- `doser-2024-svc-models-JABES.pdf`: introduces the spatially-varying
  coefficient occupancy models included in `spOccupancy`.
- `doser-2024-spAbundance-MEE.pdf`: introduces the `spAbundance` package
  including functionality for single-species and multi-species spatial
  GLMMs, N-mixture models, and hierarchical distance sampling models.

#### Occupancy models

- `mackenzie-2002-occupancy-Ecology.pdf`: original paper introducing
  occupancy models.
- `tyre-2002-occupancy-EcoApps.pdf`: paper that simultaneously developed
  the occupancy modeling concept.
- `northrup-2018-occupancy-priors-PlosONE.pdf`: paper that discusses
  priors for regression coefficients in occupancy models (with
  applications to any other sort of logistic regression model).
- `gelfand-2005-multi-species-modeling-ApplStat.pdf`: one of two papers
  that simultaneously develops the concepts used in multi-species
  occupancy models.
- `dorazio-2005-msom-JASA.pdf`: the second of two papers that
  simultaneously developed the concepts used in multi-species occupancy
  models to share information across species.
- `zipkin-2020-msom-example-Science.pdf`: application of a multi-species
  occupancy model and how it can generate estimates for species with
  very detections to answer important ecological questions.
- `pacifici-2014-community-model-guidelines-EcoEvo.pdf`: presents
  guidelines for how to form “communities” for fitting multi-species
  occupancy models.
- `erickson-2023-modelling-rare-species-ECOG.pdf`: discusses different
  approaches for modelling rare species (including the “borrowing
  strength” concept used in multi-species occupancy models) and
  discusses what situations certain approaches are better than others.
- `ribeiro-jr-2018-amphibian-EcoApps.pdf`: an application of an MSOM and
  also the source of the amphibian data we use in our multi-species
  occupancy modelling examples.
- `steenweg-2018-occ-trend-interpretation-Ecology.pdf`: a discussion of
  how to interpret trends in a multi-season occupancy model analysis.
- `von-hirschheydt-2023-mixed-occupancy-BAE.pdf`: discusses “mixed”
  occupancy designs and how to assess the number of visits needed for
  reliable estimation of occupancy parameters.
- `doser-2024-identifiability-MEE.pdf`: discusses identifiability of
  single-visit multi-season occupancy models under different
  combinations of spatial and temporal autocorrelation.

#### Joint species distribution models

- `warton-2015-jsdm-TREE.pdf`: a broad overview discussing applications
  of JSDMs. Includes a lot of foundational references for this modelling
  approach.
- `poggiato-2021-JSDM-interpretation-TREE.pdf`: discusses the problems
  associated with interpreting residual covariance matrices in JSDMs as
  true biological interactions and how the relevance of this
  interpretation is highly dependent on scale.
- `tobler-2019-JSDM-MSOM-Ecology.pdf`: paper that provides the first
  combination of multi-species occupancy modelling concepts with joint
  species distribution modelling concepts into a single framework.

#### Spatial modeling

- `zhang-2004-spatial-identifiability-JASA.pdf`: paper that discusses
  identifiability considerations for spatial covariance parameters in
  spatially-explicit models.
- `hodges-2010-spatial-confounding-AmStat.pdf`: paper that introduces
  the concept of spatial confounding and a proposed solution.
- `zimmerman-2021-spatial-confounding-JASA.pdf`: more recent paper that
  challenges existing “solutions” to spatial confounding and provide
  recommendations on what to do if spatial confounding occurs.
- `makinen-2022-spatial-confounding-ECOG.pdf`: a paper that explicitly
  discusses spatial confounding in the context of species distribution
  models and provides many good, practical recommendations for how/when
  to deal with it.
- `heaton-2019-big-spatial-JABES.pdf`: a very nice introduction to the
  many possible options of dealing with “big” spatial data. Provides an
  overview of many different methods, and a “friendly competition” where
  experts in the different methods used their approach with a test data
  set, and the different approaches were compared in terms of their
  accuracy and computational intensity.
- `datta-2016-NNGP-JASA.pdf`: paper that introduces the Nearest Neighbor
  Gaussian Process (NNGP) that we use in `spOccupancy` and `spAbundance`
  for computationally efficient spatial models.
- `finley-2019-NNGP-algorithms-JCGS.pdf`: paper that introduces the
  underlying computational algorithms used to efficiently code MCMC
  algorithms for NNGP models.
- `wright-2021-bat-multi-sesaon-occ-EcoEvo.pdf`: a spatio-temporal
  occupancy model that provides a bit more flexibility than those
  currently included in `spOccupancy`. Also the source of the bat data
  used in the bat multi-season occupancy examples.
- `pease-2022-svc-occupancy-Ecosphere.pdf`: paper that develops a
  spatially-varying occupancy model and applies it to four wildlife
  species in North Carolina, USA.

#### Modelling abundance and/or relative abundance

- `callaghan-2024-modelling-abundance-TREE.pdf`: paper describing pros
  and cons of modelling relative abundance vs. true abundance.
- `royle-2004-nmix-Biometrics.pdf`: paper introducing the N-mixture
  model for abundance estimation.
- `knape-2018-nmix-sensitivity-MEE.pdf`: paper discussing some of the
  identifiability/sensitivity considerations of N-mixture models.
- `kery-2018-nmix-identifiability.pdf`: presents a large-scale
  assessment of N-mixture model identifiability using Swiss bird data.
- `goldstein-2022-nmix-vs-glmm-SciRep.pdf`: compares GLMMs and N-mixture
  models for relative abundance estimation using eBird data.
- `yamaura-2012-multi-species-nmix-BioCon.pdf`: paper introducing the
  multi-species N-mixture model.
- `royle-2004-hds-Ecology.pdf`: paper introducing the hierarchical
  distance sampling model.
- `sollman-2015-multi-species-HDS-MEE.pdf`: paper introducing the
  multi-species hierarchical distance sampling model.

### Workshop feedback

Please fill out the survey at the following link. We would really
appreciate your feedback to help improve future courses!

Workshop feedback survey:
<https://docs.google.com/forms/d/e/1FAIpQLSdeRfOVX2O6wxGs5e5uxMl1o2JlEm0ja4iCURuLD-E8FW9XSQ/viewform?usp=sf_link>.

## Acknowledgements

Some of the material covered in the lectures on classical geostatistics
and modelling big spatial data was adapted from workshop material
developed by [Andy Finley](https://www.finley-lab.com/). Some of the
material covered in the multi-species occupancy modelling lecture was
adapted from teaching material developed by [Elise
Zipkin](https://zipkinlab.org/).
