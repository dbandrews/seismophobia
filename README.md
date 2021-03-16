---
title: "Project Proposal"
author: "Group 11 - Junghoo Kim, Trevor Kinsey, Dustin Burnham, Dustin Andrews"
date: "11/19/2020"
output: html_document
---

## About

The damage that earthquakes cause can leave people without food, water, and shelter. Being prepared for an earthquake before it happens can make living through the immediate aftermath less traumatic (Paton, Mcclure, and Buergelt (2006)). Having insurance that covers the damage caused by earthquakes may reduce the uncertainty and fear that the threat of earthquakes creates. People who are afraid of earthquakes represent a group of potential clients for companies selling earthquake preparedness products and insurance. It has been demonstrated that people who are more concerned about earthquakes are more likely to have taken preparatory measures, such as owning a preparedness kit (Dooley et al. 1992).

We aim to predict groups in the population that are afraid of earthquakes and thus are target demographics for advertising. If a machine learning algorithm can identify these groups it enables companies to build a marketing strategy based on this information.

We'll be working with the San Andreas Earthquake data set from [`fivethirtyeight`](https://github.com/fivethirtyeight/data/tree/master/san-andreas) which collected people's relative fear of earthquakes along with other demographic attributes such as age, gender, household income and region.

We aim to determine a model for predicting a person's fear of earthquakes, given demographic features about that person. We will investigate binary classifiers - random forest and logistic regression - that can predict if a person has fear about earthquakes (seismophobia) given their demographic attributes.

## Report

The final report can be found [here](https://htmlpreview.github.io/?https://github.com/UBC-MDS/seismophobia/blob/main/doc/seismophobia_report.html). 

## Environment Setup

We suggest either of the following 2 methods to reproduce our analysis:

### 1. Using Docker

After (1) cloning the Github repo - to use the Docker image and run the analysis, first (2) install Docker Desktop. 

Then, (3) navigate to the root of the directory where you cloned this repository.

Expected total time to clean and rerun the entire analysis is approximately 5-10 minutes (This may vary depending on device/stability of internet connection).

(4) To clean out intermediate files and rerun the entire analysis run:
```bash
$ bash clean_and_run_analysis_docker.sh
```
This will download the data to the `data` folder, process the data and save to `data/processed`, create the EDA visuals to `visuals/`, build the classifiers and write out a final report of the process in the `doc` folder.

Final document is found at: `doc/seismophobia_report.html`.

This shell script is just a wrapper around `docker run` commands to use `make` to clean out the files and re run the analysis pipeline. To do each one separately you can do:

```
$ docker run --rm -e PASSWORD="test" -v "/$(pwd)":/home/seismophobia/ dbandrews/seismophobia:v0.4.0 make directory=/home/seismophobia clean
```

Then re run the analysis using:
```
$ docker run --rm -e PASSWORD="test" -v "/$(pwd)":/home/seismophobia/ dbandrews/seismophobia:v0.4.0 make directory=/home/seismophobia all
```
### 2. Using Make, Conda & R

Ensure that you have installed GNU Make and it's on your PATH variable.

Clone this GitHub repository, and install the required conda dependencies by configuring a conda environment for this repo. From the root of the repo run:

```
$ conda env create -f seismophobia_conda_env.yml
```

For the R scripts install:

R Version: 4.0.3

R Packages:

ggthemes_4.2.0 
testthat_2.3.2  
here_1.0.0      
docopt_0.7.1    
forcats_0.5.0   
stringr_1.4.0   
dplyr_1.0.2     
purrr_0.3.4    
readr_1.4.0     
tidyr_1.1.2     
tibble_3.0.4    
ggplot2_3.3.0   
tidyverse_1.3.0

Then, you can re run the analysis from the root of the repo using:

```
$ conda activate seismophobia
$ make clean
$ make all
```

## License

UBC-MDS/seismophobia is licensed under the MIT License. If re-using/re-mixing, please provide attribution and link to this webpage. 

More information regarding license can be found [here](https://github.com/UBC-MDS/seismophobia/blob/main/LICENSE).

# References

Bureau, US Census. 2018. “Income and Poverty in the United States: 2015.” The United States Census Bureau. https://www.census.gov/library/publications/2016/demo/p60-256.html.

———. 2019. “State Population Totals: 2010-2019.” The United States Census Bureau. https://www.census.gov/data/tables/time-series/demo/popest/2010s-state-total.html.

Dooley, David, Ralph Catalano, Shiraz Mishra, and Seth Serxner. 1992. “Earthquake Preparedness: Predictors in a Community Survey1.” Journal of Applied Social Psychology 22 (6): 451–70. https://doi.org/https://doi.org/10.1111/j.1559-1816.1992.tb00984.x.

Lundberg, Scott M, and Su-In Lee. 2017. “A Unified Approach to Interpreting Model Predictions.” In Advances in Neural Information Processing Systems 30, edited by I. Guyon, U. V. Luxburg, S. Bengio, H. Wallach, R. Fergus, S. Vishwanathan, and R. Garnett, 4765–74. Curran Associates, Inc. http://papers.nips.cc/paper/7062-a-unified-approach-to-interpreting-model-predictions.pdf.

Paton, D, J Mcclure, and Petra Buergelt. 2006. “Natural Hazard Resilience: The Role of Individual and Household Preparedness.” In Disaster Resilience an Integrated Approach, edited by Douglas Paton and David Johnston, 105–27. Charles C Thomas Publisher, Ltd.

Pedregosa, F., G. Varoquaux, A. Gramfort, V. Michel, B. Thirion, O. Grisel, M. Blondel, et al. 2011. “Scikit-Learn: Machine Learning in Python.” Journal of Machine Learning Research 12: 2825–30.

R Core Team. 2019. R: A Language and Environment for Statistical Computing. Vienna, Austria: R Foundation for Statistical Computing. https://www.R-project.org/.

team, The pandas development. 2020. Pandas-Dev/Pandas: Pandas (version latest). Zenodo. https://doi.org/10.5281/zenodo.3509134.

Van Rossum, Guido, and Fred L Drake Jr. 1995. Python Tutorial. Centrum voor Wiskunde en Informatica Amsterdam, The Netherlands.

Wickham, Hadley. 2017. Tidyverse: Easily Install and Load the ’Tidyverse’. https://CRAN.R-project.org/package=tidyverse.

Xie, Yihui. 2014. “Knitr: A Comprehensive Tool for Reproducible Research in R.” In Implementing Reproducible Computational Research, edited by Victoria Stodden, Friedrich Leisch, and Roger D. Peng. Chapman; Hall/CRC. http://www.crcpress.com/product/isbn/9781466561595.
