Stat210 Final Project
================
CamFam
May 1st, 2019

    ## ── Attaching packages ─────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
    ## ✔ tibble  2.0.0     ✔ dplyr   0.7.8
    ## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
    ## ✔ readr   1.3.1     ✔ forcats 0.3.0

    ## ── Conflicts ────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

    ## 
    ## Attaching package: 'skimr'

    ## The following object is masked from 'package:knitr':
    ## 
    ##     kable

    ## 
    ## Attaching package: 'modelr'

    ## The following object is masked from 'package:broom':
    ## 
    ##     bootstrap

    ## The following object is masked from 'package:dslabs':
    ## 
    ##     heights

    ## -------------------------------------------------------------------------

    ## You have loaded plyr after dplyr - this is likely to cause problems.
    ## If you need functions from both plyr and dplyr, please load plyr first, then dplyr:
    ## library(plyr); library(dplyr)

    ## -------------------------------------------------------------------------

    ## 
    ## Attaching package: 'plyr'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     arrange, count, desc, failwith, id, mutate, rename, summarise,
    ##     summarize

    ## The following object is masked from 'package:purrr':
    ## 
    ##     compact

    ## Loading required package: Hmisc

    ## Loading required package: lattice

    ## Loading required package: survival

    ## Loading required package: Formula

    ## 
    ## Attaching package: 'Hmisc'

    ## The following objects are masked from 'package:plyr':
    ## 
    ##     is.discrete, summarize

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     src, summarize

    ## The following objects are masked from 'package:base':
    ## 
    ##     format.pval, units

    ## Loading required package: SparseM

    ## 
    ## Attaching package: 'SparseM'

    ## The following object is masked from 'package:base':
    ## 
    ##     backsolve

    ## Parsed with column specification:
    ## cols(
    ##   country = col_character(),
    ##   year = col_double(),
    ##   sex = col_character(),
    ##   age = col_character(),
    ##   suicides_no = col_double(),
    ##   population = col_double(),
    ##   `suicides/100k pop` = col_double(),
    ##   `country-year` = col_character(),
    ##   `HDI for year` = col_double(),
    ##   `gdp_for_year ($)` = col_number(),
    ##   `gdp_per_capita ($)` = col_double(),
    ##   generation = col_character()
    ## )

## Section 1. Introduction

With suicide being one of the leading causes of death for teens in
America, we thought it would be interesting to see how the U.S. stacks
up against other countries all over the world in terms of the number of
suicides that occur, as well as what factors may contribute to the
significant number of suicides in the U.S. and other countries.\[1\] We
want to explore how economic status, along with variables such as age,
sex, and human development index, affects suicide rates all across the
world. Our hypothesis is that generally, in poorer countries we predict
that suicide rates will lower.

Our response variable will be suicides/100k pop, which is the number of
suicides per 100,000 people in a certain country and year, which is
stored as a numeric in our dataset. Our predictors variables will be
age, sex, country, year, HDI, gdp\_for\_year, gdp\_per\_capita,
generation, region and continent. Age is the age an individual was when
they passed, sex is the gender of that individual, country is the
country they are from, year is the year they passed, HDI for year is the
human development index for a given country and year, gdp\_for\_year is
the GDP for a given country and year, gdp\_per\_capita is the GDP per
capita for a given country and year, and generation is the generation
that an individual belongs to. We wish to understand how the number of
suicides per 100,000 people in a certain country and year changes as
year, GDP, GDP per capita, and HDI increase or decreases, meaning we
want to understand the population coefficients for year, gdp\_for\_year,
gdp\_per\_capita, and HDI for year. Additionally, we want to understand
whether age, sex, generation, and country have an effect on the number
of suicides per 100,000 people, meaning we also want to understand the
population coefficients for these variables.

The variables relevant to the analysis of our research question are
stated above: suicides/100k pop, age, sex, country, year, HDI for year,
gdp\_for\_year, gdp\_per\_capita, and generation. Additionally,
suicides\_no (which is the number of suicides for individuals who are of
a certain age group and sex and who passed in a certain country and
year) and population, (which is the total number of individuals who are
of a certain age group and sex and who live in a certain country in a
certain year), since these are used to calculate suicides/100k pop.

We will now perform exploratory data analysis on the variables that we
plan to use in our model.

Given the longitudinal structure of our data and the need for making a
multilevel model, we are going to use the data collected in 2010 as that
year has a majority of the countries in the origianl data set and also
is the year HDI values were collected.

    ## Skim summary statistics
    ##  n obs: 1056 
    ##  n variables: 12 
    ## 
    ## ── Variable type:character ─────────────────────────────────────────
    ##      variable missing complete    n min max empty n_unique
    ##           age       0     1056 1056   9  11     0        6
    ##       country       0     1056 1056   4  28     0       88
    ##  country-year       0     1056 1056   8  32     0       88
    ##    generation       0     1056 1056   6  12     0        4
    ##           sex       0     1056 1056   4   6     0        2
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────
    ##            variable missing complete    n          mean            sd
    ##    gdp_for_year ($)       0     1056 1056       5.9e+11       1.8e+12
    ##  gdp_per_capita ($)       0     1056 1056   23857.19      22474.17   
    ##        HDI for year      48     1008 1056       0.79          0.086  
    ##          population       0     1056 1056 1891380.05    4052946.65   
    ##         suicides_no       0     1056 1056     226.04        805.51   
    ##   suicides/100k pop       0     1056 1056      11.22         16.94   
    ##                year       0     1056 1056    2010             0      
    ##          p0       p25          p50           p75         p100     hist
    ##     6.8e+08  2e+10         9.4e+10       3.8e+11      1.5e+13 ▇▁▁▁▁▁▁▁
    ##   991         7008.5   13817.5       36326       111328       ▇▂▂▂▁▁▁▁
    ##     0.61         0.73      0.8           0.88         0.94    ▃▃▆▇▆▆▇▇
    ##  1015       107517.75 453842.5     1548637.25         4.3e+07 ▇▁▁▁▁▁▁▁
    ##     0            2        22           107.5      11767       ▇▁▁▁▁▁▁▁
    ##     0            0.8       4.81         14.37       182.32    ▇▁▁▁▁▁▁▁
    ##  2010         2010      2010          2010         2010       ▁▁▁▇▁▁▁▁

We first need to turn our character variables into factors.

The countries that do not have HDI calculated for them are Aruba, Puerto
Rico, Korea, and Russia. Online, we can find the HDI from 2010 of South
Korea and Russia, which are .884 and .780 respectively. We will do these
after we add regions to our data set.

Later on in this EDA, we will want to do a boxplot of the countries;
however, that will be indiscernable based on the number of countries.
Instead, we should group countries into regions and their continents.

We will use the gapminder dataset for countries and regions. We will
extract the country, continent, and region from gapMinder, change the
names of differing countries, and then merge.

Online, we can find the HDI from 2010 of South Korea and Russia, which
are .884 and .780 respectively. Since the HDI’s of Puerto Rico and Aruba
are not publicly available, those we will find use the average HDI from
the Caribbean to impute.

    ##                       region      mean
    ## 1  Australia and New Zealand 0.9160000
    ## 2                  Caribbean 0.7511250
    ## 3            Central America 0.6928571
    ## 4               Central Asia 0.6802500
    ## 5             Eastern Africa 0.7495000
    ## 6               Eastern Asia 0.8840000
    ## 7             Eastern Europe 0.8020000
    ## 8           Northern America 0.9060000
    ## 9            Northern Europe 0.8809000
    ## 10             South America 0.7293333
    ## 11        South-Eastern Asia 0.7556667
    ## 12           Southern Africa 0.6430000
    ## 13             Southern Asia 0.6830000
    ## 14           Southern Europe 0.8231111
    ## 15              Western Asia 0.8020000
    ## 16            Western Europe 0.8954286

To see the shape of the distribution of the number of suicides per
100,000 people, we can plot a histogram of the suicides/100k pop
variable.

    ## Skim summary statistics
    ##  n obs: 1056 
    ##  n variables: 14 
    ## 
    ## ── Variable type:character ─────────────────────────────────────────
    ##      variable missing complete    n min max empty n_unique
    ##  country-year       0     1056 1056   8  32     0       88
    ## 
    ## ── Variable type:factor ────────────────────────────────────────────
    ##    variable missing complete    n n_unique
    ##         age       0     1056 1056        6
    ##   continent       0     1056 1056        5
    ##     country       0     1056 1056       88
    ##  generation       0     1056 1056        4
    ##      region       0     1056 1056       16
    ##         sex       0     1056 1056        2
    ##                              top_counts ordered
    ##  15-: 176, 25-: 176, 35-: 176, 5-1: 176   FALSE
    ##   Eur: 420, Ame: 336, Asi: 240, Afr: 36   FALSE
    ##      Alb: 12, Arg: 12, Arm: 12, Aru: 12   FALSE
    ##  Gen: 352, Sil: 352, Gen: 176, Mil: 176   FALSE
    ##  Car: 120, Nor: 120, Wes: 120, Eas: 108   FALSE
    ##               fem: 528, mal: 528, NA: 0   FALSE
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────
    ##            variable missing complete    n          mean            sd
    ##    gdp_for_year ($)       0     1056 1056       5.9e+11       1.8e+12
    ##  gdp_per_capita ($)       0     1056 1056   23857.19      22474.17   
    ##                 HDI       0     1056 1056       0.79          0.085  
    ##          population       0     1056 1056 1891380.05    4052946.65   
    ##         suicides_no       0     1056 1056     226.04        805.51   
    ##   suicides/100k pop       0     1056 1056      11.22         16.94   
    ##                year       0     1056 1056    2010             0      
    ##          p0       p25          p50           p75         p100     hist
    ##     6.8e+08  2e+10         9.4e+10       3.8e+11      1.5e+13 ▇▁▁▁▁▁▁▁
    ##   991         7008.5   13817.5       36326       111328       ▇▂▂▂▁▁▁▁
    ##     0.61         0.73      0.79          0.88         0.94    ▂▃▆▇▆▆▇▆
    ##  1015       107517.75 453842.5     1548637.25         4.3e+07 ▇▁▁▁▁▁▁▁
    ##     0            2        22           107.5      11767       ▇▁▁▁▁▁▁▁
    ##     0            0.8       4.81         14.37       182.32    ▇▁▁▁▁▁▁▁
    ##  2010         2010      2010          2010         2010       ▁▁▁▇▁▁▁▁

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

    ## 
    ## Skim summary statistics
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────
    ##                          variable missing complete    n  mean    sd p0 p25
    ##  suicideFinal$`suicides/100k pop`       0     1056 1056 11.22 16.94  0 0.8
    ##   p50   p75   p100     hist
    ##  4.81 14.37 182.32 ▇▁▁▁▁▁▁▁

Based on this histogram, we can see that it is not normally distributed
and is extremely right skewed. In fact, from skimming this variable, we
can see that the mean number of suicides per 100,000 people is only
11.22, while the maximum number of suicides per 100,000 people in this
dataset is 182.32. Thus, there is at least one extreme outlier in the
response variable, indicating that we should perform a log
transformation on the response variable.

Since this response variable has negative infinity values (this stems
from the fact that some countries have 0 suicides), we will first
increase the suicide number by 1 for each country and then recalculate
suicides per
    100k.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

From log transforming suicides/100k pop, we can already see that the
extreme outliers have disappeared, and the histogram seems to be
approximately normally distributed.

Note: suicides/100k pop is now log transformed for all plots below.

We will now look at an overview of the relationships that suicides/100k
pop has with each of the quantitative predictor variables (age, sex,
country, year, HDI, gdp\_for\_year, gdp\_per\_capita, and generation),
as well as the relationships these variables have with each other.

![](project-writeup_files/figure-gfm/unnamed-chunk-12-1.png)<!-- --> In
our data set, all ages have the same number of counts.
![](project-writeup_files/figure-gfm/unnamed-chunk-13-1.png)<!-- --> In
our data set, male and female have the same count

![](project-writeup_files/figure-gfm/unnamed-chunk-14-1.png)<!-- --> In
our data set, we see that most of the countries are from the Americas
and Europe.

![](project-writeup_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->
From this bar graph, we notice that most of our data set seems high in
regions from Western Asia, Southern Europe, South America, Northern
Europe, and the Caribbean.

![](project-writeup_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

By examining these boxplots, we can tell that as age increases, suicide
rate tends to increase in general.

![](project-writeup_files/figure-gfm/unnamed-chunk-17-1.png)<!-- --> In
general, each continent has a similar average number of suicides, with
Europe having much more outliers with fewer suicides than the others.

![](project-writeup_files/figure-gfm/unnamed-chunk-18-1.png)<!-- --> The
average number of suicides/100k for each region is around 2. We see
Souther Africa as a key outlier with far less suicides and Eastern
Africa with far more suicides than the average.

![](project-writeup_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

From this boxplot, we notice that males have a higher suicide rate/100k
people than females. However, there are many outliers in this data set
so we must explore further.

![](project-writeup_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

From this boxplot, we see that the average suicide rate/100k people is
varied among generation. More specifically, we notice that Generation Z
and Millienials have lower rates than the average value of around
    2.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-21-1.png)<!-- --> We
will have to log transform population. In addition, we will mean center
it so it is easier to
    interpret.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-22-1.png)<!-- --> We
see that this plot has is skewed left and has a unimodal distribution.

We will mean center HDI so it makes it easier to
    interpret.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-23-1.png)<!-- --> The
HDI does not have a set distribution. Rather, it is quite
    parse.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->
Because this is skewed greatly, a log transformation of gdp is needed.
We will also mean center this
    variable.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

Log transforming the data set, we notice that the distribution of GDPs
of countries has a near-bimodal
    distribution.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->
Like GDP, we will need to log transform this data set. We will also mean
center
    this.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

Like the GDP of the country, the GDP Per Capita has a non-normal
distribution. Rather, it is skewed to the left and is bimodal. Since
these variables are so similar, there could be mulitcollinearity between
the two.

![](project-writeup_files/figure-gfm/unnamed-chunk-28-1.png)<!-- --> We
do not see a correlation between HDI and Suicides/100k.
![](project-writeup_files/figure-gfm/unnamed-chunk-29-1.png)<!-- --> We
do not see a correlation between GDP and Suicides/100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-30-1.png)<!-- --> We
do not see a correlation between GDP per capita and Suicides/100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

From the pairs plot, it looks as if HDI, and gdp\_for\_year do not have
a clear linear relationship with suicides/100k pop. However,
gdp\_per\_capita seems to be positively correlated with suicides/100k
pop, meaning as gdp\_per\_capita increases, so does suicides/100k pop.
Additionally, it looks as if HDI and gdp\_per\_capita seem to have a
strong non-linear relationship, indicating that we should continue
looking into this relationship and perhaps include an interaction term
between these two variables. Similarly, HDI and gdp\_for\_year also seem
to have a strong non-linear relationship, so we should include an
interaction term between these two variables as well. We also see a
strong evidence of multicollinearity between GDP for year and GDP per
capita that we must address in the model.

We are very concerned about multicollinearity, so we will look into VIF.

We plan to do a multiple linear regression because suicides/100k pop is
a quantitative variable (there are no levels to it, since it is a
continuous variable).

## Section 3. Data

We are not going to include country in this model as there are over 188
countries and we can already account for much of this variability based
off of region and continent.

    ## Start:  AIC=-436.98
    ## `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## 
    ## 
    ## Step:  AIC=-436.98
    ## `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + continent + region
    ## 
    ## 
    ## Step:  AIC=-436.98
    ## `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region
    ## 
    ##                        Df Sum of Sq     RSS     AIC
    ## - `gdp_per_capita ($)`  1      0.13  664.73 -438.78
    ## <none>                               664.61 -436.98
    ## - HDI                   1      1.56  666.16 -436.51
    ## - `gdp_for_year ($)`    1      2.85  667.46 -434.46
    ## - population            1      4.97  669.58 -431.11
    ## - region               15    241.88  906.49 -139.21
    ## - sex                   1    290.42  955.02  -56.14
    ## - age                   5    769.95 1434.55  365.52
    ## 
    ## Step:  AIC=-438.78
    ## `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     region
    ## 
    ##                      Df Sum of Sq     RSS     AIC
    ## <none>                             664.73 -438.78
    ## - `gdp_for_year ($)`  1      3.65  668.38 -435.00
    ## - HDI                 1      4.50  669.23 -433.66
    ## - population          1     10.81  675.55 -423.74
    ## - region             15    252.00  916.73 -129.35
    ## - sex                 1    290.37  955.10  -58.05
    ## - age                 5    773.61 1438.34  366.31

    ## 
    ## Call:
    ## lm(formula = `suicides/100k pop` ~ sex + age + population + HDI + 
    ##     `gdp_for_year ($)` + region, data = suicideFinal)
    ## 
    ## Coefficients:
    ##              (Intercept)                   sexmale  
    ##                  6.30811                   1.04969  
    ##           age25-34 years            age35-54 years  
    ##                  0.17820                   0.40214  
    ##            age5-14 years            age55-74 years  
    ##                 -1.89731                   0.43725  
    ##             age75+ years                population  
    ##                  0.71362                  -1.87232  
    ##                      HDI        `gdp_for_year ($)`  
    ##                  1.97528                  -0.09485  
    ##          regionCaribbean     regionCentral America  
    ##                 -0.58669                  -0.59740  
    ##       regionCentral Asia      regionEastern Africa  
    ##                  0.01450                  -0.24973  
    ##       regionEastern Asia      regionEastern Europe  
    ##                  1.21047                   0.32738  
    ##   regionNorthern America     regionNorthern Europe  
    ##                  0.48474                  -0.08409  
    ##      regionSouth America  regionSouth-Eastern Asia  
    ##                  0.12288                  -0.38981  
    ##    regionSouthern Africa       regionSouthern Asia  
    ##                 -1.66591                  -0.95802  
    ##    regionSouthern Europe        regionWestern Asia  
    ##                 -0.47693                  -1.24475  
    ##     regionWestern Europe  
    ##                  0.12148

We chose a multiple linear regression model because we want to predict
the value of a variable based on multile different independent
variables. Based on backward selection, we found that sex, age
population, HDI, gdp for year, and gdp per capita, and region are
relevant predictors, whereas population, continent, and generation are
not.

# Testing of Interesting Interactions

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * age
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1025 623.14  5    41.469 13.643 6.514e-13 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 15.229 and the p-value is 1.862e-14, which is small.
We can can conclude that the interaction effect of age and sex is a
significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * population
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)    
    ## 1   1030 664.61                                 
    ## 2   1029 652.98  1    11.627 18.322 2.04e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.1534 and the p-value is 0.1426-16, which is high.
We can can conclude that the interaction effect of sex and population is
not a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * HDI
    ##   Res.Df    RSS Df Sum of Sq      F Pr(>F)
    ## 1   1030 664.61                           
    ## 2   1029 664.37  1   0.23833 0.3691 0.5436

The F statistic is .3308 and the p-value is 0.5653, which is high. We
can can conclude that the interaction effect of sex and HDI is not a
significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * `gdp_for_year ($)`
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1029 656.74  1    7.8615 12.318 0.0004681 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 13.261 and the p-value is 0.0002844, which is very
small. We can can conclude that the interaction effect of sex and
gdp\_for\_year ($) is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * `gdp_per_capita ($)`
    ##   Res.Df    RSS Df Sum of Sq      F Pr(>F)
    ## 1   1030 664.61                           
    ## 2   1029 663.91  1   0.69674 1.0799  0.299

The F statistic is .87421 and the p-value is 0.2373, which is high. We
can can conclude that the interaction effect of sex and gdp per capita
is not a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * region
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)   
    ## 1   1030 664.61                                
    ## 2   1015 641.88 15    22.727 2.3959 0.002057 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.675 and the p-value is 0.0005204, which is low We
can can conclude that the interaction effect of sex and region is a
significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + age * population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1025 585.23  5    79.378 27.805 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 3.2618 and the p-value is 0.006284 , which is small
We can can conclude that the interaction effect of age and population is
a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + age * HDI
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1025 601.46  5    63.145 21.522 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 12.609 and the p-value is 6.638e-12, which is smaller
than 0.05. We can can conclude that the interaction effect of age and
HDI is significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + age * `gdp_for_year ($)`
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1025 572.42  5    92.182 33.013 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 27.473 and the p-value is 2.2e-16, which is smaller
than 0.05. We can can conclude that the interaction effect of age and
gdp for year is significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + age * `gdp_per_capita ($)`
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1025 636.76  5    27.845 8.9644 2.389e-08 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 5.4293 and the p-value is 6.15e-05, which is smaller
than 0.05. We can can conclude that the interaction effect of
suicides\_no and population is significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + age * region
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2    955 499.60 75       165 4.2055 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 5.4293 and the p-value is 6.15e-05, which is smaller
than 0.05. We can can conclude that the interaction effect of
suicides\_no and population is significant predictor.

So, we can conclude that to not include the interaction effect between
sex and population. Our updated model will
be:

|                        term                        |   estimate    |  std.error  |  statistic  |  p.value  |
| :------------------------------------------------: | :-----------: | :---------: | :---------: | :-------: |
|                    (Intercept)                     |  28.6306936   | 49.2932512  |  0.5808238  | 0.5618866 |
|                  countryArgentina                  |  33.2930072   | 54.1108791  |  0.6152738  | 0.5389381 |
|                   countryArmenia                   | \-49.2850155  | 51.4091810  | \-0.9586812 | 0.3386530 |
|                    countryAruba                    | \-25.7494310  | 47.4341411  | \-0.5428459 | 0.5877234 |
|                  countryAustralia                  |  12.6005875   | 62.7542498  |  0.2007926  | 0.8410253 |
|                   countryAustria                   | \-29.1254959  | 51.0209773  | \-0.5708534 | 0.5686159 |
|                   countryBahamas                   | \-13.9401405  | 47.4588604  | \-0.2937310 | 0.7692091 |
|                   countryBahrain                   |  \-5.8027127  | 52.1003730  | \-0.1113756 | 0.9114086 |
|                  countryBarbados                   | \-24.5341033  | 48.0956343  | \-0.5101108 | 0.6104275 |
|                   countryBelarus                   | \-34.4834113  | 47.2216478  | \-0.7302458 | 0.4659292 |
|                   countryBelgium                   | \-21.5548943  | 53.1080707  | \-0.4058685 | 0.6851892 |
|                   countryBelize                    | \-59.6280330  | 82.8382587  | \-0.7198127 | 0.4723181 |
|                   countryBrazil                    |  35.6255377   | 72.6408075  |  0.4904342  | 0.6242603 |
|                  countryBulgaria                   | \-49.2030109  | 52.2152813  | \-0.9423106 | 0.3469507 |
|                   countryCanada                    |  25.6201516   | 61.5756786  |  0.4160758  | 0.6777143 |
|                    countryChile                    |  67.1483628   | 53.1270016  |  1.2639216  | 0.2074449 |
|                  countryColombia                   |  183.7631877  | 63.3655556  |  2.9000486  | 0.0040658 |
|                 countryCosta Rica                  |  32.8295551   | 64.1299536  |  0.5119223  | 0.6091609 |
|                   countryCroatia                   | \-21.8498466  | 48.5037581  | \-0.4504774 | 0.6527598 |
|                    countryCuba                     |   4.4476358   | 71.5626807  |  0.0621502  | 0.9504933 |
|                   countryCyprus                    |  27.5061858   | 55.1914944  |  0.4983773  | 0.6186599 |
|               countryCzech Republic                | \-30.6603672  | 49.4033972  | \-0.6206125 | 0.5354245 |
|                   countryDenmark                   |  \-2.2782148  | 52.4716318  | \-0.0434180 | 0.9654032 |
|                   countryEcuador                   |  58.1899128   | 79.0078560  |  0.7365079  | 0.4621178 |
|                 countryEl Salvador                 |  207.6717229  | 64.1999930  |  3.2347624  | 0.0013830 |
|                   countryEstonia                   | \-32.2758679  | 46.5539713  | \-0.6933000 | 0.4887701 |
|                   countryFinland                   | \-21.0228586  | 49.6374718  | \-0.4235280 | 0.6722772 |
|                   countryFrance                    | \-105.2999170 | 112.4100320 | \-0.9367484 | 0.3497993 |
|                   countryGeorgia                   | \-89.3996922  | 48.0369298  | \-1.8610617 | 0.0639188 |
|                   countryGermany                   | \-91.3943052  | 93.2920145  | \-0.9796584 | 0.3282095 |
|                   countryGreece                    |  30.5154918   | 60.8531869  |  0.5014609  | 0.6164917 |
|                   countryGrenada                   | \-24.4676242  | 46.7899799  | \-0.5229244 | 0.6014937 |
|                  countryGuatemala                  |  234.1930752  | 71.2253740  |  3.2880568  | 0.0011550 |
|                   countryGuyana                    |  104.3136871  | 54.8142515  |  1.9030395  | 0.0581934 |
|                   countryHungary                   | \-34.5270023  | 49.0563522  | \-0.7038233 | 0.4822031 |
|                   countryIceland                   |   7.9415172   | 52.5237171  |  0.1511987  | 0.8799419 |
|                   countryIreland                   |  \-8.6771935  | 55.1208823  | \-0.1574212 | 0.8750410 |
|                   countryIsrael                    |  16.8458645   | 54.7820046  |  0.3075073  | 0.7587154 |
|                    countryItaly                    | \-67.6038317  | 73.9115408  | \-0.9146587 | 0.3612593 |
|                   countryJamaica                   | \-19.7179038  | 62.4357602  | \-0.3158111 | 0.7524115 |
|                    countryJapan                    |  34.3524642   | 100.8607055 |  0.3405931  | 0.7336982 |
|                 countryKazakhstan                  |  \-3.4935459  | 48.7696663  | \-0.0716336 | 0.9429512 |
|                   countryKuwait                    | \-39.6137335  | 59.4943282  | \-0.6658405 | 0.5061319 |
|                 countryKyrgyzstan                  | \-16.3576892  | 50.4795577  | \-0.3240458 | 0.7461765 |
|                   countryLatvia                    | \-30.8845952  | 46.6460853  | \-0.6621048 | 0.5085189 |
|                  countryLithuania                  | \-38.1505197  | 47.0623068  | \-0.8106385 | 0.4183505 |
|                 countryLuxembourg                  |  \-4.8843261  | 47.7524912  | \-0.1022842 | 0.9186137 |
|                  countryMaldives                   |  \-6.1682286  | 56.7712514  | \-0.1086506 | 0.9135675 |
|                    countryMalta                    | \-12.2437448  | 47.9841743  | \-0.2551621 | 0.7988093 |
|                  countryMauritius                  |  30.3973643   | 48.7629707  |  0.6233698  | 0.5336144 |
|                   countryMexico                    |  257.1600274  | 77.8513192  |  3.3032199  | 0.0010968 |
|                 countryNetherlands                 | \-42.4907638  | 53.2673488  | \-0.7976887 | 0.4258143 |
|                 countryNew Zealand                 |  11.9630164   | 57.5125800  |  0.2080070  | 0.8353943 |
|                  countryNicaragua                  |  137.0146074  | 57.0908790  |  2.3999387  | 0.0171360 |
|                   countryNorway                    |  \-9.1076879  | 51.6711522  | \-0.1762625 | 0.8602315 |
|                    countryOman                     | \-33.7364104  | 50.7417517  | \-0.6648649 | 0.5067547 |
|                   countryPanama                    |  93.7304125   | 79.6117150  |  1.1773445  | 0.2401867 |
|                  countryParaguay                   |  53.0385177   | 68.2650339  |  0.7769500  | 0.4379287 |
|                 countryPhilippines                 |  36.5082355   | 57.9542416  |  0.6299493  | 0.5293077 |
|                   countryPoland                    | \-38.8078416  | 51.8174395  | \-0.7489340 | 0.4546067 |
|                  countryPortugal                   | \-32.8643537  | 61.1189929  | \-0.5377110 | 0.5912588 |
|                 countryPuerto Rico                 |  38.7931170   | 52.4072026  |  0.7402249  | 0.4598637 |
|                    countryQatar                    |  \-1.1974432  | 48.4829511  | \-0.0246982 | 0.9803155 |
|              countryRepublic of Korea              | \-29.4569261  | 56.8074907  | \-0.5185395 | 0.6045443 |
|                   countryRomania                   | \-41.5634230  | 52.9859203  | \-0.7844239 | 0.4335400 |
|             countryRussian Federation              |  17.4347954   | 69.1062358  |  0.2522898  | 0.8010261 |
|                 countrySaint Lucia                 | \-15.8095497  | 51.8878880  | \-0.3046867 | 0.7608603 |
|        countrySaint Vincent and Grenadines         | \-27.5832111  | 48.5081666  | \-0.5686303 | 0.5701216 |
|                   countrySerbia                    | \-53.8483241  | 56.8629573  | \-0.9469842 | 0.3445686 |
|                 countrySeychelles                  | \-24.2871829  | 46.5024435  | \-0.5222776 | 0.6019433 |
|                  countrySingapore                  |   0.1469891   | 52.0326665  |  0.0028249  | 0.9977483 |
|                  countrySlovakia                   | \-31.6894889  | 47.9297048  | \-0.6611660 | 0.5091196 |
|                  countrySlovenia                   | \-31.4153576  | 47.2854181  | \-0.6643773 | 0.5070661 |
|                countrySouth Africa                 |  \-6.8979080  | 50.9168069  | \-0.1354741 | 0.8923469 |
|                    countrySpain                    | \-56.7193543  | 70.6975687  | \-0.8022815 | 0.4231582 |
|                  countrySuriname                   | \-14.0930317  | 50.8811914  | \-0.2769792 | 0.7820268 |
|                   countrySweden                    |  10.9433048   | 54.1771757  |  0.2019911  | 0.8400893 |
|                 countrySwitzerland                 | \-15.3574909  | 52.0791443  | \-0.2948875 | 0.7683265 |
|                  countryThailand                   |  25.1456195   | 61.1912001  |  0.4109352  | 0.6814749 |
|             countryTrinidad and Tobago             |  43.0888480   | 49.4390769  |  0.8715545  | 0.3842944 |
|                   countryTurkey                    |  17.4352484   | 61.3599175  |  0.2841472  | 0.7765347 |
|                countryTurkmenistan                 |  49.5388793   | 50.3687642  |  0.9835238  | 0.3263082 |
|                   countryUkraine                   | \-30.0502172  | 50.8654312  | \-0.5907788 | 0.5552067 |
|            countryUnited Arab Emirates             | \-12.1592031  | 50.3927216  | \-0.2412889 | 0.8095306 |
|               countryUnited Kingdom                |  25.9146866   | 61.6048939  |  0.4206595  | 0.6743680 |
|                countryUnited States                | \-200.9580923 | 326.4665033 | \-0.6155550 | 0.5387527 |
|                   countryUruguay                   |  \-1.1862874  | 48.5486676  | \-0.0244350 | 0.9805253 |
|                 countryUzbekistan                  |  10.2088261   | 53.3236188  |  0.1914504  | 0.8483294 |
|                      sexmale                       |  \-0.0107157  |  0.2270934  | \-0.0471864 | 0.9624027 |
|                   age25-34 years                   |  34.1410221   | 12.9511232  |  2.6361437  | 0.0089144 |
|                   age35-54 years                   |   7.4744118   | 13.3244521  |  0.5609545  | 0.5753350 |
|                   age5-14 years                    |  352.9316525  | 127.2989997 |  2.7724621  | 0.0059856 |
|                   age55-74 years                   |   2.9949460   | 13.3825569  |  0.2237947  | 0.8231013 |
|                    age75+ years                    |  11.8154452   | 16.7139006  |  0.7069233  | 0.4802779 |
|                    suicides\_no                    |   0.1059033   |  0.0343502  |  3.0830470  | 0.0022805 |
|                     population                     | \-11.1684613  | 19.5170748  | \-0.5722405 | 0.5676774 |
|              countryArgentina:sexmale              |   0.5795713   |  0.4508156  |  1.2856061  | 0.1997797 |
|               countryArmenia:sexmale               |   1.2549914   |  0.4550617  |  2.7578487  | 0.0062514 |
|                countryAruba:sexmale                |   0.1166559   |  0.3076882  |  0.3791369  | 0.7049106 |
|              countryAustralia:sexmale              |   0.8664480   |  0.3359649  |  2.5789836  | 0.0104864 |
|               countryAustria:sexmale               |   1.0820950   |  0.3533945  |  3.0620029  | 0.0024407 |
|               countryBahamas:sexmale               |   0.1054244   |  0.2881262  |  0.3658967  | 0.7147541 |
|               countryBahrain:sexmale               |   0.1510450   |  0.3330080  |  0.4535779  | 0.6505293 |
|              countryBarbados:sexmale               |   0.1679009   |  0.2992803  |  0.5610156  | 0.5752934 |
|               countryBelarus:sexmale               |   1.4574314   |  0.3571198  |  4.0810717  | 0.0000605 |
|               countryBelgium:sexmale               |   1.0979247   |  0.3452300  |  3.1802703  | 0.0016587 |
|               countryBelize:sexmale                |   0.1976271   |  0.3535818  |  0.5589289  | 0.5767146 |
|               countryBrazil:sexmale                |   0.3580110   |  0.4161740  |  0.8602435  | 0.3904857 |
|              countryBulgaria:sexmale               |   1.2484756   |  0.3382813  |  3.6906427  | 0.0002750 |
|               countryCanada:sexmale                |   0.7565068   |  0.3435658  |  2.2019270  | 0.0285915 |
|                countryChile:sexmale                |   0.8097643   |  0.3968321  |  2.0405716  | 0.0423526 |
|              countryColombia:sexmale               |   0.5679873   |  0.4123504  |  1.3774384  | 0.1696186 |
|             countryCosta Rica:sexmale              |   1.7799617   |  0.3581702  |  4.9695979  | 0.0000013 |
|               countryCroatia:sexmale               |   0.6228254   |  0.3314982  |  1.8788199  | 0.0614420 |
|                countryCuba:sexmale                 |   0.8253898   |  0.3298702  |  2.5021651  | 0.0129885 |
|               countryCyprus:sexmale                |   0.3967075   |  0.3486005  |  1.1380006  | 0.2562184 |
|           countryCzech Republic:sexmale            |   1.2920606   |  0.3376109  |  3.8270703  | 0.0001642 |
|               countryDenmark:sexmale               |   0.7048944   |  0.3356683  |  2.0999734  | 0.0367416 |
|               countryEcuador:sexmale               |   0.5050552   |  0.4155108  |  1.2155043  | 0.2253296 |
|             countryEl Salvador:sexmale             |  \-0.3370311  |  0.3741096  | \-0.9008887 | 0.3685215 |
|               countryEstonia:sexmale               |   0.9559644   |  0.3556801  |  2.6877085  | 0.0076815 |
|               countryFinland:sexmale               |   1.0329541   |  0.3784461  |  2.7294612  | 0.0067983 |
|               countryFrance:sexmale                |   0.7102235   |  0.3497200  |  2.0308345  | 0.0433386 |
|               countryGeorgia:sexmale               |   1.8868933   |  0.3719688  |  5.0727191  | 0.0000008 |
|               countryGermany:sexmale               |   0.9880358   |  0.3748991  |  2.6354713  | 0.0089316 |
|               countryGreece:sexmale                |   0.9882191   |  0.3352151  |  2.9480150  | 0.0035033 |
|               countryGrenada:sexmale               |   0.1821183   |  0.2787632  |  0.6533082  | 0.5141628 |
|              countryGuatemala:sexmale              |   0.4118748   |  0.3783932  |  1.0884834  | 0.2774384 |
|               countryGuyana:sexmale                |   0.1418585   |  0.3169121  |  0.4476273  | 0.6548129 |
|               countryHungary:sexmale               |   1.0907515   |  0.3252214  |  3.3538740  | 0.0009216 |
|               countryIceland:sexmale               |   0.9814025   |  0.4634937  |  2.1174019  | 0.0352214 |
|               countryIreland:sexmale               |   0.7112349   |  0.3504001  |  2.0297790  | 0.0434467 |
|               countryIsrael:sexmale                |   0.5260525   |  0.3997617  |  1.3159152  | 0.1894176 |
|                countryItaly:sexmale                |   1.5320703   |  0.3511507  |  4.3629993  | 0.0000188 |
|               countryJamaica:sexmale               |   0.0523412   |  0.3387892  |  0.1544948  | 0.8773453 |
|                countryJapan:sexmale                |   0.5526302   |  0.4233460  |  1.3053866  | 0.1929710 |
|             countryKazakhstan:sexmale              |   0.5892074   |  0.4193929  |  1.4049054  | 0.1613007 |
|               countryKuwait:sexmale                |   0.1060954   |  0.3162878  |  0.3354395  | 0.7375771 |
|             countryKyrgyzstan:sexmale              |   0.7140422   |  0.3899439  |  1.8311409  | 0.0682792 |
|               countryLatvia:sexmale                |   1.2898852   |  0.3467595  |  3.7198268  | 0.0002466 |
|              countryLithuania:sexmale              |   1.1178207   |  0.3445042  |  3.2447227  | 0.0013374 |
|             countryLuxembourg:sexmale              |   0.7892251   |  0.3007346  |  2.6243244  | 0.0092209 |
|              countryMaldives:sexmale               |   0.3343434   |  0.3690679  |  0.9059131  | 0.3658612 |
|                countryMalta:sexmale                |   0.6951721   |  0.3027363  |  2.2962959  | 0.0224934 |
|              countryMauritius:sexmale              |   0.3825192   |  0.3912762  |  0.9776194  | 0.3292153 |
|               countryMexico:sexmale                |   0.3327801   |  0.5049732  |  0.6590055  | 0.5105037 |
|             countryNetherlands:sexmale             |   1.0992067   |  0.3381601  |  3.2505508  | 0.0013114 |
|             countryNew Zealand:sexmale             |   0.5020400   |  0.3434187  |  1.4618889  | 0.1450376 |
|              countryNicaragua:sexmale              |   0.5379344   |  0.3796622  |  1.4168762  | 0.1577741 |
|               countryNorway:sexmale                |   1.1584008   |  0.4104400  |  2.8223392  | 0.0051540 |
|                countryOman:sexmale                 |   0.3349979   |  0.3206582  |  1.0447196  | 0.2971698 |
|               countryPanama:sexmale                |   0.4349599   |  0.3512737  |  1.2382366  | 0.2167992 |
|              countryParaguay:sexmale               |   0.2895504   |  0.3861764  |  0.7497877  | 0.4540932 |
|             countryPhilippines:sexmale             |   0.8787084   |  0.4367682  |  2.0118417  | 0.0453182 |
|               countryPoland:sexmale                |   1.3455826   |  0.3541449  |  3.7995256  | 0.0001825 |
|              countryPortugal:sexmale               |   0.5256007   |  0.3283769  |  1.6006022  | 0.1107381 |
|             countryPuerto Rico:sexmale             |   1.2066653   |  0.3372530  |  3.5779232  | 0.0004164 |
|                countryQatar:sexmale                |   0.3721701   |  0.3795911  |  0.9804500  | 0.3278195 |
|          countryRepublic of Korea:sexmale          |   0.7391786   |  0.3573618  |  2.0684318  | 0.0396361 |
|               countryRomania:sexmale               |   1.2378344   |  0.3299762  |  3.7512834  | 0.0002191 |
|         countryRussian Federation:sexmale          |  \-0.3485045  |  0.8106883  | \-0.4298872 | 0.6676510 |
|             countrySaint Lucia:sexmale             |   0.0101062   |  0.3067465  |  0.0329463  | 0.9737439 |
|    countrySaint Vincent and Grenadines:sexmale     |   0.2035064   |  0.2995447  |  0.6793855  | 0.4975272 |
|               countrySerbia:sexmale                |   0.9383195   |  0.3319125  |  2.8270086  | 0.0050818 |
|             countrySeychelles:sexmale              |   0.2141285   |  0.2971609  |  0.7205809  | 0.4718461 |
|              countrySingapore:sexmale              |   0.2826012   |  0.3045484  |  0.9279352  | 0.3543434 |
|              countrySlovakia:sexmale               |   1.5202294   |  0.3384482  |  4.4917641  | 0.0000108 |
|              countrySlovenia:sexmale               |   1.9341515   |  0.3432574  |  5.6346980  | 0.0000000 |
|            countrySouth Africa:sexmale             |   0.8440745   |  0.4109875  |  2.0537716  | 0.0410464 |
|                countrySpain:sexmale                |   1.4604617   |  0.3406867  |  4.2868178  | 0.0000260 |
|              countrySuriname:sexmale               |   0.4172944   |  0.3277978  |  1.2730237  | 0.2042017 |
|               countrySweden:sexmale                |   0.4989404   |  0.3534852  |  1.4114888  | 0.1593539 |
|             countrySwitzerland:sexmale             |   1.2064222   |  0.3384687  |  3.5643537  | 0.0004374 |
|              countryThailand:sexmale               |   0.6947505   |  0.3585718  |  1.9375491  | 0.0538136 |
|         countryTrinidad and Tobago:sexmale         |   0.3844815   |  0.3619820  |  1.0621564  | 0.2891979 |
|               countryTurkey:sexmale                |   0.5174658   |  0.3799204  |  1.3620373  | 0.1744220 |
|            countryTurkmenistan:sexmale             |  \-0.0135498  |  0.3919758  | \-0.0345680 | 0.9724521 |
|               countryUkraine:sexmale               |   0.9186652   |  0.4066876  |  2.2588964  | 0.0247589 |
|        countryUnited Arab Emirates:sexmale         |   0.4344796   |  0.4174157  |  1.0408799  | 0.2989449 |
|           countryUnited Kingdom:sexmale            |   0.3543659   |  0.3377524  |  1.0491882  | 0.2951129 |
|            countryUnited States:sexmale            |  \-1.3284722  |  0.9664767  | \-1.3745516 | 0.1705113 |
|               countryUruguay:sexmale               |  \-0.1003770  |  0.4313058  | \-0.2327281 | 0.8161645 |
|             countryUzbekistan:sexmale              |   0.4993624   |  0.3542155  |  1.4097700  | 0.1598604 |
|          countryArgentina:age25-34 years           |   2.9120911   |  1.2430162  |  2.3427620  | 0.0199328 |
|           countryArmenia:age25-34 years            |   0.3574468   |  0.7101015  |  0.5033742  | 0.6151480 |
|            countryAruba:age25-34 years             |  \-4.5276345  |  1.9354988  | \-2.3392597 | 0.0201165 |
|          countryAustralia:age25-34 years           |   2.4153397   |  1.0448029  |  2.3117658  | 0.0216107 |
|           countryAustria:age25-34 years            |   1.3306626   |  0.8124620  |  1.6378152  | 0.1027284 |
|           countryBahamas:age25-34 years            |  \-2.4635592  |  1.2157093  | \-2.0264378 | 0.0437902 |
|           countryBahrain:age25-34 years            |  \-0.1838529  |  0.8967154  | \-0.2050293 | 0.8377174 |
|           countryBarbados:age25-34 years           |  \-2.8652199  |  1.3819397  | \-2.0733320 | 0.0391741 |
|           countryBelarus:age25-34 years            |   1.7404178   |  0.8626776  |  2.0174602  | 0.0447248 |
|           countryBelgium:age25-34 years            |   1.8429108   |  0.8580949  |  2.1476770  | 0.0327088 |
|            countryBelize:age25-34 years            |  \-1.9368989  |  1.4272199  | \-1.3571131 | 0.1759791 |
|            countryBrazil:age25-34 years            |   4.4010603   |  1.7144476  |  2.5670428  | 0.0108446 |
|           countryBulgaria:age25-34 years           |   1.2198645   |  0.8496075  |  1.4357977  | 0.1523200 |
|            countryCanada:age25-34 years            |   2.7812282   |  1.1468696  |  2.4250606  | 0.0160208 |
|            countryChile:age25-34 years             |   1.8414610   |  0.9927082  |  1.8549871  | 0.0647848 |
|           countryColombia:age25-34 years           |   2.5357877   |  1.2900919  |  1.9655868  | 0.0504622 |
|          countryCosta Rica:age25-34 years          |   1.0169076   |  0.7681599  |  1.3238228  | 0.1867808 |
|           countryCroatia:age25-34 years            |   0.2239983   |  0.7727764  |  0.2898617  | 0.7721642 |
|             countryCuba:age25-34 years             |   1.5607308   |  0.8681652  |  1.7977349  | 0.0734353 |
|            countryCyprus:age25-34 years            |  \-1.6314411  |  0.9216179  | \-1.7701925 | 0.0779237 |
|        countryCzech Republic:age25-34 years        |   1.6694494   |  0.9155504  |  1.8234380  | 0.0694408 |
|           countryDenmark:age25-34 years            |   0.7834930   |  0.7398981  |  1.0589201  | 0.2906665 |
|           countryEcuador:age25-34 years            |   1.6520980   |  1.0082214  |  1.6386261  | 0.1025592 |
|         countryEl Salvador:age25-34 years          |  \-1.2048735  |  0.8872622  | \-1.3579679 | 0.1757081 |
|           countryEstonia:age25-34 years            |  \-0.4929616  |  0.8485355  | \-0.5809557 | 0.5617979 |
|           countryFinland:age25-34 years            |   0.7905067   |  0.7530307  |  1.0497669  | 0.2948472 |
|            countryFrance:age25-34 years            |   3.3566150   |  1.2889372  |  2.6041726  | 0.0097654 |
|           countryGeorgia:age25-34 years            |   0.8327877   |  0.7451154  |  1.1176628  | 0.2647926 |
|           countryGermany:age25-34 years            |   3.3798752   |  1.3507642  |  2.5021949  | 0.0129874 |
|            countryGreece:age25-34 years            |   2.2800842   |  1.0123310  |  2.2523109  | 0.0251777 |
|           countryGrenada:age25-34 years            |  \-3.7158409  |  1.6583622  | \-2.2406691 | 0.0259333 |
|          countryGuatemala:age25-34 years           |  \-0.3112279  |  1.0889824  | \-0.2857970 | 0.7752722 |
|            countryGuyana:age25-34 years            |  \-2.4241460  |  0.9341226  | \-2.5951047 | 0.0100197 |
|           countryHungary:age25-34 years            |   1.9009513   |  0.8923538  |  2.1302664  | 0.0341342 |
|           countryIceland:age25-34 years            |  \-2.5057086  |  1.2910219  | \-1.9408722 | 0.0534069 |
|           countryIreland:age25-34 years            |   0.9455832   |  0.8682260  |  1.0890980  | 0.2771679 |
|            countryIsrael:age25-34 years            |   1.1282781   |  0.8099511  |  1.3930200  | 0.1648612 |
|            countryItaly:age25-34 years             |   3.4305835   |  1.3194469  |  2.6000163  | 0.0098812 |
|           countryJamaica:age25-34 years            |   0.2091572   |  0.8109328  |  0.2579218  | 0.7966812 |
|            countryJapan:age25-34 years             |   3.5724745   |  1.5203299  |  2.3498022  | 0.0195681 |
|          countryKazakhstan:age25-34 years          |   2.0302477   |  1.0126632  |  2.0048597  | 0.0460650 |
|            countryKuwait:age25-34 years            |   1.0055094   |  0.9531846  |  1.0548947  | 0.2925001 |
|          countryKyrgyzstan:age25-34 years          |   0.8362859   |  0.7994902  |  1.0460239  | 0.2965684 |
|            countryLatvia:age25-34 years            |  \-0.4024830  |  0.7596388  | \-0.5298348 | 0.5967005 |
|          countryLithuania:age25-34 years           |   0.1811768   |  0.7163576  |  0.2529139  | 0.8005443 |
|          countryLuxembourg:age25-34 years          |  \-1.5056604  |  1.1913885  | \-1.2637862 | 0.2074934 |
|           countryMaldives:age25-34 years           |  \-2.1143273  |  1.1235370  | \-1.8818494 | 0.0610276 |
|            countryMalta:age25-34 years             |  \-2.2484581  |  1.2085765  | \-1.8604186 | 0.0640100 |
|          countryMauritius:age25-34 years           |  \-0.2962515  |  0.8321271  | \-0.3560171 | 0.7221304 |
|            countryMexico:age25-34 years            |   3.2987381   |  1.5632210  |  2.1102187  | 0.0358413 |
|         countryNetherlands:age25-34 years          |   2.2095287   |  0.9296453  |  2.3767439  | 0.0182259 |
|         countryNew Zealand:age25-34 years          |   0.3499287   |  0.7269317  |  0.4813777  | 0.6306726 |
|          countryNicaragua:age25-34 years           |  \-0.0334538  |  0.8060086  | \-0.0415055 | 0.9669263 |
|            countryNorway:age25-34 years            |   0.9135709   |  0.7407471  |  1.2333101  | 0.2186278 |
|             countryOman:age25-34 years             |   0.5299488   |  0.7865165  |  0.6737923  | 0.5010709 |
|            countryPanama:age25-34 years            |  \-0.9715329  |  0.7417726  | \-1.3097450 | 0.1914941 |
|           countryParaguay:age25-34 years           |   0.6297862   |  0.8620674  |  0.7305533  | 0.4657416 |
|         countryPhilippines:age25-34 years          |   3.3439585   |  1.4920954  |  2.2411158  | 0.0259040 |
|            countryPoland:age25-34 years            |   3.0381338   |  1.2200988  |  2.4900720  | 0.0134274 |
|           countryPortugal:age25-34 years           |   1.8106880   |  0.9499328  |  1.9061222  | 0.0577904 |
|         countryPuerto Rico:age25-34 years          |   0.6056927   |  0.7239249  |  0.8366789  | 0.4035786 |
|            countryQatar:age25-34 years             |  \-0.2138619  |  0.8231446  | \-0.2598108 | 0.7952253 |
|      countryRepublic of Korea:age25-34 years       |   2.8735501   |  1.3043094  |  2.2031200  | 0.0285063 |
|           countryRomania:age25-34 years            |   2.2368660   |  1.0637057  |  2.1028992  | 0.0364826 |
|      countryRussian Federation:age25-34 years      |   4.1422917   |  1.6283935  |  2.5437904  | 0.0115736 |
|         countrySaint Lucia:age25-34 years          |  \-3.2885860  |  1.4919258  | \-2.2042557 | 0.0284253 |
| countrySaint Vincent and Grenadines:age25-34 years |  \-3.7127139  |  1.7127824  | \-2.1676506 | 0.0311370 |
|            countrySerbia:age25-34 years            |   1.7131108   |  0.8400552  |  2.0392836  | 0.0424819 |
|          countrySeychelles:age25-34 years          |  \-4.0657935  |  1.8342452  | \-2.2166031 | 0.0275580 |
|          countrySingapore:age25-34 years           |   0.7931565   |  0.7662139  |  1.0351634  | 0.3016010 |
|           countrySlovakia:age25-34 years           |   1.0846200   |  0.8072222  |  1.3436450  | 0.1802913 |
|           countrySlovenia:age25-34 years           |   0.1572694   |  0.8384177  |  0.1875789  | 0.8513602 |
|         countrySouth Africa:age25-34 years         |   3.1893801   |  1.3496341  |  2.3631442  | 0.0188929 |
|            countrySpain:age25-34 years             |   3.2057529   |  1.3903659  |  2.3056901  | 0.0219537 |
|           countrySuriname:age25-34 years           |  \-1.8870834  |  1.0391788  | \-1.8159373 | 0.0705875 |
|            countrySweden:age25-34 years            |   1.2724190   |  0.8150215  |  1.5612092  | 0.1197495 |
|         countrySwitzerland:age25-34 years          |   1.6250351   |  0.8193587  |  1.9833013  | 0.0484368 |
|           countryThailand:age25-34 years           |   3.5692026   |  1.3740556  |  2.5975678  | 0.0099500 |
|     countryTrinidad and Tobago:age25-34 years      |  \-0.4723989  |  0.8147562  | \-0.5798040 | 0.5625732 |
|            countryTurkey:age25-34 years            |   3.4015664   |  1.4190717  |  2.3970364  | 0.0172691 |
|         countryTurkmenistan:age25-34 years         |   0.4705749   |  0.7739324  |  0.6080311  | 0.5437233 |
|           countryUkraine:age25-34 years            |   3.0464416   |  1.2615341  |  2.4148706  | 0.0164652 |
|     countryUnited Arab Emirates:age25-34 years     |   1.4526272   |  0.8506990  |  1.7075690  | 0.0889678 |
|        countryUnited Kingdom:age25-34 years        |   3.2481832   |  1.3002210  |  2.4981778  | 0.0131318 |
|        countryUnited States:age25-34 years         |   4.8208209   |  1.8415585  |  2.6177940  | 0.0093943 |
|           countryUruguay:age25-34 years            |   0.3848034   |  0.7198386  |  0.5345690  | 0.5934268 |
|          countryUzbekistan:age25-34 years          |   2.5954329   |  1.1868163  |  2.1868868  | 0.0296854 |
|          countryArgentina:age35-54 years           |   0.9279286   |  1.1887575  |  0.7805869  | 0.4357899 |
|           countryArmenia:age35-54 years            |  \-0.0323428  |  0.7890292  | \-0.0409906 | 0.9673364 |
|            countryAruba:age35-54 years             |  \-1.8092467  |  1.9882834  | \-0.9099541 | 0.3637302 |
|          countryAustralia:age35-54 years           |   1.0858586   |  1.2862262  |  0.8442206  | 0.3993598 |
|           countryAustria:age35-54 years            |   0.5937563   |  1.1097655  |  0.5350287  | 0.5931094 |
|           countryBahamas:age35-54 years            |  \-0.7060729  |  1.1601809  | \-0.6085886 | 0.5433542 |
|           countryBahrain:age35-54 years            |  \-0.1906834  |  0.8732714  | \-0.2183553 | 0.8273319 |
|           countryBarbados:age35-54 years           |  \-1.2460718  |  1.4692685  | \-0.8480900 | 0.3972057 |
|           countryBelarus:age35-54 years            |   0.3268498   |  0.8716542  |  0.3749764  | 0.7079985 |
|           countryBelgium:age35-54 years            |   1.2028445   |  1.1723688  |  1.0259950  | 0.3058936 |
|            countryBelize:age35-54 years            |  \-0.4900041  |  1.2484581  | \-0.3924874 | 0.6950352 |
|            countryBrazil:age35-54 years            |   0.7357502   |  1.7287763  |  0.4255902  | 0.6707756 |
|           countryBulgaria:age35-54 years           |   0.4885693   |  1.1286655  |  0.4328734  | 0.6654829 |
|            countryCanada:age35-54 years            |   1.2646284   |  1.4109581  |  0.8962905  | 0.3709668 |
|            countryChile:age35-54 years             |   1.3899307   |  1.0004461  |  1.3893109  | 0.1659843 |
|           countryColombia:age35-54 years           |   1.8486411   |  1.2662096  |  1.4599803  | 0.1455611 |
|          countryCosta Rica:age35-54 years          |   1.1297723   |  0.7955563  |  1.4201035  | 0.1568334 |
|           countryCroatia:age35-54 years            |   0.2363220   |  0.9013737  |  0.2621799  | 0.7934004 |
|             countryCuba:age35-54 years             |   1.4267705   |  1.7122747  |  0.8332603  | 0.4054997 |
|            countryCyprus:age35-54 years            |   0.3213950   |  1.1417428  |  0.2814951  | 0.7785654 |
|        countryCzech Republic:age35-54 years        |   0.5714967   |  0.9494878  |  0.6019000  | 0.5477906 |
|           countryDenmark:age35-54 years            |   1.3634622   |  1.1114069  |  1.2267894  | 0.2210651 |
|           countryEcuador:age35-54 years            |   0.4305174   |  0.9891098  |  0.4352574  | 0.6637541 |
|         countryEl Salvador:age35-54 years          |   0.1963019   |  0.7269746  |  0.2700258  | 0.7873649 |
|           countryEstonia:age35-54 years            |  \-0.3666292  |  0.8331544  | \-0.4400495 | 0.6602845 |
|           countryFinland:age35-54 years            |   0.2764311   |  0.8374458  |  0.3300884  | 0.7416118 |
|            countryFrance:age35-54 years            |  \-1.7782180  |  2.5093315  | \-0.7086421 | 0.4792122 |
|           countryGeorgia:age35-54 years            |  \-0.3753217  |  0.7554444  | \-0.4968224 | 0.6197544 |
|           countryGermany:age35-54 years            |  \-1.2045236  |  2.3331789  | \-0.5162585 | 0.6061338 |
|            countryGreece:age35-54 years            |   1.8120775   |  1.5759014  |  1.1498673  | 0.2513062 |
|           countryGrenada:age35-54 years            |  \-0.7745254  |  1.7458238  | \-0.4436447 | 0.6576863 |
|          countryGuatemala:age35-54 years           |  \-2.0152808  |  1.0653993  | \-1.8915731 | 0.0597130 |
|            countryGuyana:age35-54 years            |   0.0984008   |  0.9307021  |  0.1057275  | 0.9158840 |
|           countryHungary:age35-54 years            |   0.9106240   |  0.9638564  |  0.9447714  | 0.3456951 |
|           countryIceland:age35-54 years            |   0.4783112   |  1.4419967  |  0.3317006  | 0.7403955 |
|           countryIreland:age35-54 years            |   0.3026804   |  0.9839985  |  0.3076025  | 0.7586430 |
|            countryIsrael:age35-54 years            |   0.6201208   |  0.8123638  |  0.7633535  | 0.4459782 |
|            countryItaly:age35-54 years             |   0.3988221   |  2.1312472  |  0.1871309  | 0.8517110 |
|           countryJamaica:age35-54 years            |  \-0.1757430  |  0.7036119  | \-0.2497727 | 0.8029699 |
|            countryJapan:age35-54 years             |  \-0.9589646  |  2.1692164  | \-0.4420788 | 0.6588174 |
|          countryKazakhstan:age35-54 years          |   0.1872122   |  0.9550390  |  0.1960257  | 0.8447506 |
|            countryKuwait:age35-54 years            |  \-0.2801241  |  0.7947192  | \-0.3524818 | 0.7247763 |
|          countryKyrgyzstan:age35-54 years          |   0.0289388   |  0.7123338  |  0.0406254  | 0.9676272 |
|            countryLatvia:age35-54 years            |  \-0.1132262  |  0.7585442  | \-0.1492678 | 0.8814636 |
|          countryLithuania:age35-54 years           |  \-0.0957820  |  0.7506065  | \-0.1276061 | 0.8985641 |
|          countryLuxembourg:age35-54 years          |   0.7303661   |  1.3417544  |  0.5443367  | 0.5866989 |
|           countryMaldives:age35-54 years           |  \-0.6483132  |  1.1880753  | \-0.5456836 | 0.5857739 |
|            countryMalta:age35-54 years             |  \-0.9307916  |  1.2545889  | \-0.7419096 | 0.4588441 |
|          countryMauritius:age35-54 years           |   0.7843937   |  0.8441636  |  0.9291963  | 0.3536909 |
|            countryMexico:age35-54 years            |   1.9255333   |  1.5201198  |  1.2666984  | 0.2064515 |
|         countryNetherlands:age35-54 years          |   0.8646354   |  1.1757917  |  0.7353644  | 0.4628124 |
|         countryNew Zealand:age35-54 years          |   0.4285060   |  1.0008925  |  0.4281239  | 0.6689325 |
|          countryNicaragua:age35-54 years           |  \-0.3136829  |  0.7346997  | \-0.4269538 | 0.6697834 |
|            countryNorway:age35-54 years            |   1.2082674   |  0.9550114  |  1.2651864  | 0.2069920 |
|             countryOman:age35-54 years             |   0.0159486   |  0.6861807  |  0.0232425  | 0.9814755 |
|            countryPanama:age35-54 years            |   0.6175815   |  0.9103025  |  0.6784355  | 0.4981282 |
|           countryParaguay:age35-54 years           |   0.0976470   |  0.7647916  |  0.1276780  | 0.8985073 |
|         countryPhilippines:age35-54 years          |   0.6770078   |  1.4287197  |  0.4738562  | 0.6360193 |
|            countryPoland:age35-54 years            |   0.6392678   |  1.2205080  |  0.5237719  | 0.6009050 |
|           countryPortugal:age35-54 years           |   0.3862760   |  1.6627750  |  0.2323081  | 0.8164903 |
|         countryPuerto Rico:age35-54 years          |   1.8971057   |  0.8906609  |  2.1299978  | 0.0341566 |
|            countryQatar:age35-54 years             |  \-0.5895075  |  0.7466800  | \-0.7895048 | 0.4305712 |
|      countryRepublic of Korea:age35-54 years       |  \-1.1219253  |  1.5262083  | \-0.7351063 | 0.4629693 |
|           countryRomania:age35-54 years            |   0.4258817   |  1.1336807  |  0.3756628  | 0.7074887 |
|      countryRussian Federation:age35-54 years      |   0.3049266   |  1.7966722  |  0.1697174  | 0.8653707 |
|         countrySaint Lucia:age35-54 years          |  \-0.8198095  |  1.5414487  | \-0.5318435 | 0.5953105 |
| countrySaint Vincent and Grenadines:age35-54 years |  \-1.1010442  |  1.7202748  | \-0.6400397 | 0.5227376 |
|            countrySerbia:age35-54 years            |   0.5649151   |  1.2523187  |  0.4510953  | 0.6523150 |
|          countrySeychelles:age35-54 years          |  \-1.3422696  |  1.8184179  | \-0.7381524 | 0.4611197 |
|          countrySingapore:age35-54 years           |   0.7510734   |  1.1130007  |  0.6748184  | 0.5004197 |
|           countrySlovakia:age35-54 years           |   0.7265768   |  0.7951965  |  0.9137072  | 0.3617582 |
|           countrySlovenia:age35-54 years           |   1.2163365   |  0.9250633  |  1.3148684  | 0.1897687 |
|         countrySouth Africa:age35-54 years         |   0.6357614   |  1.2500891  |  0.5085729  | 0.6115037 |
|            countrySpain:age35-54 years             |   0.9063735   |  1.9924050  |  0.4549143  | 0.6495689 |
|           countrySuriname:age35-54 years           |  \-0.4559557  |  1.0592441  | \-0.4304538 | 0.6672394 |
|            countrySweden:age35-54 years            |   0.8622203   |  1.0252420  |  0.8409920  | 0.4011626 |
|         countrySwitzerland:age35-54 years          |   1.5526171   |  1.2039149  |  1.2896402  | 0.1983770 |
|           countryThailand:age35-54 years           |   1.2371592   |  1.5095448  |  0.8195578  | 0.4132551 |
|     countryTrinidad and Tobago:age35-54 years      |   0.5053142   |  0.8024173  |  0.6297399  | 0.5294445 |
|            countryTurkey:age35-54 years            |   0.7508349   |  1.3715099  |  0.5474513  | 0.5845610 |
|         countryTurkmenistan:age35-54 years         |   0.2256680   |  0.7190915  |  0.3138238  | 0.7539187 |
|           countryUkraine:age35-54 years            |   0.1716701   |  1.2847496  |  0.1336214  | 0.8938103 |
|     countryUnited Arab Emirates:age35-54 years     |  \-0.6713635  |  0.7604096  | \-0.8828972 | 0.3781468 |
|        countryUnited Kingdom:age35-54 years        |   0.9255389   |  1.4942026  |  0.6194200  | 0.5362084 |
|        countryUnited States:age35-54 years         |  \-6.2835256  |  5.1068007  | \-1.2304231 | 0.2197045 |
|           countryUruguay:age35-54 years            |   0.0868946   |  0.7395426  |  0.1174977  | 0.9065608 |
|          countryUzbekistan:age35-54 years          |   0.4223621   |  1.1054116  |  0.3820858  | 0.7027249 |
|           countryArgentina:age5-14 years           |  27.0291556   | 10.1756891  |  2.6562482  | 0.0084140 |
|            countryArmenia:age5-14 years            |  \-1.8645256  |  1.1842409  | \-1.5744480 | 0.1166587 |
|             countryAruba:age5-14 years             | \-45.4235658  | 16.6916767  | \-2.7213303 | 0.0069627 |
|           countryAustralia:age5-14 years           |  17.1954144   |  6.8657442  |  2.5045230  | 0.0129044 |
|            countryAustria:age5-14 years            |   5.3013250   |  2.4584133  |  2.1564011  | 0.0320141 |
|            countryBahamas:age5-14 years            | \-25.9613781  |  9.6840544  | \-2.6808377 | 0.0078364 |
|            countryBahrain:age5-14 years            | \-11.9688018  |  4.6428390  | \-2.5779058 | 0.0105183 |
|           countryBarbados:age5-14 years            | \-30.8453126  | 11.4865154  | \-2.6853499 | 0.0077344 |
|            countryBelarus:age5-14 years            |   5.7332413   |  2.7049243  |  2.1195570  | 0.0350372 |
|            countryBelgium:age5-14 years            |   9.0960627   |  3.7964978  |  2.3959088  | 0.0173211 |
|            countryBelize:age5-14 years             | \-21.7065990  |  7.9734693  | \-2.7223531 | 0.0069418 |
|            countryBrazil:age5-14 years             |  40.5053612   | 15.2107611  |  2.6629411  | 0.0082531 |
|           countryBulgaria:age5-14 years            |   2.9829026   |  1.5264575  |  1.9541341  | 0.0518093 |
|            countryCanada:age5-14 years             |  20.5245433   |  7.9522668  |  2.5809676  | 0.0104279 |
|             countryChile:age5-14 years             |  16.9727301   |  6.6346491  |  2.5581956  | 0.0111170 |
|           countryColombia:age5-14 years            |  28.5601631   | 10.6962470  |  2.6701107  | 0.0080838 |
|          countryCosta Rica:age5-14 years           |   4.2294459   |  2.0268685  |  2.0866898  | 0.0379378 |
|            countryCroatia:age5-14 years            |  \-1.6513247  |  0.4960256  | \-3.3291119 | 0.0010037 |
|             countryCuba:age5-14 years              |  11.0692720   |  4.2761746  |  2.5885922  | 0.0102059 |
|            countryCyprus:age5-14 years             | \-19.9173488  |  7.0812470  | \-2.8126894 | 0.0053062 |
|        countryCzech Republic:age5-14 years         |   5.8166414   |  2.8435438  |  2.0455607  | 0.0418548 |
|            countryDenmark:age5-14 years            |   2.6345343   |  1.5619729  |  1.6866709  | 0.0929241 |
|            countryEcuador:age5-14 years            |  19.5601814   |  7.2708116  |  2.6902336  | 0.0076253 |
|          countryEl Salvador:age5-14 years          |  11.1248049   |  4.2560654  |  2.6138707  | 0.0094998 |
|            countryEstonia:age5-14 years            | \-16.1258733  |  5.6872020  | \-2.8354669 | 0.0049533 |
|            countryFinland:age5-14 years            |   0.2674795   |  1.0891136  |  0.2455938  | 0.8061998 |
|            countryFrance:age5-14 years             |  27.5367919   | 10.4161559  |  2.6436617  | 0.0087242 |
|            countryGeorgia:age5-14 years            |   1.7134301   |  0.5718467  |  2.9963104  | 0.0030099 |
|            countryGermany:age5-14 years            |  27.3596629   | 10.3524837  |  2.6428115  | 0.0087455 |
|            countryGreece:age5-14 years             |   7.9290980   |  3.2890215  |  2.4107771  | 0.0166467 |
|            countryGrenada:age5-14 years            | \-40.8568065  | 15.1414250  | \-2.6983462 | 0.0074472 |
|           countryGuatemala:age5-14 years           |  22.7638500   |  8.0616098  |  2.8237350  | 0.0051323 |
|            countryGuyana:age5-14 years             | \-11.3073648  |  4.3994794  | \-2.5701597 | 0.0107500 |
|            countryHungary:age5-14 years            |   6.8543643   |  3.0207673  |  2.2690805  | 0.0241231 |
|            countryIceland:age5-14 years            | \-29.9762632  | 10.8308207  | \-2.7676816 | 0.0060714 |
|            countryIreland:age5-14 years            |   2.1804412   |  1.1254730  |  1.9373554  | 0.0538374 |
|            countryIsrael:age5-14 years             |  11.2711091   |  4.2511833  |  2.6512875  | 0.0085350 |
|             countryItaly:age5-14 years             |  24.4022829   |  9.3453189  |  2.6111771  | 0.0095729 |
|            countryJamaica:age5-14 years            |   2.4150479   |  0.7331719  |  3.2939722  | 0.0011319 |
|             countryJapan:age5-14 years             |  31.0021943   | 11.7290930  |  2.6431877  | 0.0087361 |
|          countryKazakhstan:age5-14 years           |  16.3524848   |  6.3569725  |  2.5723699  | 0.0106835 |
|            countryKuwait:age5-14 years             |   0.2642219   |  0.5223938  |  0.5057906  | 0.6134529 |
|          countryKyrgyzstan:age5-14 years           |   8.2630540   |  3.2424134  |  2.5484270  | 0.0114248 |
|            countryLatvia:age5-14 years             | \-11.5700342  |  3.8826330  | \-2.9799454 | 0.0031694 |
|           countryLithuania:age5-14 years           |  \-5.6864620  |  1.6935455  | \-3.3577261 | 0.0009094 |
|          countryLuxembourg:age5-14 years           | \-24.6445827  |  9.1525562  | \-2.6926448 | 0.0075720 |
|           countryMaldives:age5-14 years            | \-24.6280756  |  9.2448837  | \-2.6639681 | 0.0082286 |
|             countryMalta:age5-14 years             | \-29.4195500  | 10.8213120  | \-2.7186676 | 0.0070174 |
|           countryMauritius:age5-14 years           | \-11.2091515  |  3.8949459  | \-2.8778709 | 0.0043527 |
|            countryMexico:age5-14 years             |  37.6858141   | 14.1454872  |  2.6641581  | 0.0082241 |
|          countryNetherlands:age5-14 years          |  14.0301807   |  5.6535668  |  2.4816512  | 0.0137408 |
|          countryNew Zealand:age5-14 years          |   1.4346539   |  1.0699387  |  1.3408748  | 0.1811879 |
|           countryNicaragua:age5-14 years           |  10.4533697   |  3.9575172  |  2.6413959  | 0.0087811 |
|            countryNorway:age5-14 years             |   1.0789653   |  1.2541297  |  0.8603299  | 0.3904381 |
|             countryOman:age5-14 years              |   1.5067292   |  0.5432598  |  2.7734966  | 0.0059672 |
|            countryPanama:age5-14 years             |   4.0967426   |  1.7287251  |  2.3698056  | 0.0185635 |
|           countryParaguay:age5-14 years            |  11.6829600   |  4.3680292  |  2.6746525  | 0.0079782 |
|          countryPhilippines:age5-14 years          |  36.5968525   | 13.6093162  |  2.6891030  | 0.0076504 |
|            countryPoland:age5-14 years             |  20.8017891   |  7.9827733  |  2.6058349  | 0.0097194 |
|           countryPortugal:age5-14 years            |   8.4325447   |  3.4476668  |  2.4458700  | 0.0151462 |
|          countryPuerto Rico:age5-14 years          |   0.2266043   |  0.7236824  |  0.3131268  | 0.7544475 |
|             countryQatar:age5-14 years             | \-13.4713611  |  5.0922348  | \-2.6454713 | 0.0086790 |
|       countryRepublic of Korea:age5-14 years       |  24.8901189   |  9.4990964  |  2.6202617  | 0.0093284 |
|            countryRomania:age5-14 years            |  15.6842364   |  5.9810990  |  2.6223001  | 0.0092743 |
|      countryRussian Federation:age5-14 years       |  32.4619082   | 12.4285918  |  2.6118734  | 0.0095540 |
|          countrySaint Lucia:age5-14 years          | \-34.7958622  | 12.9179812  | \-2.6935991 | 0.0075509 |
| countrySaint Vincent and Grenadines:age5-14 years  | \-40.3571604  | 14.9793013  | \-2.6941951 | 0.0075378 |
|            countrySerbia:age5-14 years             |   4.1597669   |  2.0236684  |  2.0555576  | 0.0408723 |
|          countrySeychelles:age5-14 years           | \-46.5997300  | 17.1847580  | \-2.7116896 | 0.0071624 |
|           countrySingapore:age5-14 years           |  \-0.9043723  |  0.4915073  | \-1.8399975 | 0.0669636 |
|           countrySlovakia:age5-14 years            |   1.5461262   |  0.8577674  |  1.8025004  | 0.0726808 |
|           countrySlovenia:age5-14 years            | \-11.1238755  |  3.9641468  | \-2.8061210 | 0.0054121 |
|         countrySouth Africa:age5-14 years          |  30.6673514   | 11.4043696  |  2.6890878  | 0.0076508 |
|             countrySpain:age5-14 years             |  21.6455574   |  8.5185139  |  2.5410016  | 0.0116639 |
|           countrySuriname:age5-14 years            | \-18.5627130  |  6.7647082  | \-2.7440523 | 0.0065120 |
|            countrySweden:age5-14 years             |   6.7379013   |  3.1106056  |  2.1661060  | 0.0312562 |
|          countrySwitzerland:age5-14 years          |   4.3694654   |  2.2240088  |  1.9646799  | 0.0505678 |
|           countryThailand:age5-14 years            |  28.5898341   | 10.8304244  |  2.6397704  | 0.0088222 |
|      countryTrinidad and Tobago:age5-14 years      | \-12.1034504  |  4.1139435  | \-2.9420556 | 0.0035691 |
|            countryTurkey:age5-14 years             |  32.8082995   | 12.0776729  |  2.7164421  | 0.0070633 |
|         countryTurkmenistan:age5-14 years          |   8.2550858   |  3.0545857  |  2.7025223  | 0.0073570 |
|            countryUkraine:age5-14 years            |  21.7441255   |  8.2831875  |  2.6250915  | 0.0092007 |
|     countryUnited Arab Emirates:age5-14 years      |   3.7578188   |  1.6046882  |  2.3417751  | 0.0199844 |
|        countryUnited Kingdom:age5-14 years         |  25.2646321   | 10.0802922  |  2.5063393  | 0.0128399 |
|         countryUnited States:age5-14 years         |  42.4973003   | 15.9279286  |  2.6680996  | 0.0081310 |
|            countryUruguay:age5-14 years            |   0.6950841   |  0.6909676  |  1.0059577  | 0.3154164 |
|          countryUzbekistan:age5-14 years           |  24.8859183   |  9.2488044  |  2.6907173  | 0.0076146 |
|          countryArgentina:age55-74 years           |   0.2165765   |  1.0940197  |  0.1979640  | 0.8432354 |
|           countryArmenia:age55-74 years            |   0.9237169   |  0.5400746  |  1.7103505  | 0.0884517 |
|            countryAruba:age55-74 years             |  \-0.5082364  |  2.0089797  | \-0.2529823 | 0.8004914 |
|          countryAustralia:age55-74 years           |   0.5221009   |  0.9180435  |  0.5687104  | 0.5700673 |
|           countryAustria:age55-74 years            |   0.7359548   |  0.8003860  |  0.9194998  | 0.3587277 |
|           countryBahamas:age55-74 years            |  \-0.0278195  |  1.1357077  | \-0.0244953 | 0.9804772 |
|           countryBahrain:age55-74 years            |  \-0.0089777  |  1.2104840  | \-0.0074166 | 0.9940884 |
|           countryBarbados:age55-74 years           |  \-0.4177190  |  1.3918761  | \-0.3001122 | 0.7643430 |
|           countryBelarus:age55-74 years            |   0.3540177   |  0.6332056  |  0.5590880  | 0.5766062 |
|           countryBelgium:age55-74 years            |   0.9861502   |  0.8331667  |  1.1836169  | 0.2376980 |
|            countryBelize:age55-74 years            |   2.2962976   |  3.4372828  |  0.6680561  | 0.5047191 |
|            countryBrazil:age55-74 years            |   0.1873064   |  1.6540102  |  0.1132438  | 0.9099289 |
|           countryBulgaria:age55-74 years           |   0.7614574   |  0.9847524  |  0.7732476  | 0.4401122 |
|            countryCanada:age55-74 years            |   0.7790619   |  1.0828307  |  0.7194678  | 0.4725301 |
|            countryChile:age55-74 years             |  \-0.2553246  |  0.8081352  | \-0.3159429 | 0.7523116 |
|           countryColombia:age55-74 years           |  \-2.6340590  |  1.3013587  | \-2.0240837 | 0.0440337 |
|          countryCosta Rica:age55-74 years          |  \-0.5998678  |  0.7542095  | \-0.7953597 | 0.4271649 |
|           countryCroatia:age55-74 years            |   0.4149519   |  0.7735827  |  0.5364028  | 0.5921610 |
|             countryCuba:age55-74 years             |   1.2920399   |  0.8411179  |  1.5360984  | 0.1257890 |
|            countryCyprus:age55-74 years            |  \-0.0737620  |  0.8391800  | \-0.0878977 | 0.9300289 |
|        countryCzech Republic:age55-74 years        |   0.5738050   |  0.7760355  |  0.7394057  | 0.4603600 |
|           countryDenmark:age55-74 years            |   1.2884137   |  0.8973568  |  1.4357875  | 0.1523229 |
|           countryEcuador:age55-74 years            |  \-1.2953911  |  1.3642879  | \-0.9494998 | 0.3432908 |
|         countryEl Salvador:age55-74 years          |  \-4.5627759  |  1.1977581  | \-3.8094303 | 0.0001757 |
|           countryEstonia:age55-74 years            |   0.1725321   |  0.7589534  |  0.2273290  | 0.8203552 |
|           countryFinland:age55-74 years            |   0.2019779   |  0.7096568  |  0.2846135  | 0.7761777 |
|            countryFrance:age55-74 years            |  \-1.0106503  |  1.9203573  | \-0.5262824 | 0.5991623 |
|           countryGeorgia:age55-74 years            |   0.8336921   |  0.5392343  |  1.5460664  | 0.1233636 |
|           countryGermany:age55-74 years            |  \-1.1142133  |  2.0155094  | \-0.5528197 | 0.5808848 |
|            countryGreece:age55-74 years            |   1.4438842   |  1.1830991  |  1.2204254  | 0.2234628 |
|           countryGrenada:age55-74 years            |   0.3632493   |  1.7543629  |  0.2070548  | 0.8361369 |
|          countryGuatemala:age55-74 years           |  \-8.1682524  |  2.0437375  | \-3.9967229 | 0.0000847 |
|            countryGuyana:age55-74 years            |  \-3.4677105  |  1.1818097  | \-2.9342377 | 0.0036571 |
|           countryHungary:age55-74 years            |   0.9986556   |  0.8029296  |  1.2437649  | 0.2147605 |
|           countryIceland:age55-74 years            |   0.2559982   |  1.2671477  |  0.2020272  | 0.8400611 |
|           countryIreland:age55-74 years            |   0.3133505   |  0.5687294  |  0.5509659  | 0.5821530 |
|            countryIsrael:age55-74 years            |   0.3335449   |  0.5744088  |  0.5806752  | 0.5619867 |
|            countryItaly:age55-74 years             |   0.4847712   |  1.7455186  |  0.2777233  | 0.7814561 |
|           countryJamaica:age55-74 years            |   0.3488517   |  0.8806504  |  0.3961297  | 0.6923500 |
|            countryJapan:age55-74 years             |  \-1.6500552  |  2.3611808  | \-0.6988263 | 0.4853154 |
|          countryKazakhstan:age55-74 years          |   0.1104048   |  0.8624878  |  0.1280074  | 0.8982469 |
|            countryKuwait:age55-74 years            |   1.0590147   |  1.3554685  |  0.7812905  | 0.4353768 |
|          countryKyrgyzstan:age55-74 years          |   0.1292295   |  0.9414265  |  0.1372699  | 0.8909288 |
|            countryLatvia:age55-74 years            |   0.4495387   |  0.6239137  |  0.7205142  | 0.4718870 |
|          countryLithuania:age55-74 years           |   0.2668625   |  0.5374382  |  0.4965454  | 0.6199495 |
|          countryLuxembourg:age55-74 years          |   0.6157674   |  1.1866336  |  0.5189196  | 0.6042796 |
|           countryMaldives:age55-74 years           |  \-0.3478011  |  1.9955427  | \-0.1742890 | 0.8617806 |
|            countryMalta:age55-74 years             |   0.1307538   |  1.2456052  |  0.1049721  | 0.9164828 |
|          countryMauritius:age55-74 years           |  \-0.0800052  |  0.6472819  | \-0.1236018 | 0.9017307 |
|            countryMexico:age55-74 years            |  \-3.6728922  |  1.7239423  | \-2.1305192 | 0.0341131 |
|         countryNetherlands:age55-74 years          |   0.7495181   |  0.8946254  |  0.8378010  | 0.4029491 |
|         countryNew Zealand:age55-74 years          |  \-0.0287517  |  0.5657972  | \-0.0508163 | 0.9595128 |
|          countryNicaragua:age55-74 years           |  \-5.0431327  |  1.3022787  | \-3.8725448 | 0.0001378 |
|            countryNorway:age55-74 years            |   0.9160530   |  0.6474820  |  1.4147931  | 0.1583835 |
|             countryOman:age55-74 years             |   1.3609748   |  1.0522875  |  1.2933488  | 0.1970938 |
|            countryPanama:age55-74 years            |  \-2.1612591  |  1.1443824  | \-1.8885813 | 0.0601150 |
|           countryParaguay:age55-74 years           |  \-1.2521892  |  1.3227333  | \-0.9466680 | 0.3447295 |
|         countryPhilippines:age55-74 years          |  \-0.8875378  |  1.5446926  | \-0.5745725 | 0.5661013 |
|            countryPoland:age55-74 years            |   0.6300773   |  1.0765903  |  0.5852526  | 0.5589100 |
|           countryPortugal:age55-74 years           |   0.5672293   |  1.3141561  |  0.4316301  | 0.6663853 |
|         countryPuerto Rico:age55-74 years          |   1.2001780   |  0.5277055  |  2.2743332  | 0.0238007 |
|            countryQatar:age55-74 years             |  \-0.5994707  |  0.8749719  | \-0.6851314 | 0.4939009 |
|      countryRepublic of Korea:age55-74 years       |  \-0.9384603  |  1.2662273  | \-0.7411468 | 0.4593056 |
|           countryRomania:age55-74 years            |   0.6138900   |  0.9166090  |  0.6697403  | 0.5036464 |
|      countryRussian Federation:age55-74 years      |   0.3217243   |  1.6579790  |  0.1940461  | 0.8462987 |
|         countrySaint Lucia:age55-74 years          |  \-0.2332632  |  1.5257571  | \-0.1528836 | 0.8786144 |
| countrySaint Vincent and Grenadines:age55-74 years |   0.2093849   |  1.7900197  |  0.1169735  | 0.9069757 |
|            countrySerbia:age55-74 years            |   0.8837623   |  1.1915183  |  0.7417111  | 0.4589642 |
|          countrySeychelles:age55-74 years          |  \-0.0223317  |  1.9031474  | \-0.0117341 | 0.9906472 |
|          countrySingapore:age55-74 years           |   0.7977516   |  0.5681339  |  1.4041611  | 0.1615220 |
|           countrySlovakia:age55-74 years           |   0.7847200   |  0.5499197  |  1.4269719  | 0.1548458 |
|           countrySlovenia:age55-74 years           |   1.6568868   |  0.7874332  |  2.1041618  | 0.0363712 |
|         countrySouth Africa:age55-74 years         |  \-0.0506367  |  1.2897292  | \-0.0392615 | 0.9687135 |
|            countrySpain:age55-74 years             |   0.9972848   |  1.4179906  |  0.7033085  | 0.4825233 |
|           countrySuriname:age55-74 years           |  \-0.4000531  |  1.0777434  | \-0.3711951 | 0.7108091 |
|            countrySweden:age55-74 years            |   0.7206091   |  0.8488542  |  0.8489198  | 0.3967446 |
|         countrySwitzerland:age55-74 years          |   1.4808338   |  0.8617102  |  1.7184823  | 0.0869567 |
|           countryThailand:age55-74 years           |   0.4226419   |  1.1952387  |  0.3536045  | 0.7239357 |
|     countryTrinidad and Tobago:age55-74 years      |  \-0.4133771  |  0.6151354  | \-0.6720099 | 0.5022030 |
|            countryTurkey:age55-74 years            |   0.1239564   |  1.3290717  |  0.0932654  | 0.9257680 |
|         countryTurkmenistan:age55-74 years         |  \-1.8209984  |  0.9209002  | \-1.9774112 | 0.0491025 |
|           countryUkraine:age55-74 years            |   0.1651789   |  1.1345994  |  0.1455834  | 0.8843685 |
|     countryUnited Arab Emirates:age55-74 years     |   0.1223489   |  0.9650219  |  0.1267836  | 0.8992144 |
|        countryUnited Kingdom:age55-74 years        |   0.7400083   |  1.2522834  |  0.5909272  | 0.5551074 |
|        countryUnited States:age55-74 years         |  \-2.6740269  |  3.0351815  | \-0.8810106 | 0.3791651 |
|           countryUruguay:age55-74 years            |   0.0833381   |  0.5344858  |  0.1559221  | 0.8762213 |
|          countryUzbekistan:age55-74 years          |  \-0.5625810  |  1.3667279  | \-0.4116262 | 0.6809689 |
|           countryArgentina:age75+ years            |   0.1983842   |  2.8596327  |  0.0693740  | 0.9447478 |
|            countryArmenia:age75+ years             |   2.7927564   |  2.6426311  |  1.0568090  | 0.2916271 |
|             countryAruba:age75+ years              |  \-0.2561206  |  3.4770422  | \-0.0736605 | 0.9413399 |
|           countryAustralia:age75+ years            |   0.9879370   |  2.7162930  |  0.3637078  | 0.7163861 |
|            countryAustria:age75+ years             |   2.4289047   |  2.4788908  |  0.9798353  | 0.3281223 |
|            countryBahamas:age75+ years             |  \-0.2574981  |  2.9521911  | \-0.0872227 | 0.9305649 |
|            countryBahrain:age75+ years             |  \-0.9369716  |  4.2933508  | \-0.2182378 | 0.8274233 |
|            countryBarbados:age75+ years            |   0.2189375   |  2.9012416  |  0.0754634  | 0.9399069 |
|            countryBelarus:age75+ years             |   2.1501744   |  2.5026219  |  0.8591687  | 0.3910771 |
|            countryBelgium:age75+ years             |   2.1060366   |  2.5037999  |  0.8411361  | 0.4010820 |
|             countryBelize:age75+ years             |   5.1532942   |  9.3554901  |  0.5508310  | 0.5822454 |
|             countryBrazil:age75+ years             |   0.2808664   |  3.8861908  |  0.0722729  | 0.9424430 |
|            countryBulgaria:age75+ years            |   3.2410022   |  2.4696050  |  1.3123565  | 0.1906132 |
|             countryCanada:age75+ years             |   0.8238108   |  2.7308749  |  0.3016655  | 0.7631599 |
|             countryChile:age75+ years              |  \-2.5425415  |  2.7804863  | \-0.9144233 | 0.3613827 |
|            countryColombia:age75+ years            |  \-9.7980877  |  3.6361931  | \-2.6946004 | 0.0075289 |
|           countryCosta Rica:age75+ years           |  \-3.2343126  |  3.6251376  | \-0.8921903 | 0.3731558 |
|            countryCroatia:age75+ years             |   1.9810567   |  2.4476635  |  0.8093664  | 0.4190802 |
|              countryCuba:age75+ years              |   1.7581273   |  2.8420676  |  0.6186086  | 0.5367420 |
|             countryCyprus:age75+ years             |  \-1.6771071  |  2.8239041  | \-0.5938966 | 0.5531226 |
|         countryCzech Republic:age75+ years         |   2.2636731   |  2.4993531  |  0.9057036  | 0.3659718 |
|            countryDenmark:age75+ years             |   1.8762261   |  2.4639308  |  0.7614768  | 0.4470958 |
|            countryEcuador:age75+ years             |  \-3.6702540  |  4.4323301  | \-0.8280642 | 0.4084303 |
|          countryEl Salvador:age75+ years           | \-13.5471317  |  3.8837942  | \-3.4881178 | 0.0005753 |
|            countryEstonia:age75+ years             |   1.7164698   |  2.5100847  |  0.6838295  | 0.4947213 |
|            countryFinland:age75+ years             |   1.0144742   |  2.4526371  |  0.4136259  | 0.6795056 |
|             countryFrance:age75+ years             |   2.2786395   |  2.8332910  |  0.8042377  | 0.4220300 |
|            countryGeorgia:age75+ years             |   4.3390454   |  2.4533451  |  1.7686241  | 0.0781859 |
|            countryGermany:age75+ years             |   2.0435151   |  2.9524780  |  0.6921356  | 0.4894997 |
|             countryGreece:age75+ years             |   1.7976065   |  2.4979001  |  0.7196471  | 0.4724200 |
|            countryGrenada:age75+ years             |   0.2174901   |  3.2382613  |  0.0671626  | 0.9465064 |
|           countryGuatemala:age75+ years            | \-18.4200966  |  4.8140382  | \-3.8263296 | 0.0001647 |
|             countryGuyana:age75+ years             | \-13.6089612  |  4.2552188  | \-3.1981813 | 0.0015629 |
|            countryHungary:age75+ years             |   2.8622040   |  2.4951823  |  1.1470922  | 0.2524490 |
|            countryIceland:age75+ years             |  \-1.5257488  |  2.9638993  | \-0.5147775 | 0.6071670 |
|            countryIreland:age75+ years             |   0.1155125   |  2.5895577  |  0.0446071  | 0.9644564 |
|             countryIsrael:age75+ years             |   0.4368951   |  2.6705453  |  0.1635977  | 0.8701811 |
|             countryItaly:age75+ years              |   2.9759932   |  2.7944881  |  1.0649511  | 0.2879338 |
|            countryJamaica:age75+ years             |   1.4774949   |  3.3217328  |  0.4447964  | 0.6568548 |
|             countryJapan:age75+ years              |  \-0.2435120  |  4.0084920  | \-0.0607490 | 0.9516080 |
|           countryKazakhstan:age75+ years           |   0.5642683   |  2.7601987  |  0.2044303  | 0.8381849 |
|             countryKuwait:age75+ years             |   3.4213013   |  5.4583360  |  0.6268030  | 0.5313650 |
|           countryKyrgyzstan:age75+ years           |   0.6945962   |  2.9812486  |  0.2329884  | 0.8159626 |
|             countryLatvia:age75+ years             |   1.6121611   |  2.4615058  |  0.6549491  | 0.5131075 |
|           countryLithuania:age75+ years            |   1.9174545   |  2.4451914  |  0.7841736  | 0.4336866 |
|           countryLuxembourg:age75+ years           |   0.4426995   |  2.7296057  |  0.1621844  | 0.8712927 |
|            countryMaldives:age75+ years            |  \-1.4176048  |  4.7038515  | \-0.3013711 | 0.7633841 |
|             countryMalta:age75+ years              |  \-0.0607329  |  2.7681727  | \-0.0219397 | 0.9825137 |
|           countryMauritius:age75+ years            |  \-3.0950996  |  2.7173647  | \-1.1390078 | 0.2557989 |
|             countryMexico:age75+ years             | \-11.5660535  |  4.1232589  | \-2.8050758 | 0.0054291 |
|          countryNetherlands:age75+ years           |   2.4168528   |  2.5634529  |  0.9428115  | 0.3466949 |
|          countryNew Zealand:age75+ years           |  \-0.2860680  |  2.5963471  | \-0.1101810 | 0.9123550 |
|           countryNicaragua:age75+ years            | \-12.1356657  |  3.6379910  | \-3.3358152 | 0.0009808 |
|             countryNorway:age75+ years             |   0.7583899   |  2.4590294  |  0.3084103  | 0.7580291 |
|              countryOman:age75+ years              |   3.0140461   |  3.4856429  |  0.8647031  | 0.3880374 |
|             countryPanama:age75+ years             |  \-5.7331156  |  4.7335104  | \-1.2111763 | 0.2269807 |
|            countryParaguay:age75+ years            |  \-4.0282536  |  4.3719455  | \-0.9213870 | 0.3577439 |
|          countryPhilippines:age75+ years           |  \-2.0929317  |  3.6844315  | \-0.5680474 | 0.5705167 |
|             countryPoland:age75+ years             |   2.6392111   |  2.7214871  |  0.9697680  | 0.3331070 |
|            countryPortugal:age75+ years            |   2.5405686   |  2.4973957  |  1.0172872  | 0.3100082 |
|          countryPuerto Rico:age75+ years           |  \-0.5840752  |  2.5334486  | \-0.2305455 | 0.8178580 |
|             countryQatar:age75+ years              |  \-2.5310659  |  3.9534927  | \-0.6402101 | 0.5226271 |
|       countryRepublic of Korea:age75+ years        |   1.1912046   |  2.9357715  |  0.4057552  | 0.6852723 |
|            countryRomania:age75+ years             |   2.6120060   |  2.6242592  |  0.9953308  | 0.3205455 |
|       countryRussian Federation:age75+ years       |   0.8272206   |  3.2098786  |  0.2577109  | 0.7968438 |
|          countrySaint Lucia:age75+ years           |  \-0.4157950  |  3.4789273  | \-0.1195182 | 0.9049616 |
|  countrySaint Vincent and Grenadines:age75+ years  |   0.4307338   |  3.6437306  |  0.1182123  | 0.9059951 |
|             countrySerbia:age75+ years             |   3.5942236   |  2.4737073  |  1.4529705  | 0.1474961 |
|           countrySeychelles:age75+ years           |  \-0.1692569  |  3.3940280  | \-0.0498690 | 0.9602669 |
|           countrySingapore:age75+ years            |   1.0197006   |  2.6552961  |  0.3840252  | 0.7012888 |
|            countrySlovakia:age75+ years            |   2.1194733   |  2.4735027  |  0.8568712  | 0.3923433 |
|            countrySlovenia:age75+ years            |   2.4066334   |  2.4784433  |  0.9710262  | 0.3324813 |
|          countrySouth Africa:age75+ years          |   0.8990227   |  3.1785423  |  0.2828412  | 0.7775345 |
|             countrySpain:age75+ years              |   3.3060323   |  2.7037348  |  1.2227650  | 0.2225792 |
|            countrySuriname:age75+ years            |  \-0.3323766  |  3.4208261  | \-0.0971627 | 0.9226757 |
|             countrySweden:age75+ years             |   1.2624849   |  2.4966832  |  0.5056648  | 0.6135411 |
|          countrySwitzerland:age75+ years           |   2.2436561   |  2.4696297  |  0.9084990  | 0.3644966 |
|            countryThailand:age75+ years            |   0.3024522   |  3.2122932  |  0.0941546  | 0.9250624 |
|      countryTrinidad and Tobago:age75+ years       |  \-4.3679945  |  2.7475547  | \-1.5897753 | 0.1131594 |
|             countryTurkey:age75+ years             |   0.6798468   |  3.3406784  |  0.2035056  | 0.8389068 |
|          countryTurkmenistan:age75+ years          |  \-5.1964306  |  2.9965433  | \-1.7341416 | 0.0841356 |
|            countryUkraine:age75+ years             |   2.3402308   |  2.7605886  |  0.8477289  | 0.3974064 |
|      countryUnited Arab Emirates:age75+ years      |  \-0.1756043  |  3.7008327  | \-0.0474499 | 0.9621928 |
|         countryUnited Kingdom:age75+ years         |   1.5309621   |  2.8108818  |  0.5446554  | 0.5864799 |
|         countryUnited States:age75+ years          |   5.4959525   |  5.1388561  |  1.0694895  | 0.2858890 |
|            countryUruguay:age75+ years             |   0.9252148   |  2.4613944  |  0.3758905  | 0.7073196 |
|           countryUzbekistan:age75+ years           |  \-1.1540286  |  3.2806458  | \-0.3517687 | 0.7253104 |
|           countryArgentina:suicides\_no            |  \-0.0806750  |  0.0323377  | \-2.4947681 | 0.0132554 |
|            countryArmenia:suicides\_no             |  \-0.0614051  |  0.0650869  | \-0.9434330 | 0.3463776 |
|             countryAruba:suicides\_no              |   0.3809003   |  0.1131858  |  3.3652660  | 0.0008860 |
|           countryAustralia:suicides\_no            |  \-0.0815896  |  0.0322955  | \-2.5263426 | 0.0121490 |
|            countryAustria:suicides\_no             |  \-0.0815214  |  0.0323018  | \-2.5237420 | 0.0122369 |
|            countryBahamas:suicides\_no             |   0.3747032   |  0.1804012  |  2.0770550  | 0.0388261 |
|            countryBahrain:suicides\_no             |   0.1951997   |  0.1223331  |  1.5956418  | 0.1118423 |
|            countryBarbados:suicides\_no            |   0.4363275   |  0.1449441  |  3.0103149  | 0.0028792 |
|            countryBelarus:suicides\_no             |  \-0.0824125  |  0.0322901  | \-2.5522504 | 0.0113034 |
|            countryBelgium:suicides\_no             |  \-0.0828221  |  0.0323061  | \-2.5636700 | 0.0109477 |
|             countryBelize:suicides\_no             |   0.2478437   |  0.1171167  |  2.1162111  | 0.0353235 |
|             countryBrazil:suicides\_no             |  \-0.0810642  |  0.0323221  | \-2.5080091 | 0.0127810 |
|            countryBulgaria:suicides\_no            |  \-0.0816292  |  0.0323312  | \-2.5247805 | 0.0122017 |
|             countryCanada:suicides\_no             |  \-0.0816463  |  0.0323012  | \-2.5276546 | 0.0121048 |
|             countryChile:suicides\_no              |  \-0.0809091  |  0.0323182  | \-2.5035163 | 0.0129402 |
|            countryColombia:suicides\_no            |  \-0.0796057  |  0.0323178  | \-2.4632134 | 0.0144498 |
|           countryCosta Rica:suicides\_no           |  \-0.0831143  |  0.0326457  | \-2.5459478 | 0.0115041 |
|            countryCroatia:suicides\_no             |  \-0.0771199  |  0.0323297  | \-2.3854207 | 0.0178112 |
|              countryCuba:suicides\_no              |  \-0.0806610  |  0.0322791  | \-2.4988591 | 0.0131072 |
|             countryCyprus:suicides\_no             |   0.0756841   |  0.0709981  |  1.0660018  | 0.2874595 |
|         countryCzech Republic:suicides\_no         |  \-0.0817259  |  0.0322831  | \-2.5315403 | 0.0119750 |
|            countryDenmark:suicides\_no             |  \-0.0775162  |  0.0325010  | \-2.3850398 | 0.0178292 |
|            countryEcuador:suicides\_no             |  \-0.0768997  |  0.0325154  | \-2.3650252 | 0.0187994 |
|          countryEl Salvador:suicides\_no           |  \-0.0723225  |  0.0329293  | \-2.1962973 | 0.0289968 |
|            countryEstonia:suicides\_no             |  \-0.0613153  |  0.0331326  | \-1.8506053 | 0.0654156 |
|            countryFinland:suicides\_no             |  \-0.0819916  |  0.0323535  | \-2.5342434 | 0.0118853 |
|             countryFrance:suicides\_no             |  \-0.0816542  |  0.0323133  | \-2.5269561 | 0.0121283 |
|            countryGeorgia:suicides\_no             |  \-0.0611992  |  0.0354936  | \-1.7242288 | 0.0859126 |
|            countryGermany:suicides\_no             |  \-0.0817679  |  0.0323151  | \-2.5303293 | 0.0120153 |
|             countryGreece:suicides\_no             |  \-0.0693623  |  0.0324123  | \-2.1400018 | 0.0333307 |
|           countryGuatemala:suicides\_no            |  \-0.0741577  |  0.0328972  | \-2.2542224 | 0.0250555 |
|             countryGuyana:suicides\_no             |  \-0.0516541  |  0.0327609  | \-1.5766991 | 0.1161395 |
|            countryHungary:suicides\_no             |  \-0.0821726  |  0.0322915  | \-2.5447143 | 0.0115438 |
|            countryIceland:suicides\_no             |  \-0.0521563  |  0.0895771  | \-0.5822508 | 0.5609267 |
|            countryIreland:suicides\_no             |  \-0.0744752  |  0.0324270  | \-2.2967066 | 0.0224696 |
|             countryIsrael:suicides\_no             |  \-0.0679414  |  0.0325827  | \-2.0852013 | 0.0380739 |
|             countryItaly:suicides\_no              |  \-0.0823402  |  0.0323050  | \-2.5488350 | 0.0114118 |
|            countryJamaica:suicides\_no             |   0.7577259   |  0.3310008  |  2.2891967  | 0.0229090 |
|             countryJapan:suicides\_no              |  \-0.0815499  |  0.0323201  | \-2.5231954 | 0.0122554 |
|           countryKazakhstan:suicides\_no           |  \-0.0815244  |  0.0323064  | \-2.5234741 | 0.0122460 |
|             countryKuwait:suicides\_no             |  \-0.0132800  |  0.1565160  | \-0.0848474 | 0.9324511 |
|           countryKyrgyzstan:suicides\_no           |  \-0.0736321  |  0.0325346  | \-2.2631932 | 0.0244889 |
|             countryLatvia:suicides\_no             |  \-0.0736641  |  0.0323625  | \-2.2762138 | 0.0236863 |
|           countryLithuania:suicides\_no            |  \-0.0798935  |  0.0322825  | \-2.4748206 | 0.0139998 |
|           countryLuxembourg:suicides\_no           |  \-0.0332912  |  0.0400820  | \-0.8305763 | 0.4070119 |
|            countryMaldives:suicides\_no            |   0.2512396   |  0.4315717  |  0.5821503  | 0.5609943 |
|             countryMalta:suicides\_no              |   0.0622954   |  0.0421696  |  1.4772606  | 0.1408745 |
|           countryMauritius:suicides\_no            |  \-0.0225363  |  0.0414269  | \-0.5440027 | 0.5869283 |
|             countryMexico:suicides\_no             |  \-0.0806564  |  0.0323346  | \-2.4944329 | 0.0132676 |
|          countryNetherlands:suicides\_no           |  \-0.0828607  |  0.0323072  | \-2.5647771 | 0.0109138 |
|          countryNew Zealand:suicides\_no           |  \-0.0752128  |  0.0324916  | \-2.3148386 | 0.0214390 |
|           countryNicaragua:suicides\_no            |  \-0.0727249  |  0.0327725  | \-2.2190849 | 0.0273865 |
|             countryNorway:suicides\_no             |  \-0.0867091  |  0.0330521  | \-2.6234067 | 0.0092451 |
|              countryOman:suicides\_no              |   0.1266821   |  0.1184074  |  1.0698828  | 0.2857123 |
|             countryPanama:suicides\_no             |  \-0.0164439  |  0.0339479  | \-0.4843853 | 0.6285399 |
|            countryParaguay:suicides\_no            |  \-0.0488642  |  0.0358400  | \-1.3633986 | 0.1739933 |
|          countryPhilippines:suicides\_no           |  \-0.0804913  |  0.0323325  | \-2.4894866 | 0.0134490 |
|             countryPoland:suicides\_no             |  \-0.0822240  |  0.0323052  | \-2.5452245 | 0.0115274 |
|            countryPortugal:suicides\_no            |  \-0.0779051  |  0.0323268  | \-2.4099220 | 0.0166849 |
|          countryPuerto Rico:suicides\_no           |  \-0.0774960  |  0.0325953  | \-2.3775207 | 0.0181884 |
|             countryQatar:suicides\_no              |   0.0923382   |  0.0558173  |  1.6542945  | 0.0993327 |
|       countryRepublic of Korea:suicides\_no        |  \-0.0818510  |  0.0323063  | \-2.5335892 | 0.0119070 |
|            countryRomania:suicides\_no             |  \-0.0819025  |  0.0322966  | \-2.5359499 | 0.0118291 |
|       countryRussian Federation:suicides\_no       |  \-0.0817782  |  0.0323211  | \-2.5301823 | 0.0120202 |
|          countrySaint Lucia:suicides\_no           |   0.5677165   |  0.1691411  |  3.3564668  | 0.0009134 |
|  countrySaint Vincent and Grenadines:suicides\_no  |   0.2607689   |  0.1157039  |  2.2537606  | 0.0250850 |
|             countrySerbia:suicides\_no             |  \-0.0804714  |  0.0323022  | \-2.4912027 | 0.0133858 |
|           countrySeychelles:suicides\_no           |   0.3297920   |  0.1137836  |  2.8984142  | 0.0040863 |
|           countrySingapore:suicides\_no            |  \-0.0655943  |  0.0329139  | \-1.9929022 | 0.0473681 |
|            countrySlovakia:suicides\_no            |  \-0.0805290  |  0.0323075  | \-2.4925807 | 0.0133353 |
|            countrySlovenia:suicides\_no            |  \-0.0881482  |  0.0324508  | \-2.7163634 | 0.0070649 |
|          countrySouth Africa:suicides\_no          |  \-0.0740758  |  0.0330389  | \-2.2420814 | 0.0258406 |
|             countrySpain:suicides\_no              |  \-0.0824339  |  0.0323005  | \-2.5520943 | 0.0113084 |
|            countrySuriname:suicides\_no            |  \-0.0499075  |  0.0363821  | \-1.3717593 | 0.1713781 |
|             countrySweden:suicides\_no             |  \-0.0785716  |  0.0323072  | \-2.4320194 | 0.0157235 |
|          countrySwitzerland:suicides\_no           |  \-0.0842400  |  0.0323145  | \-2.6068811 | 0.0096906 |
|            countryThailand:suicides\_no            |  \-0.0811590  |  0.0323028  | \-2.5124446 | 0.0126254 |
|      countryTrinidad and Tobago:suicides\_no       |  \-0.0465156  |  0.0342746  | \-1.3571466 | 0.1759685 |
|             countryTurkey:suicides\_no             |  \-0.0784300  |  0.0323222  | \-2.4265051 | 0.0159587 |
|          countryTurkmenistan:suicides\_no          |  \-0.0363559  |  0.0354174  | \-1.0264983 | 0.3056569 |
|            countryUkraine:suicides\_no             |  \-0.0820573  |  0.0323094  | \-2.5397342 | 0.0117051 |
|      countryUnited Arab Emirates:suicides\_no      |  \-0.0258759  |  0.0432996  | \-0.5976015 | 0.5506512 |
|         countryUnited Kingdom:suicides\_no         |  \-0.0808368  |  0.0323059  | \-2.5022326 | 0.0129861 |
|         countryUnited States:suicides\_no          |  \-0.0810488  |  0.0323324  | \-2.5067378 | 0.0128258 |
|            countryUruguay:suicides\_no             |  \-0.0605405  |  0.0329180  | \-1.8391275 | 0.0670919 |
|           countryUzbekistan:suicides\_no           |  \-0.0784408  |  0.0323290  | \-2.4263317 | 0.0159661 |
|            countryArgentina:population             | \-11.3844542  | 20.9861377  | \-0.5424750 | 0.5879785 |
|             countryArmenia:population              |  19.3226261   | 20.3297984  |  0.9504583  | 0.3428048 |
|              countryAruba:population               |  10.8789136   | 19.0093820  |  0.5722918  | 0.5676427 |
|            countryAustralia:population             |  \-3.8353159  | 24.2020220  | \-0.1584709 | 0.8742147 |
|             countryAustria:population              |  11.8624250   | 20.1051681  |  0.5900187  | 0.5557153 |
|             countryBahamas:population              |   5.2455947   | 18.8725088  |  0.2779490  | 0.7812831 |
|             countryBahrain:population              |   1.7728663   | 20.8191328  |  0.0851556  | 0.9322064 |
|             countryBarbados:population             |   9.8456350   | 19.2820664  |  0.5106110  | 0.6100777 |
|             countryBelarus:population              |  14.0626225   | 18.6542499  |  0.7538562  | 0.4516507 |
|             countryBelgium:population              |   9.0242132   | 20.8542022  |  0.4327288  | 0.6655879 |
|              countryBelize:population              |  24.7990594   | 34.5936035  |  0.7168683  | 0.4741299 |
|              countryBrazil:population              | \-11.7277785  | 26.9319945  | \-0.4354590 | 0.6636081 |
|             countryBulgaria:population             |  19.4490706   | 20.5788447  |  0.9451002  | 0.3455276 |
|              countryCanada:population              |  \-8.5530228  | 23.6683385  | \-0.3613698 | 0.7181307 |
|              countryChile:population               | \-24.4173410  | 20.7456433  | \-1.1769864 | 0.2403293 |
|             countryColombia:population             | \-66.6375072  | 24.1488599  | \-2.7594473 | 0.0062218 |
|            countryCosta Rica:population            | \-12.5655922  | 25.2013539  | \-0.4986078 | 0.6184976 |
|             countryCroatia:population              |   9.1445680   | 19.1973296  |  0.4763458  | 0.6342474 |
|               countryCuba:population               |  \-1.1488078  | 27.7570324  | \-0.0413880 | 0.9670199 |
|              countryCyprus:population              | \-11.7457469  | 22.2276490  | \-0.5284296 | 0.5976738 |
|          countryCzech Republic:population          |  12.3886927   | 19.4663729  |  0.6364151  | 0.5250929 |
|             countryDenmark:population              |   1.1903576   | 20.7248231  |  0.0574363  | 0.9542439 |
|             countryEcuador:population              | \-21.2234282  | 30.3065283  | \-0.7002923 | 0.4844012 |
|           countryEl Salvador:population            | \-79.4434382  | 25.0125600  | \-3.1761418 | 0.0016815 |
|             countryEstonia:population              |  13.2551929   | 18.4474670  |  0.7185373  | 0.4731025 |
|             countryFinland:population              |   9.0204925   | 19.6274079  |  0.4595865  | 0.6462156 |
|              countryFrance:population              |  39.6907916   | 41.8441226  |  0.9485392  | 0.3437784 |
|             countryGeorgia:population              |  34.6130770   | 18.9899573  |  1.8227043  | 0.0695523 |
|             countryGermany:population              |  34.4194788   | 34.8190730  |  0.9885237  | 0.3238597 |
|              countryGreece:population              | \-11.7849606  | 23.8169256  | \-0.4948145 | 0.6211691 |
|             countryGrenada:population              |  10.1873891   | 18.6210401  |  0.5470902  | 0.5848087 |
|            countryGuatemala:population             | \-87.5684490  | 27.3186101  | \-3.2054504 | 0.0015255 |
|              countryGuyana:population              | \-42.8918910  | 22.0769743  | \-1.9428338 | 0.0531680 |
|             countryHungary:population              |  13.9155698   | 19.3436102  |  0.7193885  | 0.4725790 |
|             countryIceland:population              |  \-3.7500372  | 21.3694980  | \-0.1754855 | 0.8608414 |
|             countryIreland:population              |   3.8838419   | 21.7931459  |  0.1782139  | 0.8587005 |
|              countryIsrael:population              |  \-6.1689607  | 21.5002447  | \-0.2869251 | 0.7744092 |
|              countryItaly:population               |  25.5642231   | 28.0438856  |  0.9115792  | 0.3628755 |
|             countryJamaica:population              |   6.9091034   | 24.7320686  |  0.2793581  | 0.7802029 |
|              countryJapan:population               | \-11.4767496  | 37.3854797  | \-0.3069841 | 0.7591130 |
|            countryKazakhstan:population            |   2.3992166   | 19.1803729  |  0.1250871  | 0.9005560 |
|              countryKuwait:population              |  15.4431505   | 23.6838323  |  0.6520545  | 0.5149698 |
|            countryKyrgyzstan:population            |   6.9094619   | 19.8930573  |  0.3473303  | 0.7286378 |
|              countryLatvia:population              |  12.6218569   | 18.4753215  |  0.6831739  | 0.4951347 |
|            countryLithuania:population             |  15.7523584   | 18.6323768  |  0.8454294  | 0.3986861 |
|            countryLuxembourg:population            |   1.5792115   | 19.0590832  |  0.0828587  | 0.9340307 |
|             countryMaldives:population             |   1.8986919   | 22.9373690  |  0.0827772  | 0.9340954 |
|              countryMalta:population               |   4.6607180   | 19.1721267  |  0.2430986  | 0.8081299 |
|            countryMauritius:population             | \-12.5215881  | 19.3965374  | \-0.6455579 | 0.5191625 |
|              countryMexico:population              | \-91.4497322  | 28.9033256  | \-3.1639865 | 0.0017505 |
|           countryNetherlands:population            |  16.8225841   | 20.8354681  |  0.8074013  | 0.4202090 |
|           countryNew Zealand:population            |  \-4.0266265  | 22.7129290  | \-0.1772835 | 0.8594305 |
|            countryNicaragua:population             | \-52.3500862  | 22.3862368  | \-2.3384943 | 0.0201568 |
|              countryNorway:population              |   4.1516282   | 20.4328038  |  0.2031845  | 0.8391575 |
|               countryOman:population               |  12.7287179   | 20.1107560  |  0.6329308  | 0.5273620 |
|              countryPanama:population              | \-36.9332445  | 31.4029514  | \-1.1761074 | 0.2406797 |
|             countryParaguay:population             | \-20.2531488  | 26.6815421  | \-0.7590697 | 0.4485317 |
|           countryPhilippines:population            | \-12.3458596  | 22.1431110  | \-0.5575486 | 0.5776556 |
|              countryPoland:population              |  15.2375422   | 20.1967541  |  0.7544550  | 0.4512918 |
|             countryPortugal:population             |  13.1140085   | 23.9304499  |  0.5480051  | 0.5841813 |
|           countryPuerto Rico:population            | \-15.2555160  | 20.7231455  | \-0.7361583 | 0.4623301 |
|              countryQatar:population               |  \-0.0522879  | 19.2398774  | \-0.0027177 | 0.9978338 |
|        countryRepublic of Korea:population         |  11.9715823   | 21.9424285  |  0.5455906  | 0.5858378 |
|             countryRomania:population              |  16.3841920   | 20.6780172  |  0.7923483  | 0.4289149 |
|        countryRussian Federation:population        |  \-5.2555340  | 26.0225063  | \-0.2019611 | 0.8401127 |
|           countrySaint Lucia:population            |   6.0527976   | 21.1598038  |  0.2860517  | 0.7750773 |
|   countrySaint Vincent and Grenadines:population   |  11.5243728   | 19.5300602  |  0.5900838  | 0.5556717 |
|              countrySerbia:population              |  21.2472702   | 22.3734262  |  0.9496655  | 0.3432068 |
|            countrySeychelles:population            |  10.1292831   | 18.4406027  |  0.5492924  | 0.5832990 |
|            countrySingapore:population             |   0.1795636   | 20.5998100  |  0.0087168  | 0.9930521 |
|             countrySlovakia:population             |  12.6424263   | 18.9455367  |  0.6673037  | 0.5051986 |
|             countrySlovenia:population             |  12.6679803   | 18.7545601  |  0.6754613  | 0.5000120 |
|           countrySouth Africa:population           |   2.8612643   | 19.8401330  |  0.1442160  | 0.8854470 |
|              countrySpain:population               |  21.5877444   | 26.9770312  |  0.8002268  | 0.4243453 |
|             countrySuriname:population             |   6.1756747   | 20.4556963  |  0.3019049  | 0.7629776 |
|              countrySweden:population              |  \-3.5109826  | 21.2658841  | \-0.1650993 | 0.8690003 |
|           countrySwitzerland:population            |   6.4585264   | 20.5212811  |  0.3147234  | 0.7532363 |
|             countryThailand:population             |  \-8.2856543  | 23.3269753  | \-0.3551963 | 0.7227445 |
|       countryTrinidad and Tobago:population        | \-17.3656819  | 19.6691066  | \-0.8828912 | 0.3781500 |
|              countryTurkey:population              |  \-5.6474053  | 23.3357558  | \-0.2420065 | 0.8089751 |
|           countryTurkmenistan:population           | \-19.0483254  | 19.8783748  | \-0.9582436 | 0.3388732 |
|             countryUkraine:population              |  12.1586402   | 19.8657673  |  0.6120398  | 0.5410721 |
|       countryUnited Arab Emirates:population       |   4.6880853   | 19.9450876  |  0.2350496  | 0.8143642 |
|          countryUnited Kingdom:population          |  \-8.5752141  | 23.5215399  | \-0.3645686 | 0.7157442 |
|          countryUnited States:population           |  71.8620307   | 115.7953560 |  0.6205951  | 0.5354360 |
|             countryUruguay:population              |   0.8735476   | 19.2125897  |  0.0454675  | 0.9637713 |
|            countryUzbekistan:population            |  \-3.0042840  | 20.7035416  | \-0.1451097 | 0.8847422 |
|               sexmale:age25-34 years               |   0.1429618   |  0.0710517  |  2.0120816  | 0.0452927 |
|               sexmale:age35-54 years               |  \-0.2784285  |  0.0992281  | \-2.8059434 | 0.0054150 |
|               sexmale:age5-14 years                |   0.0269182   |  0.2144861  |  0.1255008  | 0.9002288 |
|               sexmale:age55-74 years               |  \-0.0116397  |  0.0984611  | \-0.1182166 | 0.9059917 |
|                sexmale:age75+ years                |  \-0.0908720  |  0.1919529  | \-0.4734079 | 0.6363387 |
|                sexmale:suicides\_no                |  \-0.0012253  |  0.0004074  | \-3.0073040 | 0.0029068 |
|            age25-34 years:suicides\_no             |  \-0.0002652  |  0.0001471  | \-1.8022803 | 0.0727155 |
|            age35-54 years:suicides\_no             |  \-0.0001016  |  0.0002157  | \-0.4709192 | 0.6381124 |
|             age5-14 years:suicides\_no             |   0.0223920   |  0.0098830  |  2.2657072  | 0.0243321 |
|            age55-74 years:suicides\_no             |  \-0.0001411  |  0.0002158  | \-0.6538600 | 0.5138079 |
|             age75+ years:suicides\_no              |   0.0007183   |  0.0014471  |  0.4963824  | 0.6200643 |
|             age25-34 years:population              | \-13.7050303  |  5.1477026  | \-2.6623586 | 0.0082670 |
|             age35-54 years:population              |  \-2.9053588  |  5.2483811  | \-0.5535724 | 0.5803703 |
|              age5-14 years:population              | \-140.8053227 | 50.6702203  | \-2.7788575 | 0.0058726 |
|             age55-74 years:population              |  \-1.2126662  |  5.2990584  | \-0.2288456 | 0.8191775 |
|              age75+ years:population               |  \-5.1242967  |  6.5779995  | \-0.7790053 | 0.4367193 |
|              suicides\_no:population               |  \-0.0078987  |  0.0045387  | \-1.7403042 | 0.0830460 |

### Section 4 - References

  - \[1\] <https://www.cdc.gov/nchs/fastats/adolescent-health.htm>
  - \[2\] <http://hdr.undp.org/en/content/human-development-index-hdi>
    Your project goes here\! Before you submit, make sure your chunks
    are turned off with `echo = FALSE`.

You can add sections as you see fit. At a minimum, you should have the
following sections:

  - Section 1: Introduction (includes introduction and exploratory data
    analysis)
  - Section 2: Regression Analysis (includes the final model and
    discussion of assumptions)
  - Section 3: Discussion and Limitations
  - Section 4: Conclusion
  - Section 5: Additional Work
