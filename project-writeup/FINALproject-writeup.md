CAMFAM: An Analysis of Suicide Rates
================
May 1st, 2019

## Section 1. Introduction

With suicide being one of the leading causes of death for teens in the
world, it is important to not only see how Northern America (Canada,
Greenland, and the United States) stack up with the rest of the world
but also the key trends of suicide rates among different groups and what
factors shed light onto these different rates\[1\] We want to explore
how economic status, along with variables such as age, sex, and human
development index, affects suicide rates all across the world. Our
hypothesis is that generally, in poorer countries we predict that
suicide rates will lower.

Our response variable will be suicides/100k pop, which is the number of
suicides per 100,000 people in a certain country and year, which is
stored as a numeric in our dataset. Our predictors variables will be
age, sex, HDI, gdp\_for\_year, gdp\_per\_capita, generation, region and
continent. Age is the age an individual was when they passed, sex is the
gender of that individual, country is the country they are from, year is
the year they passed, HDI for year is the human development index for a
given country and year, gdp\_for\_year is the GDP for a given country
and year, gdp\_per\_capita is the GDP per capita for a given country and
year, and generation is the generation that an individual belongs to. We
wish to understand how the number of suicides per 100,000 people in a
certain country and year changes as year, GDP, GDP per capita, and HDI
increase or decreases, meaning we want to understand the population
coefficients for year, gdp\_for\_year, gdp\_per\_capita, and HDI for
year. Additionally, we want to understand whether age, sex, generation,
and country have an effect on the number of suicides per 100,000 people,
meaning we also want to understand the population coefficients for these
variables. We will not include country and suicide/no in our analysis
because having 188 different levels is unrealistic for the former and
the latter is manifested in the response variable and population.

### EDA

Given the longitudinal structure of our data and the need for making a
multilevel model, we are going to use the data collected in 2010. This
year has a majority of the countries in the origianl data set and also
is the year HDI values were collected. Since region and continent were
not in this data set orginially, we used the gapminder data set as the
cold deck and merged those values into the suicide data set.

Since South Korea and Russia did not have HDI values, we found them from
online and imputed those (had values of .884 and .780 respectively).
However, Aruba and Puerto Rico’s HDI’s were not available, so we took
the average of the HDI in the Caribbean and used a mean imputation for
those values.

For the response variable, since there are a few negative infinity
values, we added one to each number of suicides, divided by population
(to turn into suicided/100k) and then log transformed. We log
transformed because of the original skewed histogram (Figure 1).

    ## Loading required package: cowplot

    ## 
    ## Attaching package: 'cowplot'

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     ggsave

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](FINALproject-writeup_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

The mean number of suicides per 100,000 people is 11.22, while the
maximum number of suicides per 100,000 people in this dataset is 182.32.
The distribution of this reponse variable is normal. We see that most of
our countries are from the Amerias and Europe and are in the regions of
Western Asia, Southern Europe, South America, Northern Europe, and the
Caribbean. In general, each continent has a similar average number of
suicides, with Europe having much more outliers with fewer suicides than
the others.

![](FINALproject-writeup_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

As age increases, suicide rate tends to increase in general. The 5-14
age group is far lower than the other age groups, which is expected. The
average number of suicides/100k for each region is around 7.38. We see
Southern Africa as a key outlier with far less suicides and Eastern
Africa with far more suicides than the average. We notice that males
have a higher suicide rate/100k people than females. However, there are
many outliers in this data set so we must explore further. We notice
that Generation Z is significantly lower in terms of the average number
of suicides/100k of 7.38.

Due to the skewed histograms of GDP, GDP per capita, and population, we
log transformed them (Figures 2,3,4). We also mean center all the
quantitative
    variables.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.
    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](FINALproject-writeup_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

The HDI does not have a set distribution. Rather, it is quite sparse.
The distribution of population is skewed left and has a unimodal
distribution. We notice that the distribution of GDPs of countries has a
near-bimodal distribution. The GDP Per Capita is skewed to the left and
is bimodal.

![](FINALproject-writeup_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

We do not see correlations between HDI, GDP, and GDP per capita and
suicides/100k. We notice that as population has a specific cutoff.

\#\#Section 2. Regression Analysis

###
