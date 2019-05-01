Stat210 Final Project
================
CamFam
May 1st, 2019

    ## ── Attaching packages ───────────────────────────────────────────────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
    ## ✔ tibble  2.0.0     ✔ dplyr   0.7.8
    ## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
    ## ✔ readr   1.3.1     ✔ forcats 0.3.0

    ## ── Conflicts ──────────────────────────────────────────────────────── tidyverse_conflicts() ──
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
    ## ── Variable type:character ───────────────────────────────────────────────────────────────────
    ##      variable missing complete    n min max empty n_unique
    ##           age       0     1056 1056   9  11     0        6
    ##       country       0     1056 1056   4  28     0       88
    ##  country-year       0     1056 1056   8  32     0       88
    ##    generation       0     1056 1056   6  12     0        4
    ##           sex       0     1056 1056   4   6     0        2
    ## 
    ## ── Variable type:numeric ─────────────────────────────────────────────────────────────────────
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
    ## ── Variable type:character ───────────────────────────────────────────────────────────────────
    ##      variable missing complete    n min max empty n_unique
    ##  country-year       0     1056 1056   8  32     0       88
    ## 
    ## ── Variable type:factor ──────────────────────────────────────────────────────────────────────
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
    ## ── Variable type:numeric ─────────────────────────────────────────────────────────────────────
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

![](project-writeup_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

    ## 
    ## Skim summary statistics
    ## 
    ## ── Variable type:numeric ─────────────────────────────────────────────────────────────────────
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
suicides per 100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

From log transforming suicides/100k pop, we can already see that the
extreme outliers have disappeared, and the histogram seems to be
approximately normally distributed.

Note: suicides/100k pop is now log transformed for all plots below.

We will now look at an overview of the relationships that suicides/100k
pop has with each of the quantitative predictor variables (age, sex,
country, year, HDI, gdp\_for\_year, gdp\_per\_capita, and generation),
as well as the relationships these variables have with each other.

![](project-writeup_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

In our data set, all ages have the same number of counts.
![](project-writeup_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

In our data set, male and female have the same count

![](project-writeup_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

In our data set, we see that most of the countries are from the Americas
and Europe.

![](project-writeup_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

From this bar graph, we notice that most of our data set seems high in
regions from Western Asia, Southern Europe, South America, Northern
Europe, and the Caribbean.

![](project-writeup_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

By examining these boxplots, we can tell that as age increases, suicide
rate tends to increase in general.

![](project-writeup_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

In general, each continent has a similar average number of suicides,
with Europe having much more outliers with fewer suicides than the
others.

![](project-writeup_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

The average number of suicides/100k for each region is around 2. We see
Souther Africa as a key outlier with far less suicides and Eastern
Africa with far more suicides than the average.

![](project-writeup_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

From this boxplot, we notice that males have a higher suicide rate/100k
people than females. However, there are many outliers in this data set
so we must explore further.

![](project-writeup_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

From this boxplot, we see that the average suicide rate/100k people is
varied among generation. More specifically, we notice that Generation Z
and Millienials have lower rates than the average value of around 2.

![](project-writeup_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

We will have to log transform population. In addition, we will mean
center it so it is easier to interpret.

![](project-writeup_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

We see that this plot has is skewed left and has a unimodal
distribution.

We will mean center HDI so it makes it easier to interpret.

![](project-writeup_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

The HDI does not have a set distribution. Rather, it is quite sparse.

![](project-writeup_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

Because this is skewed greatly, a log transformation of gdp is needed.
We will also mean center this variable.

![](project-writeup_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

Log transforming the data set, we notice that the distribution of GDPs
of countries has a near-bimodal distribution.

![](project-writeup_files/figure-gfm/unnamed-chunk-26-1.png)<!-- -->

Like GDP, we will need to log transform this data set. We will also mean
center this.

![](project-writeup_files/figure-gfm/unnamed-chunk-27-1.png)<!-- -->

Like the GDP of the country, the GDP Per Capita has a non-normal
distribution. Rather, it is skewed to the left and is bimodal. Since
these variables are so similar, there could be mulitcollinearity between
the two.

![](project-writeup_files/figure-gfm/unnamed-chunk-28-1.png)<!-- -->

We do not see a correlation between HDI and Suicides/100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

We do not see a correlation between GDP and Suicides/100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

We do not see a correlation between GDP per capita and Suicides/100k.

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

We are very concerned about multicollinearity between all of these
variables, so we will look into VIF.

We plan to do a multiple linear regression because suicides/100k pop is
a quantitative variable (there are no levels to it, since it is a
continuous variable).

## Section 3. Data

We are not going to include country in this model as there are over 188
countries and we can already account for much of this variability based
off of region.

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

### Testing of Interesting Interactions

For the interaction effects, we will look into the interaction of each
quantitative variable with each qualitative variable. We will also look
at a select few qualitative variables with one
another.

![](project-writeup_files/figure-gfm/unnamed-chunk-33-1.png)<!-- -->![](project-writeup_files/figure-gfm/unnamed-chunk-33-2.png)<!-- -->![](project-writeup_files/figure-gfm/unnamed-chunk-33-3.png)<!-- -->![](project-writeup_files/figure-gfm/unnamed-chunk-33-4.png)<!-- -->

There seems to be a significant interaction effect between all of the
quantitative variables that were selected in backwards selection
(population, GDP per capita, GDP for year, and HDI) and region because
the lines are not relatively parallel, as the slopes of the all of the
lines in each graph look to be quite different. Thus, we will use Nested
F Tests to formally test if any of these interactions are significant.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + region * HDI
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)    
    ## 1   1030 664.61                                 
    ## 2   1018 632.15 12    32.453 4.3552 8.54e-07 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.4591 and the p-value is 0.003639, which is small.
We can conclude that the interaction effect of HDI and region is a
significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + region * population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1015 609.10 15    55.505 6.1662 1.472e-12 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 4.3923 and the p-value is 4.641e-08, which is very
low. We can conclude that the interaction effect of region and
population is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + region * `gdp_for_year ($)`
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1017 628.99 13    35.613 4.4294 2.374e-07 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.216 and the p-value is 0.007552 , which is below
.05. We can conclude that the interaction effect of region and GDP for
year is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + region * `gdp_per_capita ($)`
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1030 664.61                                  
    ## 2   1017 639.27 13    25.334 3.1002 0.0001524 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 1.2491 and the p-value is 0.2387, which is above .05.
Contrary to what we first thought, we can conclude that the interaction
effect of region and gdp per capita is not a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + age + population + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ sex + age + population + HDI + `gdp_for_year ($)` + 
    ##     `gdp_per_capita ($)` + region + sex * HDI
    ##   Res.Df    RSS Df Sum of Sq      F Pr(>F)
    ## 1   1030 664.61                           
    ## 2   1029 664.37  1   0.23833 0.3691 0.5436

We see that sex will not have a significant effect on any interactions.
We will not be looking at the interaction effects between sex and other
variables.

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

The F statistic is 13.857 and the p-value is 4.027e-13, which is smaller
than 0.05. We can conclude that the interaction effect of age and HDI is
significant predictor.

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

The F statistic is 3.0279 and the p-value is 0.01015, which is smaller
than 0.05. We can conclude that the interaction effect of age and gdp
per capita is a significant predictor.

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

The F statistic is 27.466 and the p-value is 2.2e-16, which is smaller
than 0.05. We can conclude that the interaction effect of age and gdp
for year is significant predictor.

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

The F statistic is 23.793 and the p-value is 2.2e-16, which is smaller
than 0.05. We can conclude that the interaction effect of age and gdp
per capita is a significant predictor.

From this, analysis, we will include 7 interaction effects in our new
model

|                    term                     |   estimate   | std.error  |  statistic  |  p.value  |
| :-----------------------------------------: | :----------: | :--------: | :---------: | :-------: |
|                 (Intercept)                 |  2.5199093   | 7.9046711  |  0.3187874  | 0.7499557 |
|                   sexmale                   |  1.0366314   | 0.0416535  | 24.8870099  | 0.0000000 |
|               age25-34 years                |  15.9584239  | 9.2728953  |  1.7209753  | 0.0855709 |
|               age35-54 years                |  1.8670545   | 10.5753940 |  0.1765470  | 0.8599007 |
|                age5-14 years                |  20.9964213  | 9.4840301  |  2.2138712  | 0.0270672 |
|               age55-74 years                |  2.5874080   | 8.6162296  |  0.3002947  | 0.7640161 |
|                age75+ years                 |  13.8415938  | 7.9241816  |  1.7467537  | 0.0809933 |
|                 population                  |  0.4260107   | 2.9634448  |  0.1437552  | 0.8857233 |
|                     HDI                     | \-21.2343535 | 25.8760051 | \-0.8206195 | 0.4120626 |
|             `gdp_for_year ($)`              |  0.0173486   | 0.2649987  |  0.0654667  | 0.9478158 |
|            `gdp_per_capita ($)`             |  0.2966462   | 0.6165608  |  0.4811304  | 0.6305312 |
|               regionCaribbean               | \-2.5301383  | 2.5003136  | \-1.0119284 | 0.3118221 |
|            regionCentral America            | \-2.8510033  | 2.5000954  | \-1.1403578 | 0.2544159 |
|             regionCentral Asia              | \-0.4741630  | 2.5167399  | \-0.1884037 | 0.8505992 |
|            regionEastern Africa             | \-4.6153287  | 2.6322969  | \-1.7533466 | 0.0798552 |
|             regionEastern Asia              |  1.4758395   | 0.8509792  |  1.7342840  | 0.0831822 |
|            regionEastern Europe             | \-2.1334831  | 2.5062684  | \-0.8512588 | 0.3948336 |
|           regionNorthern America            | \-1.8160963  | 6.1183772  | \-0.2968265 | 0.7666619 |
|            regionNorthern Europe            | \-1.5592014  | 2.5133883  | \-0.6203584 | 0.5351661 |
|             regionSouth America             | \-1.5769908  | 2.4982817  | \-0.6312302 | 0.5280372 |
|          regionSouth-Eastern Asia           | \-3.7384365  | 2.5820779  | \-1.4478403 | 0.1479815 |
|            regionSouthern Africa            | \-7.0399931  | 6.2848695  | \-1.1201494 | 0.2629245 |
|             regionSouthern Asia             | \-4.5399118  | 4.6823311  | \-0.9695837 | 0.3324933 |
|            regionSouthern Europe            | \-2.5972177  | 2.4974147  | \-1.0399625 | 0.2986138 |
|             regionWestern Asia              | \-3.2628672  | 2.4967473  | \-1.3068472 | 0.1915712 |
|            regionWestern Europe             | \-1.2096246  | 2.9662786  | \-0.4077920 | 0.6835155 |
|             HDI:regionCaribbean             |  30.6319097  | 26.1112565 |  1.1731304  | 0.2410286 |
|          HDI:regionCentral America          |  28.1189251  | 26.1829169 |  1.0739417  | 0.2831132 |
|           HDI:regionCentral Asia            |  48.5437722  | 26.3251933 |  1.8440044  | 0.0654842 |
|          HDI:regionEastern Africa           | \-46.4758831 | 27.7448886 | \-1.6751151 | 0.0942307 |
|          HDI:regionEastern Europe           |  17.1884396  | 26.4418585 |  0.6500466  | 0.5158145 |
|         HDI:regionNorthern America          |  13.7593264  | 57.1696475 |  0.2406754  | 0.8098571 |
|          HDI:regionNorthern Europe          |  8.5400096   | 26.7660263 |  0.3190615  | 0.7497478 |
|           HDI:regionSouth America           |  15.4973642  | 25.9436039 |  0.5973482  | 0.5504129 |
|        HDI:regionSouth-Eastern Asia         |  19.7525334  | 19.9735295 |  0.9889355  | 0.3229388 |
|          HDI:regionSouthern Europe          |  22.8910983  | 26.1949093 |  0.8738758  | 0.3824000 |
|           HDI:regionWestern Asia            |  29.1020965  | 25.9735906 |  1.1204495  | 0.2627968 |
|          HDI:regionWestern Europe           |  7.8557090   | 22.4001193 |  0.3506994  | 0.7258892 |
|     `gdp_for_year ($)`:regionCaribbean      | \-0.3349923  | 0.1478963  | \-2.2650494 | 0.0237273 |
|  `gdp_for_year ($)`:regionCentral America   | \-0.1011988  | 0.1495226  | \-0.6768122 | 0.4986848 |
|    `gdp_for_year ($)`:regionCentral Asia    | \-0.4495542  | 0.2142800  | \-2.0979757 | 0.0361629 |
|    `gdp_for_year ($)`:regionEastern Asia    | \-0.3831628  | 0.4005241  | \-0.9566536 | 0.3389780 |
|   `gdp_for_year ($)`:regionEastern Europe   |  0.1395157   | 0.1574637  |  0.8860182  | 0.3758251 |
|  `gdp_for_year ($)`:regionNorthern Europe   | \-0.2227774  | 0.1488423  | \-1.4967347 | 0.1347843 |
|   `gdp_for_year ($)`:regionSouth America    | \-0.3887931  | 0.1442737  | \-2.6948304 | 0.0071629 |
| `gdp_for_year ($)`:regionSouth-Eastern Asia |  0.9425181   | 0.5213408  |  1.8078732  | 0.0709327 |
|  `gdp_for_year ($)`:regionSouthern Europe   | \-0.2046936  | 0.1469101  | \-1.3933262 | 0.1638371 |
|    `gdp_for_year ($)`:regionWestern Asia    | \-0.0094657  | 0.1502833  | \-0.0629858 | 0.9497906 |
|    `gdp_per_capita ($)`:regionCaribbean     |  0.1449404   | 0.5516732  |  0.2627288  | 0.7928149 |
| `gdp_per_capita ($)`:regionCentral America  | \-1.0923013  | 0.6995542  | \-1.5614248 | 0.1187464 |
|   `gdp_per_capita ($)`:regionCentral Asia   | \-0.9175886  | 0.5856206  | \-1.5668653 | 0.1174690 |
|  `gdp_per_capita ($)`:regionEastern Europe  | \-0.4036319  | 0.6647629  | \-0.6071817 | 0.5438710 |
| `gdp_per_capita ($)`:regionNorthern Europe  |  0.4096081   | 0.6600452  |  0.6205758  | 0.5350230 |
|  `gdp_per_capita ($)`:regionSouth America   |  1.0100262   | 0.6016985  |  1.6786251  | 0.0935439 |
| `gdp_per_capita ($)`:regionSouthern Europe  | \-0.2989290  | 0.6246232  | \-0.4785749 | 0.6323478 |
|   `gdp_per_capita ($)`:regionWestern Asia   | \-0.5832564  | 0.5619691  | \-1.0378798 | 0.2995820 |
|             age25-34 years:HDI              |  1.7942578   | 2.0339682  |  0.8821465  | 0.3779139 |
|             age35-54 years:HDI              |  6.9028518   | 2.0954559  |  3.2942004  | 0.0010224 |
|              age5-14 years:HDI              | \-5.2616333  | 2.0945989  | \-2.5120003 | 0.0121647 |
|             age55-74 years:HDI              |  7.5700050   | 2.2512405  |  3.3625928  | 0.0008020 |
|              age75+ years:HDI               |  8.1133422   | 2.2604839  |  3.5892060  | 0.0003481 |
|          age25-34 years:population          | \-6.1706187  | 3.6261276  | \-1.7017103 | 0.0891269 |
|          age35-54 years:population          | \-0.6014393  | 4.1004269  | \-0.1466772 | 0.8834170 |
|          age5-14 years:population           | \-8.9796033  | 3.7153035  | \-2.4169232 | 0.0158341 |
|          age55-74 years:population          | \-0.8372444  | 3.3715255  | \-0.2483281 | 0.8039326 |
|           age75+ years:population           | \-5.2747910  | 3.1110562  | \-1.6954985 | 0.0902985 |
|     age25-34 years:`gdp_per_capita ($)`     | \-0.5576948  | 0.3397704  | \-1.6413874 | 0.1010379 |
|     age35-54 years:`gdp_per_capita ($)`     | \-0.3679886  | 0.3791281  | \-0.9706181 | 0.3319780 |
|     age5-14 years:`gdp_per_capita ($)`      | \-0.2251742  | 0.3435985  | \-0.6553412 | 0.5124019 |
|     age55-74 years:`gdp_per_capita ($)`     | \-0.3477536  | 0.3500694  | \-0.9933848 | 0.3207677 |
|      age75+ years:`gdp_per_capita ($)`      | \-0.6278469  | 0.3310567  | \-1.8964934 | 0.0581887 |
|      age25-34 years:`gdp_for_year ($)`      |  0.4831941   | 0.2873713  |  1.6814278  | 0.0929985 |
|      age35-54 years:`gdp_for_year ($)`      |  0.0558644   | 0.3172164  |  0.1761082  | 0.8602453 |
|      age5-14 years:`gdp_for_year ($)`       |  0.3607650   | 0.2951526  |  1.2222998  | 0.2218882 |
|      age55-74 years:`gdp_for_year ($)`      |  0.0088806   | 0.2681111  |  0.0331229  | 0.9735833 |
|       age75+ years:`gdp_for_year ($)`       |  0.3127316   | 0.2495005  |  1.2534309  | 0.2103479 |

|                    term                     |   estimate   | std.error  |  statistic  |  p.value  |
| :-----------------------------------------: | :----------: | :--------: | :---------: | :-------: |
|                 (Intercept)                 |  2.5199093   | 7.9046711  |  0.3187874  | 0.7499557 |
|                   sexmale                   |  1.0366314   | 0.0416535  | 24.8870099  | 0.0000000 |
|               age25-34 years                |  15.9584239  | 9.2728953  |  1.7209753  | 0.0855709 |
|               age35-54 years                |  1.8670545   | 10.5753940 |  0.1765470  | 0.8599007 |
|                age5-14 years                |  20.9964213  | 9.4840301  |  2.2138712  | 0.0270672 |
|               age55-74 years                |  2.5874080   | 8.6162296  |  0.3002947  | 0.7640161 |
|                age75+ years                 |  13.8415938  | 7.9241816  |  1.7467537  | 0.0809933 |
|                 population                  |  0.4260107   | 2.9634448  |  0.1437552  | 0.8857233 |
|                     HDI                     | \-21.2343535 | 25.8760051 | \-0.8206195 | 0.4120626 |
|             `gdp_for_year ($)`              |  0.0173486   | 0.2649987  |  0.0654667  | 0.9478158 |
|            `gdp_per_capita ($)`             |  0.2966462   | 0.6165608  |  0.4811304  | 0.6305312 |
|               regionCaribbean               | \-2.5301383  | 2.5003136  | \-1.0119284 | 0.3118221 |
|            regionCentral America            | \-2.8510033  | 2.5000954  | \-1.1403578 | 0.2544159 |
|             regionCentral Asia              | \-0.4741630  | 2.5167399  | \-0.1884037 | 0.8505992 |
|            regionEastern Africa             | \-4.6153287  | 2.6322969  | \-1.7533466 | 0.0798552 |
|             regionEastern Asia              |  1.4758395   | 0.8509792  |  1.7342840  | 0.0831822 |
|            regionEastern Europe             | \-2.1334831  | 2.5062684  | \-0.8512588 | 0.3948336 |
|           regionNorthern America            | \-1.8160963  | 6.1183772  | \-0.2968265 | 0.7666619 |
|            regionNorthern Europe            | \-1.5592014  | 2.5133883  | \-0.6203584 | 0.5351661 |
|             regionSouth America             | \-1.5769908  | 2.4982817  | \-0.6312302 | 0.5280372 |
|          regionSouth-Eastern Asia           | \-3.7384365  | 2.5820779  | \-1.4478403 | 0.1479815 |
|            regionSouthern Africa            | \-7.0399931  | 6.2848695  | \-1.1201494 | 0.2629245 |
|             regionSouthern Asia             | \-4.5399118  | 4.6823311  | \-0.9695837 | 0.3324933 |
|            regionSouthern Europe            | \-2.5972177  | 2.4974147  | \-1.0399625 | 0.2986138 |
|             regionWestern Asia              | \-3.2628672  | 2.4967473  | \-1.3068472 | 0.1915712 |
|            regionWestern Europe             | \-1.2096246  | 2.9662786  | \-0.4077920 | 0.6835155 |
|             HDI:regionCaribbean             |  30.6319097  | 26.1112565 |  1.1731304  | 0.2410286 |
|          HDI:regionCentral America          |  28.1189251  | 26.1829169 |  1.0739417  | 0.2831132 |
|           HDI:regionCentral Asia            |  48.5437722  | 26.3251933 |  1.8440044  | 0.0654842 |
|          HDI:regionEastern Africa           | \-46.4758831 | 27.7448886 | \-1.6751151 | 0.0942307 |
|          HDI:regionEastern Europe           |  17.1884396  | 26.4418585 |  0.6500466  | 0.5158145 |
|         HDI:regionNorthern America          |  13.7593264  | 57.1696475 |  0.2406754  | 0.8098571 |
|          HDI:regionNorthern Europe          |  8.5400096   | 26.7660263 |  0.3190615  | 0.7497478 |
|           HDI:regionSouth America           |  15.4973642  | 25.9436039 |  0.5973482  | 0.5504129 |
|        HDI:regionSouth-Eastern Asia         |  19.7525334  | 19.9735295 |  0.9889355  | 0.3229388 |
|          HDI:regionSouthern Europe          |  22.8910983  | 26.1949093 |  0.8738758  | 0.3824000 |
|           HDI:regionWestern Asia            |  29.1020965  | 25.9735906 |  1.1204495  | 0.2627968 |
|          HDI:regionWestern Europe           |  7.8557090   | 22.4001193 |  0.3506994  | 0.7258892 |
|     `gdp_for_year ($)`:regionCaribbean      | \-0.3349923  | 0.1478963  | \-2.2650494 | 0.0237273 |
|  `gdp_for_year ($)`:regionCentral America   | \-0.1011988  | 0.1495226  | \-0.6768122 | 0.4986848 |
|    `gdp_for_year ($)`:regionCentral Asia    | \-0.4495542  | 0.2142800  | \-2.0979757 | 0.0361629 |
|    `gdp_for_year ($)`:regionEastern Asia    | \-0.3831628  | 0.4005241  | \-0.9566536 | 0.3389780 |
|   `gdp_for_year ($)`:regionEastern Europe   |  0.1395157   | 0.1574637  |  0.8860182  | 0.3758251 |
|  `gdp_for_year ($)`:regionNorthern Europe   | \-0.2227774  | 0.1488423  | \-1.4967347 | 0.1347843 |
|   `gdp_for_year ($)`:regionSouth America    | \-0.3887931  | 0.1442737  | \-2.6948304 | 0.0071629 |
| `gdp_for_year ($)`:regionSouth-Eastern Asia |  0.9425181   | 0.5213408  |  1.8078732  | 0.0709327 |
|  `gdp_for_year ($)`:regionSouthern Europe   | \-0.2046936  | 0.1469101  | \-1.3933262 | 0.1638371 |
|    `gdp_for_year ($)`:regionWestern Asia    | \-0.0094657  | 0.1502833  | \-0.0629858 | 0.9497906 |
|    `gdp_per_capita ($)`:regionCaribbean     |  0.1449404   | 0.5516732  |  0.2627288  | 0.7928149 |
| `gdp_per_capita ($)`:regionCentral America  | \-1.0923013  | 0.6995542  | \-1.5614248 | 0.1187464 |
|   `gdp_per_capita ($)`:regionCentral Asia   | \-0.9175886  | 0.5856206  | \-1.5668653 | 0.1174690 |
|  `gdp_per_capita ($)`:regionEastern Europe  | \-0.4036319  | 0.6647629  | \-0.6071817 | 0.5438710 |
| `gdp_per_capita ($)`:regionNorthern Europe  |  0.4096081   | 0.6600452  |  0.6205758  | 0.5350230 |
|  `gdp_per_capita ($)`:regionSouth America   |  1.0100262   | 0.6016985  |  1.6786251  | 0.0935439 |
| `gdp_per_capita ($)`:regionSouthern Europe  | \-0.2989290  | 0.6246232  | \-0.4785749 | 0.6323478 |
|   `gdp_per_capita ($)`:regionWestern Asia   | \-0.5832564  | 0.5619691  | \-1.0378798 | 0.2995820 |
|             age25-34 years:HDI              |  1.7942578   | 2.0339682  |  0.8821465  | 0.3779139 |
|             age35-54 years:HDI              |  6.9028518   | 2.0954559  |  3.2942004  | 0.0010224 |
|              age5-14 years:HDI              | \-5.2616333  | 2.0945989  | \-2.5120003 | 0.0121647 |
|             age55-74 years:HDI              |  7.5700050   | 2.2512405  |  3.3625928  | 0.0008020 |
|              age75+ years:HDI               |  8.1133422   | 2.2604839  |  3.5892060  | 0.0003481 |
|          age25-34 years:population          | \-6.1706187  | 3.6261276  | \-1.7017103 | 0.0891269 |
|          age35-54 years:population          | \-0.6014393  | 4.1004269  | \-0.1466772 | 0.8834170 |
|          age5-14 years:population           | \-8.9796033  | 3.7153035  | \-2.4169232 | 0.0158341 |
|          age55-74 years:population          | \-0.8372444  | 3.3715255  | \-0.2483281 | 0.8039326 |
|           age75+ years:population           | \-5.2747910  | 3.1110562  | \-1.6954985 | 0.0902985 |
|     age25-34 years:`gdp_per_capita ($)`     | \-0.5576948  | 0.3397704  | \-1.6413874 | 0.1010379 |
|     age35-54 years:`gdp_per_capita ($)`     | \-0.3679886  | 0.3791281  | \-0.9706181 | 0.3319780 |
|     age5-14 years:`gdp_per_capita ($)`      | \-0.2251742  | 0.3435985  | \-0.6553412 | 0.5124019 |
|     age55-74 years:`gdp_per_capita ($)`     | \-0.3477536  | 0.3500694  | \-0.9933848 | 0.3207677 |
|      age75+ years:`gdp_per_capita ($)`      | \-0.6278469  | 0.3310567  | \-1.8964934 | 0.0581887 |
|      age25-34 years:`gdp_for_year ($)`      |  0.4831941   | 0.2873713  |  1.6814278  | 0.0929985 |
|      age35-54 years:`gdp_for_year ($)`      |  0.0558644   | 0.3172164  |  0.1761082  | 0.8602453 |
|      age5-14 years:`gdp_for_year ($)`       |  0.3607650   | 0.2951526  |  1.2222998  | 0.2218882 |
|      age55-74 years:`gdp_for_year ($)`      |  0.0088806   | 0.2681111  |  0.0331229  | 0.9735833 |
|       age75+ years:`gdp_for_year ($)`       |  0.3127316   | 0.2495005  |  1.2534309  | 0.2103479 |

### Model Assumptions

![](project-writeup_files/figure-gfm/unnamed-chunk-46-1.png)<!-- -->

From the residual vs. predicted values, the residuals with lower
predicted values seem to be more sparse and spread out than the others,
which may be worth looking into. However, for the most part, the
majority of the residuals are randomly distributed around the red line
and do not exhibit any obvious nonlinear trends. Thus, we can conclude
that constant variance is satisfied.

We will now look at predictors vs. residuals to more closely examine
linearity.

![](project-writeup_files/figure-gfm/unnamed-chunk-47-1.png)<!-- -->

While there are some differences between some of the means of the
residuals for some regions, these means do not seem to vary by too much,
and thus the linearity assumption is moderately satisfied for this
variable. However, there are a few regions with some extreme residuals,
such as the Carribean and Western Asia. It could be worth looking into
these more.

![](project-writeup_files/figure-gfm/unnamed-chunk-48-1.png)<!-- -->

While there is some differences between the means of the residuals for
the two gender groups, these means do not seem to vary by too much, and
the plots seem to have very similar distributions, and thus the
linearity assumption is moderately satisfied for this variable.

![](project-writeup_files/figure-gfm/unnamed-chunk-49-1.png)<!-- -->

Again, while there are some differences between some of the means of the
residuals for some age groups, these means do not seem to vary by too
much, and thus the linearity assumption is satisfied for this variable.

![](project-writeup_files/figure-gfm/unnamed-chunk-50-1.png)<!-- -->

![](project-writeup_files/figure-gfm/unnamed-chunk-51-1.png)<!-- -->

![](project-writeup_files/figure-gfm/unnamed-chunk-52-1.png)<!-- -->

![](project-writeup_files/figure-gfm/unnamed-chunk-53-1.png)<!-- -->

For all of these scatterplots, the residuals seem to be scattered pretty
evenly around the 0 line, and none of them show an obvious curving
shape, so we can conclude that the linearity assumption is met for these
predictors as well.

We also need to check the normality and independence assumptions. For
normality, we can create a QQ-plot of the residuals and a histogram of
the distribution of residuals for this model.

![](project-writeup_files/figure-gfm/unnamed-chunk-54-1.png)<!-- -->

![](project-writeup_files/figure-gfm/unnamed-chunk-55-1.png)<!-- -->

According to the QQ-plot, the normality assumption seems to be satisfied
because the majority of the points seem to align well with the expected
QQ-plot line. In addition, the histogram seems to be approximately
normal and follows a mostly smooth curve.

Finally, based on the description of the data, the independence
assumption seems to be met because this data was not collected over
time, since we only took the year 2010, and there does not appear to be
a cluster effect.

### Leverage

![](project-writeup_files/figure-gfm/unnamed-chunk-56-1.png)<!-- -->

    ## # A tibble: 752 x 7
    ##    region  population age   sex       HDI gdp_for_year.... gdp_per_capita.…
    ##    <fct>        <dbl> <fct> <fct>   <dbl>            <dbl>            <dbl>
    ##  1 Southe…       2.52 55-7… male  -0.0718            -1.94            -1.22
    ##  2 Southe…       2.55 35-5… male  -0.0718            -1.94            -1.22
    ##  3 Southe…       2.49 25-3… male  -0.0718            -1.94            -1.22
    ##  4 Southe…       2.38 75+ … male  -0.0718            -1.94            -1.22
    ##  5 Southe…       2.53 15-2… male  -0.0718            -1.94            -1.22
    ##  6 Southe…       2.49 25-3… fema… -0.0718            -1.94            -1.22
    ##  7 Southe…       2.40 75+ … fema… -0.0718            -1.94            -1.22
    ##  8 Southe…       2.56 35-5… fema… -0.0718            -1.94            -1.22
    ##  9 Southe…       2.52 55-7… fema… -0.0718            -1.94            -1.22
    ## 10 Southe…       2.52 15-2… fema… -0.0718            -1.94            -1.22
    ## # … with 742 more rows

There are 762 points with high leverage.

![](project-writeup_files/figure-gfm/unnamed-chunk-58-1.png)<!-- -->

Based on cook’s distance, these points do not have a significant
influence on the model coefficients. None of these points have a cook’s
distance that is greater than the threshold of 1.

![](project-writeup_files/figure-gfm/unnamed-chunk-59-1.png)<!-- -->

    ## # A tibble: 66 x 7
    ##    region  population age   sex       HDI gdp_for_year.... gdp_per_capita.…
    ##    <fct>        <dbl> <fct> <fct>   <dbl>            <dbl>            <dbl>
    ##  1 Southe…       2.38 75+ … male  -0.0718           -1.94           -1.22  
    ##  2 Southe…       2.52 5-14… male  -0.0718           -1.94           -1.22  
    ##  3 Wester…       2.49 5-14… fema… -0.0728           -2.20           -1.45  
    ##  4 Caribb…       2.33 25-3… male  -0.0198           -2.11            0.714 
    ##  5 Wester…       2.45 15-2… male   0.0252           -1.18            0.422 
    ##  6 Caribb…       2.29 25-3… male  -0.0138           -2.93            0.140 
    ##  7 Caribb…       2.31 55-7… male  -0.0138           -2.93            0.140 
    ##  8 Caribb…       2.16 75+ … male  -0.0138           -2.93            0.140 
    ##  9 Easter…       2.54 5-14… male  -0.0208           -0.499          -0.740 
    ## 10 South …       2.56 75+ … fema…  0.0202            0.964          -0.0649
    ## # … with 56 more rows

There are 66 observations that are considered to have standarized
residuals with large magnitude.

Based on a N(0,1) distribution, we expect 5% of observations to have
standardized residuals with magnitude greater than 2 because of the
68-95-99.7 rule.

There are 66 observations flagged as having standardized residuals with
large magnitude and 1056 observations in total, so approximately 6.25%
of observations have standardized residuals with magnitude greater than
2. This is not a concern because this is only a small percentage greater
than 5%.

    ## Warning: 'tidy.numeric' is deprecated.
    ## See help("Deprecated")

    ## # A tibble: 90 x 2
    ##    names                    x
    ##    <chr>                <dbl>
    ##  1 sexmale                 NA
    ##  2 age25-34 years          NA
    ##  3 age35-54 years          NA
    ##  4 age5-14 years           NA
    ##  5 age55-74 years          NA
    ##  6 age75+ years            NA
    ##  7 population              NA
    ##  8 HDI                     NA
    ##  9 `gdp_for_year ($)`      NA
    ## 10 `gdp_per_capita ($)`    NA
    ## # … with 80 more rows

Because all of the values are NA, this means these variables are
perfectly or almost perfectly correlated. This is most likely to our
inclusion of interaction terms in our model. Thus, we will remove these
terms and run VIF again.

    ## Warning: 'tidy.numeric' is deprecated.
    ## See help("Deprecated")

    ## # A tibble: 25 x 2
    ##    names                    x
    ##    <chr>                <dbl>
    ##  1 sexmale               1.00
    ##  2 age25-34 years        1.67
    ##  3 age35-54 years        1.82
    ##  4 age5-14 years         1.68
    ##  5 age55-74 years        1.67
    ##  6 age75+ years          2.90
    ##  7 population           17.1 
    ##  8 HDI                  13.2 
    ##  9 `gdp_for_year ($)`   21.2 
    ## 10 `gdp_per_capita ($)` 15.0 
    ## # … with 15 more rows

There are some obvious concerns with multicollinearity in this model
because the threshold for the variance inflation factor is 10, and some
of the variance inflation factors are higher than 10. Population, HDI,
`gdp_for_year ($)`, and `gdp_for_year ($)` all have variance inflation
factors greater than 10.

![](project-writeup_files/figure-gfm/unnamed-chunk-63-1.png)<!-- -->

Based on this pairs plot from EDA, we can see that HDI, gdp\_for\_year,
gdp\_per\_capita, and population are all very correlated. Thus, we will
remove gdp\_for\_year from the model, since it seems to have the
strongest correlation with all three of the other variables, and run VIF
again.

    ## Warning: 'tidy.numeric' is deprecated.
    ## See help("Deprecated")

    ## # A tibble: 24 x 2
    ##    names                    x
    ##    <chr>                <dbl>
    ##  1 sexmale               1.00
    ##  2 age25-34 years        1.67
    ##  3 age35-54 years        1.69
    ##  4 age5-14 years         1.67
    ##  5 age55-74 years        1.67
    ##  6 age75+ years          1.82
    ##  7 population            2.09
    ##  8 HDI                  13.1 
    ##  9 `gdp_per_capita ($)`  8.77
    ## 10 regionCaribbean       7.39
    ## # … with 14 more rows

All predictors now have variance inflation factors less than 10 except
for HDI. Thus, we can remove HDI as well from the model.

    ## Warning: 'tidy.numeric' is deprecated.
    ## See help("Deprecated")

    ## # A tibble: 23 x 2
    ##    names                     x
    ##    <chr>                 <dbl>
    ##  1 sexmale                1.00
    ##  2 age25-34 years         1.67
    ##  3 age35-54 years         1.68
    ##  4 age5-14 years          1.67
    ##  5 age55-74 years         1.67
    ##  6 age75+ years           1.81
    ##  7 population             1.99
    ##  8 `gdp_per_capita ($)`   2.30
    ##  9 regionCaribbean        6.17
    ## 10 regionCentral America  4.91
    ## # … with 13 more rows

Now we see that all VIF values are below 10, meaning that we do not have
any multicollinearity. Adding back the interaction terms that still have
both main effects in the model, our final model
is:

|                   term                    |   estimate   | std.error |  statistic  |  p.value  |
| :---------------------------------------: | :----------: | :-------: | :---------: | :-------: |
|                (Intercept)                |  7.4319749   | 1.2976134 |  5.7274183  | 0.0000000 |
|                  sexmale                  |  1.0443624   | 0.0449309 | 23.2437684  | 0.0000000 |
|              age25-34 years               |  0.1824455   | 1.3419519 |  0.1359553  | 0.8918837 |
|              age35-54 years               | \-1.3271798  | 1.3766342 | \-0.9640758 | 0.3352389 |
|               age5-14 years               |  10.1969348  | 1.3442199 |  7.5857637  | 0.0000000 |
|              age55-74 years               | \-0.2663786  | 1.2902339 | \-0.2064576 | 0.8364751 |
|               age75+ years                |  3.1581620   | 1.1867781 |  2.6611225  | 0.0079117 |
|                population                 | \-2.2538772  | 0.4120662 | \-5.4696964 | 0.0000001 |
|             gdp\_per\_capita              | \-0.1044137  | 0.7169762 | \-0.1456307 | 0.8842420 |
|              regionCaribbean              | \-0.7702552  | 0.8021422 | \-0.9602477 | 0.3371606 |
|           regionCentral America           | \-0.8791535  | 0.8181826 | \-1.0745199 | 0.2828466 |
|            regionCentral Asia             |  0.2394507   | 0.8298430 |  0.2885494  | 0.7729855 |
|           regionEastern Africa            | \-0.0058994  | 0.9071472 | \-0.0065032 | 0.9948125 |
|            regionEastern Asia             |  1.5168428   | 0.8822089 |  1.7193692  | 0.0858538 |
|           regionEastern Europe            |  0.0924298   | 0.8074347 |  0.1144735  | 0.9088853 |
|          regionNorthern America           | \-13.2357265 | 9.3860403 | \-1.4101502 | 0.1588035 |
|           regionNorthern Europe           |  0.0393244   | 0.8077281 |  0.0486852  | 0.9611798 |
|            regionSouth America            |  0.1015780   | 0.8111703 |  0.1252240  | 0.9003712 |
|         regionSouth-Eastern Asia          | \-0.5331926  | 0.8128215 | \-0.6559774 | 0.5119882 |
|           regionSouthern Africa           | \-2.0401081  | 1.2465380 | \-1.6366193 | 0.1020219 |
|            regionSouthern Asia            | \-1.2780679  | 1.2686499 | \-1.0074236 | 0.3139728 |
|           regionSouthern Europe           | \-0.5779351  | 0.8046075 | \-0.7182820 | 0.4727497 |
|            regionWestern Asia             | \-1.4212634  | 0.8036647 | \-1.7684781 | 0.0772831 |
|           regionWestern Europe            |  1.1486307   | 0.8856006 |  1.2970077  | 0.1949250 |
|     gdp\_per\_capita:regionCaribbean      |  0.2446517   | 0.7233934 |  0.3382000  | 0.7352828 |
|  gdp\_per\_capita:regionCentral America   | \-0.0706397  | 0.7265289 | \-0.0972290 | 0.9225638 |
|    gdp\_per\_capita:regionCentral Asia    |  0.2544162   | 0.7245420 |  0.3511407  | 0.7255561 |
|   gdp\_per\_capita:regionEastern Africa   |  1.1741816   | 1.2550743 |  0.9355475  | 0.3497301 |
|    gdp\_per\_capita:regionEastern Asia    | \-0.4709708  | 0.8263977 | \-0.5699081 | 0.5688669 |
|   gdp\_per\_capita:regionEastern Europe   | \-0.3288133  | 0.7274604 | \-0.4520017 | 0.6513649 |
|  gdp\_per\_capita:regionNorthern America  |  11.0440498  | 7.5988765 |  1.4533793  | 0.1464294 |
|  gdp\_per\_capita:regionNorthern Europe   | \-0.2052237  | 0.7213537 | \-0.2844981 | 0.7760871 |
|   gdp\_per\_capita:regionSouth America    |  0.2566074   | 0.7266446 |  0.3531402  | 0.7240571 |
| gdp\_per\_capita:regionSouth-Eastern Asia |  0.0830189   | 0.7223317 |  0.1149318  | 0.9085220 |
|  gdp\_per\_capita:regionSouthern Europe   | \-0.0255527  | 0.7213259 | \-0.0354246 | 0.9717482 |
|    gdp\_per\_capita:regionWestern Asia    |  0.0086593   | 0.7193692 |  0.0120374  | 0.9903981 |
|   gdp\_per\_capita:regionWestern Europe   | \-0.8165807  | 0.7657223 | \-1.0664189 | 0.2864894 |
|         age25-34 years:population         | \-0.0015690  | 0.5238859 | \-0.0029950 | 0.9976110 |
|         age35-54 years:population         |  0.6714523   | 0.5329288 |  1.2599288  | 0.2079864 |
|         age5-14 years:population          | \-4.7499597  | 0.5258463 | \-9.0329811 | 0.0000000 |
|         age55-74 years:population         |  0.2749182   | 0.5042421 |  0.5452108  | 0.5857290 |
|          age75+ years:population          | \-1.0223252  | 0.4703201 | \-2.1736796 | 0.0299611 |
|      age25-34 years:gdp\_per\_capita      |  0.0983139   | 0.0743233 |  1.3227877  | 0.1862057 |
|      age35-54 years:gdp\_per\_capita      |  0.2275430   | 0.0744419 |  3.0566512  | 0.0022971 |
|      age5-14 years:gdp\_per\_capita       | \-0.1951639  | 0.0743597 | \-2.6245917 | 0.0088064 |
|      age55-74 years:gdp\_per\_capita      |  0.2579984   | 0.0745822 |  3.4592480  | 0.0005643 |
|       age75+ years:gdp\_per\_capita       |  0.2824247   | 0.0746506 |  3.7832888  | 0.0001639 |

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ sex + population + gdp_per_capita + region + 
    ##     region * gdp_per_capita
    ## Model 2: `suicides/100k pop` ~ sex + age + population + gdp_per_capita + 
    ##     region + region * gdp_per_capita + age * population + age * 
    ##     gdp_per_capita
    ##   Res.Df     RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1024 1415.93                                  
    ## 2   1009  536.72 15    879.21 110.19 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ age + population + gdp_per_capita + region + 
    ##     region * gdp_per_capita + age * population + age * gdp_per_capita
    ## Model 2: `suicides/100k pop` ~ sex + age + population + gdp_per_capita + 
    ##     region + region * gdp_per_capita + age * population + age * 
    ##     gdp_per_capita
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1   1010 824.11                                  
    ## 2   1009 536.72  1    287.39 540.27 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

### Model Validation

We are again removing our interaction terms in this part because the
map() function cannot calculate ‘models’ with the interaction terms in
the model.

    ##         1         2         3         4         5 
    ## 0.6843994 0.6027148 0.6306883 0.7074964 0.6824154

All of these values are relatively small, so we can conclude that our
model predicts well.

### Section 3: Discussion and Limitations

# Discussion

Our original hypothesis was that the economic status of a country (as
determined by the country’s GDP per capita) would predict that country’s
suicide rates. However, in our model, the p-value for gdp\_per\_capita
is 0.8842420. At a .05 significance level, we find that the relationship
between economic status and suicide rates is insignificant. A more
significant predictor (as determined by the p-value less than our
significance level of .05) is population. In our nested-F tests above,
we also found age and sex to be a significant predictors of suicide
rates.

# Test Cases

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit      lwr      upr
    ## 1 3.409644 2.710234 4.109055

    ## [1] 30.25447

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 15-24 years of age, we expect the median suicides per 100k to be
approximately
    30.3.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit      lwr      upr
    ## 1 2.365282 1.665873 3.064691

    ## [1] 10.64704

For females in a Northern American country with a population 2.2 above
the log of the mean and GDP per capita 1.2 above the log of the mean,
who are 15-24 years of age, we expect the median suicides per 100k to be
approximately 10.6, which is much lower than the male rate. This shows
that suicide rates vary by sex, holding all else
    constant.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit      lwr      upr
    ## 1 2.922471 2.228339 3.616603

    ## [1] 18.58716

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 5-14 years of age, we expect the median suicides per 100k to be
approximately
    18.6.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit      lwr      upr
    ## 1 3.409644 2.710234 4.109055

    ## [1] 30.25447

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 15-24 years of age, we expect the median suicides per 100k to be
approximately
    30.3.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit     lwr      upr
    ## 1 3.706615 3.00572 4.407509

    ## [1] 40.71575

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 25-34 years of age, we expect the median suicides per 100k to be
approximately
    40.7.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit     lwr      upr
    ## 1 3.832711 3.10729 4.558133

    ## [1] 46.18758

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 35-54 years of age, we expect the median suicides per 100k to be
approximately
    46.2.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit      lwr      upr
    ## 1 4.057684 3.363107 4.752261

    ## [1] 57.8402

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 55-74 years of age, we expect the median suicides per 100k to be
approximately
    57.8.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##      fit      lwr      upr
    ## 1 4.6576 4.002046 5.313155

    ## [1] 105.3829

For males in a Northern American country with a population 2.2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 75+ years of age, we expect the median suicides per 100k to be
approximately 105.4. We can see that as age increases, suicides per 100k
also increase, holding all else
    constant.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##       fit      lwr      upr
    ## 1 3.86042 3.077674 4.643165

    ## [1] 47.48529

For males in a Northern American country with a population 2 above the
log of the mean and GDP per capita 1.2 above the log of the mean, who
are 15-24 years of age, we expect the median suicides per 100k to be
approximately
    47.5.

    ## Warning in predict.lm(finalmodel, x0, interval = "confidence"): prediction
    ## from a rank-deficient fit may be misleading

    ##        fit      lwr     upr
    ## 1 6.114297 4.694834 7.53376

    ## [1] 452.278

For males in a Northern American country with a population at the log of
the mean and GDP per capita 1.2 above the log of the mean, who are 15-24
years of age, we expect the median suicides per 100k to be approximately
452.3. The vast difference between suicide rates in the highly-populated
subset versus the lower-populated subset shows that suicide rates differ
by population.

# Limitations

Suicide rate in general can vary a lot depending on the year. Just
looking at it by year, we noticed that some countries’ average values
tend to change over time. As such, our model might not be the most
accurate; however, we can predict certain things to a reasonable degree
of accuracy. HDI is a limitation because you can only calculate that
every 5 years. For predicting, we have to plug in numbers that make
sense for a region, or else it gives us a negative grade. In terms of
what we could have done better, we could have assessed multicollinearity
before selecting the model, which may have changed the variables in the
final model. We also could have renamed our mean-centered variables so
that we wouldn’t get confused later on when trying to differentiate. If
we were to conduct this project again, we would utilize a time series
model, as suicide rates vary across time.

### Section 4: Conclusions

### Section 5: Additional Work

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
