Seismophobia Report
================
Trevor Kinsey, Dustin Andrews, Dustin Burnham, Junghoo Kim
2020/11/26

  - [Summary](#summary)
  - [Introduction](#introduction)
  - [Methods](#methods)
  - [Data](#data)
  - [Analysis](#analysis)
  - [Results](#results)
  - [References](#references)

## Summary

We use a random forest classifier and logistic regression model to
predict a person’s fear of earthquakes based on their demographic
information. Both models were able to predict subjects’ fear of
earthquakes only slightly better than a dummy classifier. This indicates
that there is potential for predictions based on demographics. However,
our data set was small and included only four demographic features,
which limited the models’ predictive ability to slightly better than
random guessing. More data that contains more demographic information
could lead to better prediction results.

## Introduction

The damage that earthquakes cause can leave people without food, water,
and shelter. Being prepared for an earthquake before it happens can make
living through the immediate aftermath less traumatic (Paton, Mcclure,
and Buergelt (2006)). Having insurance that covers the damage caused by
earthquakes may reduce the uncertainty and fear that the threat of
earthquakes creates. People who are afraid of earthquakes represent a
group of potential clients for companies selling earthquake preparedness
products and insurance. It has been demonstrated that people who are
more concerned about earthquakes are more likely to have taken
preparatory measures, such as owning a preparedness kit (Dooley et al.
1992).

We aim to predict whether a US resident is afraid of earthquakes and to
identify which demographic features contribute to the prediction. This
information could be used to identify target demographics for
advertising. This would enable earthquake-related companies to build a
marketing strategy based on this information to reach potential
customers and increase revenue.

## Methods

## Data

The data for this analysis was downloaded from
<https://github.com/fivethirtyeight/data/tree/master/san-andreas>. It is
based on a survey conducted by
[fivethirtyeight.com](https://fivethirtyeight.com/) in May 2015, of 1014
respondents in the US.

The data set contains

  - demographic information (age, gender, household income, region of
    residence in the United States),

  - responses to survey questions relating to knowledge of and
    experience with earthquakes,

  - self-reported level of fear of earthquakes.

The responses to the survey questions would likely have been very
predictive of fear of earthquakes, but advertisers would not have access
to this information conducting a similar survey of their own. This would
likely be very expensive so we limited our analysis to the demographic
information, which is publicly available through US census data.

Some preliminary examination of the data shows some relation between the
demographic features and earthquake fear.

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/feature_distributions.png" alt="Fig 1: Distribution of demographic information among survey respondents" width="80%" />

<p class="caption">

Fig 1: Distribution of demographic information among survey respondents

</p>

</div>

The survey respondents were fairly evenly split across ages categories
and genders. The household income distribution was not uniform, but is
likely a reflection of the US population’s income distribution, that had
a median value of $55,775 in 2015 (Bureau 2018). The distribution across
US regions was not uniform, possibly due to the fact that the list of
regions is divided into geographic regions that don’t necessarily have
the same populations. For example, the Pacific region (Washington,
Oregon, and California) has a population of 50.1 million compared to New
England (Connecticut, Massachusetts, Maine, New Hampshire, Rhode Island,
and Vermont) has a combined population of 14.7 million (Bureau 2019).

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/feature_distributions_across_response.png" alt="Fig 2: The level of earthquake fear across demograhic features" width="100%" />

<p class="caption">

Fig 2: The level of earthquake fear across demograhic features

</p>

</div>

Younger people tend to report being afraid more often than older people,
while women report being afraid more often than men. The geographic
region with the highest level of fear is the Pacific. Overall there were
more people who were not afraid of earthquakes than were afraid.

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/target_distribution.png" alt="Fig 3: The distribution of earthquake fear among respondents" width="75%" />

<p class="caption">

Fig 3: The distribution of earthquake fear among respondents

</p>

</div>

## Analysis

We used a random forest classifier and a logistic regression for the
classification task. In addition to binary classification for
prediction, random forest classifier and logistic regression give a
measure of importance for each feature. The prediction target is the
self-reported fear of earthquakes, which we converted from an ordinal
variable to a binary variable called `target`. The class `target` = 0
includes the levels *“not at all worried”* and *“not so worried”*, while
`target` = 1 includes *“somewhat worried”*, *“very worried”*, and
*“extremely worried”*. We computed SHAP values to investigate feature
importance after some preliminary exploration of global feature
importance.

## Results

Our models were a random forest classifier and a logistic regression
which we compared to a dummy classifier that assigned a class randomly
based on the target distribution. The models correctly predicted more
positive outcomes and had fewer false positives than the dummy
classifier .They also correctly predicted more negative outcomes than
the dummy classifier.

This means the models could identify who was afraid of earthquakes
better than picking at random, and who was not afraid of earthquakes
better than picking at random. Incorrect predictions were lower than
when picking at random.

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/confusion_matrix_RandomForestClassifier.png" alt="Fig 4: Confusion matrix for each model used" width="50%" height="50%" /><img src="/home/seismophobia/visuals/confusion_matrix_LogisticRegression.png" alt="Fig 4: Confusion matrix for each model used" width="50%" height="50%" /><img src="/home/seismophobia/visuals/confusion_matrix_DummyClassifier.png" alt="Fig 4: Confusion matrix for each model used" width="50%" height="50%" />

<p class="caption">

Fig 4: Confusion matrix for each model used

</p>

</div>

To capture the combined effects of precision and recall we scored our
models’ predictions using the F1 score. Both the random forest and
logistic regression models had higher F1 scores than the dummy
classifier.

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/classifier_results_table.png" alt="Fig 5: Classifier F1 scores" width="60%" height="60%" />

<p class="caption">

Fig 5: Classifier F1 scores

</p>

</div>

Of the models positive predictions, a greater proportion were correct
than the dummy classifier’s, as characterized by our models’ higher *ROC
AUC* scores. The models predicted better than guessing at random, but
not a by lot.

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/roc_auc_curve_RandomForestClassifier.png" alt="Fig 6: ROC curves for various models" width="50%" height="50%" /><img src="/home/seismophobia/visuals/roc_auc_curve_LogisticRegression.png" alt="Fig 6: ROC curves for various models" width="50%" height="50%" /><img src="/home/seismophobia/visuals/roc_auc_curve_DummyClassifier.png" alt="Fig 6: ROC curves for various models" width="50%" height="50%" />

<p class="caption">

Fig 6: ROC curves for various models

</p>

</div>

We computed SHAP values to see the degree to which each feature
contributed to a positive prediction. The feature for both that was most
important in both models for being afraid of earthquakes was living in
the Pacific region. This is not surprising since that region experiences
more earthquakes than any other region.

Both models predicted that living in the East North Central region was
predictive of lower levels of fear. These results indicate that
geographic region plays a big role in predicted fear levels.

<div class="figure" style="text-align: center">

<img src="/home/seismophobia/visuals/shap_summary_plot_RandomForestClassifier.png" alt="Fig 7: SHAP plot for random forest and logistic regression classifiers" width="50%" height="50%" /><img src="/home/seismophobia/visuals/shap_summary_plot_LogisticRegression.png" alt="Fig 7: SHAP plot for random forest and logistic regression classifiers" width="50%" height="50%" />

<p class="caption">

Fig 7: SHAP plot for random forest and logistic regression classifiers

</p>

</div>

The next feature that both models identified as predictive of a positive
fear response was age, with younger people showing more fear than older
people. Looking at the two variables for gender, our model predicts
women are more likely to be afraid of earthquakes than men.

With the data that we have, our models were not effective in identifying
people who are afraid of earthquakes with a high degree of certainty.
However, because our data set had only four features, we believe there
is potential for improved predictions if we had a more comprehensive
data set. This would require collecting more information in the form of
a larger survey.

The R (R Core Team 2019) and Python (Van Rossum and Drake Jr 1995)
programming languages and the following Python packages were used for
this project: pandas (team 2020), sklearn (Pedregosa et al. 2011),
shap(Lundberg and Lee 2017), tidyverse (Wickham 2017), and knitr (Xie
2014). The code used to perform the analysis and create this report can
be found at: <https://github.com/UBC-MDS/seismophobia>

## References

<div id="refs" class="references">

<div id="ref-bureau_2018">

Bureau, US Census. 2018. “Income and Poverty in the United States:
2015.” *The United States Census Bureau*.
<https://www.census.gov/library/publications/2016/demo/p60-256.html>.

</div>

<div id="ref-bureau_2019">

———. 2019. “State Population Totals: 2010-2019.” *The United States
Census Bureau*.
<https://www.census.gov/data/tables/time-series/demo/popest/2010s-state-total.html>.

</div>

<div id="ref-doi.org/10.1111/j.1559-1816.1992.tb00984.x">

Dooley, David, Ralph Catalano, Shiraz Mishra, and Seth Serxner. 1992.
“Earthquake Preparedness: Predictors in a Community Survey1.” *Journal
of Applied Social Psychology* 22 (6): 451–70.
<https://doi.org/https://doi.org/10.1111/j.1559-1816.1992.tb00984.x>.

</div>

<div id="ref-NIPS2017_7062">

Lundberg, Scott M, and Su-In Lee. 2017. “A Unified Approach to
Interpreting Model Predictions.” In *Advances in Neural Information
Processing Systems 30*, edited by I. Guyon, U. V. Luxburg, S. Bengio, H.
Wallach, R. Fergus, S. Vishwanathan, and R. Garnett, 4765–74. Curran
Associates, Inc.
<http://papers.nips.cc/paper/7062-a-unified-approach-to-interpreting-model-predictions.pdf>.

</div>

<div id="ref-72124acf2fa84e8aad36e68d0dc4c5e6">

Paton, D, J Mcclure, and Petra Buergelt. 2006. “Natural Hazard
Resilience: The Role of Individual and Household Preparedness.” In
*Disaster Resilience an Integrated Approach*, edited by Douglas Paton
and David Johnston, 105–27. Charles C Thomas Publisher, Ltd.

</div>

<div id="ref-scikit-learn">

Pedregosa, F., G. Varoquaux, A. Gramfort, V. Michel, B. Thirion, O.
Grisel, M. Blondel, et al. 2011. “Scikit-Learn: Machine Learning in
Python.” *Journal of Machine Learning Research* 12: 2825–30.

</div>

<div id="ref-R">

R Core Team. 2019. *R: A Language and Environment for Statistical
Computing*. Vienna, Austria: R Foundation for Statistical Computing.
<https://www.R-project.org/>.

</div>

<div id="ref-reback2020pandas">

team, The pandas development. 2020. *Pandas-Dev/Pandas: Pandas* (version
latest). Zenodo. <https://doi.org/10.5281/zenodo.3509134>.

</div>

<div id="ref-van1995python">

Van Rossum, Guido, and Fred L Drake Jr. 1995. *Python Tutorial*. Centrum
voor Wiskunde en Informatica Amsterdam, The Netherlands.

</div>

<div id="ref-tidyverse">

Wickham, Hadley. 2017. *Tidyverse: Easily Install and Load the
’Tidyverse’*. <https://CRAN.R-project.org/package=tidyverse>.

</div>

<div id="ref-knitr">

Xie, Yihui. 2014. “Knitr: A Comprehensive Tool for Reproducible Research
in R.” In *Implementing Reproducible Computational Research*, edited by
Victoria Stodden, Friedrich Leisch, and Roger D. Peng. Chapman;
Hall/CRC. <http://www.crcpress.com/product/isbn/9781466561595>.

</div>

</div>
