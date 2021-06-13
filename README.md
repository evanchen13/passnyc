# Data Science for Good with PASSNYC

Each year, thousands of eighth and ninth grade students in New York City take the Specialized High Schools Admissions Test (SHSAT) in hopes of getting into one of the city's eight specialized high schools. These institutions are considered to be prestigious and can have potentially tremendous impacts on students' lives, but the only way to gain admission is to take the SHSAT.

Recently, the demographics at the specialized high schools have become increasingly homogeneous, so the mission of PASSNYC is to identify schools with underrepresented demographics and, through consultation and outreach, increase the amount of students from these schools that take the SHSAT. Ultimately, if more diverse students take the exam, then more of them will also be admitted.

As PASSNYC states in its competition on [Kaggle](https://www.kaggle.com/passnyc/data-science-for-good), the organization would like more assistance in identifying schools where its services would be most useful. Therefore, I have performed some wrangling and exploration on data provided by both PASSNYC and other public sources, as well as constructed a model to learn more about what features are important in identifying schools with low participation in the SHSAT. I have also evaluated how useful this model is by looking at the actual vs. predicted values and the distribution of residuals. This has allowed me to see how well the model actually fits the existing data and, consequently, how much I can trust the feature importance provided by the model.

# Requirements

- Jupyter Notebook
- Numpy
- Pandas
- re
- Matplotlib
- Seaborn
- Scipy
- Datetime
- Sklearn
- Warnings

# Files

- [passnyc.ipynb](https://github.com/evanchen13/passnyc/blob/main/passnyc.ipynb) - Jupyter Notebook containing all the code for this analysis
- [2016 School Explorer.csv](https://github.com/evanchen13/passnyc/blob/main/2016%20School%20Explorer.csv) - school data provided by PASSNYC
- [2017-2018 SHSAT Admissions Test Offers By Sending School.csv](https://github.com/evanchen13/passnyc/blob/main/2017-2018%20SHSAT%20Admissions%20Test%20Offers%20By%20Sending%20School.csv) - data on SHSAT offers
- [2017-doe-high-school-directory.csv](https://github.com/evanchen13/passnyc/blob/main/2017-doe-high-school-directory.csv) - school data provided by the Department of Education
- [results](https://github.com/evanchen13/passnyc/tree/main/results)
  - [actual-predicted.png](https://github.com/evanchen13/passnyc/blob/main/results/actual-predicted.png) - plots actuals from the target variable vs. the final model's predicted values
  - [feature-importance.png](https://github.com/evanchen13/passnyc/blob/main/results/feature-importance.png) - visualization of the top 20 most important features
  - [residuals-vs-predicted.png](https://github.com/evanchen13/passnyc/blob/main/results/residuals-vs-predicted.png) - plots residuals against final model's predicted values
  - [residuals.png](https://github.com/evanchen13/passnyc/blob/main/results/residuals.png) - histogram of residuals
- [base.yaml](https://github.com/evanchen13/passnyc/blob/main/base.yaml) - contains the environment used in this project

To get the Jupyter Notebook running, execute the following in the command line and select `passnyc.ipynb` from the Jupyter Notebook dashboard. The conda environment setup is optional.

```
$ git clone https://github.com/evanchen13/passnyc.git
$ cd passnyc
$ conda env create -f base.yaml
$ jupyter notebook
```

# Results

I found that a RandomForestRegressor specifically tuned with a maximum depth of 10 was the optimal model for the data, with the best GridSearchCV R-squared score being 0.48. In terms of feature importances, here is what I found.

![Feature Importances](/results/feature-importance.png)

The three most important features that stand out are the proportion of students who receive 4s on seventh and sixth grade math exams, as well as the percentage of Black and Hispanic students. Other than these factors, it looks like standardized test performance in the sixth to eighth grades, as well as average ELA and math proficiency, are important factors in determining whether a high proportion of students will take the SHSAT.

However, I did not want to fully accept the model without making sure that it actually fit the data. Therefore, I decided to create other visualizations to examine the performance of the model. First, I plotted the actual vs. predicted values.

![Actual vs. Predicted](/results/actual-predicted.png)

The red line represents a perfect model, one in which the actual values are equal to the predicted values. Based on that, it looks like the model represents the data pretty well. There are some data points that do not fit as well, for example the point with an actual value of about 0.6 and predicted value of about 0.4, but this is also an outlier that is more difficult to predict.

I also wanted to plot the distribution of the residuals. If the model fits the data well, the residuals would look more like a normal distribution rather than being right-skewed or left-skewed. In other words, the predicted values would not be consistently larger or consistently smaller, but rather more random in the error.

![Residuals](/results/residuals.png)

The distribution here is centered around zero and appears to be more normally distributed rather than being right-skewed or left-skewed. There is one outlier residual, which is related to the outlier mentioned previously, but otherwise the distribution matches what I would expect.

Finally, I also wanted to plot the residuals against the predicted values.

![Residuals vs. Predicted](/results/residuals-vs-predicted.png)

It appears that as the predicted value increases, the absolute values of the residuals also increase. While an optimal model would have roughly equal residuals no matter the magnitude of the predicted values, I was fine with the model as it is, especially with the small amount of data. Perhaps if there were more data points, the residuals would respect homoscedasticity more.

A detailed summary of this analysis and resulting insights can also be found [here](https://evanchen13.medium.com/using-data-science-to-increase-diversity-at-new-york-city-high-schools-6611a21ec26c).

# Acknowledgements

Special thanks to PASSNYC and the Kaggle community for providing the data and necessary background information to complete this project.

# License

The contents of this repository are covered under the [GNU General Public License v3.0](https://github.com/evanchen13/passnyc/blob/main/LICENSE).
