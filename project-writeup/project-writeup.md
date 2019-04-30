Stat210 Final Project
================
CamFam
May 1st, 2019

<<<<<<< HEAD
    ## ── Attaching packages ─────────────────────────── tidyverse 1.2.1 ──
=======
    ## ── Attaching packages ────────────────────────────── tidyverse 1.2.1 ──
>>>>>>> Trilok

    ## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
    ## ✔ tibble  2.0.0     ✔ dplyr   0.7.8
    ## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
    ## ✔ readr   1.3.1     ✔ forcats 0.3.0

<<<<<<< HEAD
    ## ── Conflicts ────────────────────────────── tidyverse_conflicts() ──
=======
    ## ── Conflicts ───────────────────────────────── tidyverse_conflicts() ──
>>>>>>> Trilok
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

<<<<<<< HEAD
=======
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

>>>>>>> Trilok
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
<<<<<<< HEAD
age, sex, country, year, HDI, gdp\_for\_year, gdp\_per\_capita, and
generation. Age is the age an individual was when they passed, sex is
the gender of that individual, country is the country they are from,
year is the year they passed, HDI for year is the human development
index for a given country and year, gdp\_for\_year is the GDP for a
given country and year, gdp\_per\_capita is the GDP per capita for a
given country and year, and generation is the generation that an
individual belongs to. We wish to understand how the number of suicides
per 100,000 people in a certain country and year changes as year, GDP,
GDP per capita, and HDI increase or decreases, meaning we want to
understand the population coefficients for year, gdp\_for\_year,
=======
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
>>>>>>> Trilok
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
<<<<<<< HEAD
    ## ── Variable type:character ─────────────────────────────────────────
=======
    ## ── Variable type:character ────────────────────────────────────────────
>>>>>>> Trilok
    ##      variable missing complete    n min max empty n_unique
    ##           age       0     1056 1056   9  11     0        6
    ##       country       0     1056 1056   4  28     0       88
    ##  country-year       0     1056 1056   8  32     0       88
    ##    generation       0     1056 1056   6  12     0        4
    ##           sex       0     1056 1056   4   6     0        2
    ## 
<<<<<<< HEAD
    ## ── Variable type:numeric ───────────────────────────────────────────
=======
    ## ── Variable type:numeric ──────────────────────────────────────────────
>>>>>>> Trilok
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
<<<<<<< HEAD
    ## ── Variable type:character ─────────────────────────────────────────
    ##      variable missing complete    n min max empty n_unique
    ##  country-year       0     1056 1056   8  32     0       88
    ## 
    ## ── Variable type:factor ────────────────────────────────────────────
=======
    ## ── Variable type:character ────────────────────────────────────────────
    ##      variable missing complete    n min max empty n_unique
    ##  country-year       0     1056 1056   8  32     0       88
    ## 
    ## ── Variable type:factor ───────────────────────────────────────────────
>>>>>>> Trilok
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
<<<<<<< HEAD
    ## ── Variable type:numeric ───────────────────────────────────────────
=======
    ## ── Variable type:numeric ──────────────────────────────────────────────
>>>>>>> Trilok
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
<<<<<<< HEAD
    ## ── Variable type:numeric ───────────────────────────────────────────
=======
    ## ── Variable type:numeric ──────────────────────────────────────────────
>>>>>>> Trilok
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
<<<<<<< HEAD

![](project-writeup_files/figure-gfm/unnamed-chunk-14-1.png)<!-- --> In
our data set, we see that most of the countries are from the Americas
and Europe.

![](project-writeup_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->
From this bar graph, we notice that most of our data set seems high in
regions from Western Asia, Southern Europe, South America, Northern
Europe, and the Caribbean.

=======

![](project-writeup_files/figure-gfm/unnamed-chunk-14-1.png)<!-- --> In
our data set, we see that most of the countries are from the Americas
and Europe.

![](project-writeup_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->
From this bar graph, we notice that most of our data set seems high in
regions from Western Asia, Southern Europe, South America, Northern
Europe, and the Caribbean.

>>>>>>> Trilok
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

![](project-writeup_files/figure-gfm/unnamed-chunk-21-1.png)<!-- --> The
distribution of HDI shows that as HDI increases, suicide rate increases
until about .75 and then begins to slightly
    decrease.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->
Because this is skewed greatly, a log transformation of gdp is
    needed.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-23-1.png)<!-- -->

Log transforming the data set, we notice that the distribution of GDPs
of countries has a bimonial
    distribution.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->
Like GDP, we will need to log transform this data
    set.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-25-1.png)<!-- -->

Like the GDP of the country, the GDP Per Capita has a non-normal
distribution. Rather, it is skewed to the left. Since these variables
are so similar, there could be mulitcollinearity between the two.

![](project-writeup_files/figure-gfm/unnamed-chunk-26-1.png)<!-- --> We
do not see a correlation between HDI and Suicides/100k.
![](project-writeup_files/figure-gfm/unnamed-chunk-27-1.png)<!-- --> We
do not see a correlation between GDP and Suicides/100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-28-1.png)<!-- --> We
do not see a correlation between GDP per capita and Suicides/100k.

![](project-writeup_files/figure-gfm/unnamed-chunk-29-1.png)<!-- -->

From the pairs plot, it looks as if HDI, and gdp\_for\_year do not have
a clear linear relationship with suicides/100k pop. However,
gdp\_per\_capita seems to be positively correlated with suicides/100k
pop, meaning as gdp\_per\_capita increases, so does suicides/100k pop.
Additionally, it looks as if HDI and gdp\_per\_capita seem to have a
strong non-linear relationship, indicating that we should continue
looking into this relationship and perhaps include an interaction term
between these two variables. Similarly, HDI and gdp\_for\_year also seem
to have a strong non-linear relationship, so we should include an
interaction term between these two variables as well.

![](project-writeup_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

As mentioned before, we do see evidence of multicollinearity that we
must address in the model.

We plan to do a multiple linear regression because suicides/100k pop is
a quantitative variable (there are no levels to it, since it is a
continuous variable).

## Section 3. Data

<<<<<<< HEAD
    ## Observations: 27,820
    ## Variables: 12
    ## $ country              <chr> "Albania", "Albania", "Albania", "Albania",…
    ## $ year                 <dbl> 1987, 1987, 1987, 1987, 1987, 1987, 1987, 1…
    ## $ sex                  <chr> "male", "male", "female", "male", "male", "…
    ## $ age                  <chr> "15-24 years", "35-54 years", "15-24 years"…
    ## $ suicides_no          <dbl> 21, 16, 14, 1, 9, 1, 6, 4, 1, 0, 0, 0, 2, 1…
    ## $ population           <dbl> 312900, 308000, 289700, 21800, 274300, 3560…
    ## $ `suicides/100k pop`  <dbl> 6.71, 5.19, 4.83, 4.59, 3.28, 2.81, 2.15, 1…
    ## $ `country-year`       <chr> "Albania1987", "Albania1987", "Albania1987"…
    ## $ `HDI for year`       <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
    ## $ `gdp_for_year ($)`   <dbl> 2156624900, 2156624900, 2156624900, 2156624…
    ## $ `gdp_per_capita ($)` <dbl> 796, 796, 796, 796, 796, 796, 796, 796, 796…
    ## $ generation           <chr> "Generation X", "Silent", "Generation X", "…
=======
    ## Start:  AIC=-773.95
    ## `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## 
    ## 
    ## Step:  AIC=-773.95
    ## `suicides/100k pop` ~ country + sex + age + suicides_no + population + 
    ##     HDI + `gdp_for_year ($)` + `gdp_per_capita ($)` + continent + 
    ##     region
    ## 
    ## 
    ## Step:  AIC=-773.95
    ## `suicides/100k pop` ~ country + sex + age + suicides_no + population + 
    ##     HDI + `gdp_for_year ($)` + `gdp_per_capita ($)` + continent
    ## 
    ## 
    ## Step:  AIC=-773.95
    ## `suicides/100k pop` ~ country + sex + age + suicides_no + population + 
    ##     HDI + `gdp_for_year ($)` + `gdp_per_capita ($)`
    ## 
    ## 
    ## Step:  AIC=-773.95
    ## `suicides/100k pop` ~ country + sex + age + suicides_no + population + 
    ##     HDI + `gdp_for_year ($)`
    ## 
    ## 
    ## Step:  AIC=-773.95
    ## `suicides/100k pop` ~ country + sex + age + suicides_no + population + 
    ##     HDI
    ## 
    ## 
    ## Step:  AIC=-773.95
    ## `suicides/100k pop` ~ country + sex + age + suicides_no + population
    ## 
    ##               Df Sum of Sq     RSS     AIC
    ## <none>                      423.06 -773.95
    ## - population   1      1.45  424.51 -772.33
    ## - suicides_no  1     10.79  433.85 -749.35
    ## - sex          1    251.27  674.33 -283.63
    ## - country     87    539.72  962.78  -79.59
    ## - age          5    777.40 1200.46  317.39

    ## 
    ## Call:
    ## lm(formula = `suicides/100k pop` ~ country + sex + age + suicides_no + 
    ##     population, data = suicideFinal)
    ## 
    ## Coefficients:
    ##                         (Intercept)                     countryArgentina  
    ##                           7.031e-01                            3.309e-01  
    ##                      countryArmenia                         countryAruba  
    ##                          -1.321e-01                            1.819e+00  
    ##                    countryAustralia                       countryAustria  
    ##                           5.705e-01                            8.801e-01  
    ##                      countryBahamas                       countryBahrain  
    ##                           7.999e-01                           -5.997e-03  
    ##                     countryBarbados                       countryBelarus  
    ##                           5.595e-01                            1.286e+00  
    ##                      countryBelgium                        countryBelize  
    ##                           1.098e+00                            1.124e+00  
    ##                       countryBrazil                      countryBulgaria  
    ##                          -5.229e-01                            5.360e-01  
    ##                       countryCanada                         countryChile  
    ##                           6.359e-01                            7.774e-01  
    ##                     countryColombia                    countryCosta Rica  
    ##                          -1.538e-01                            2.018e-01  
    ##                      countryCroatia                          countryCuba  
    ##                           9.968e-01                            8.081e-01  
    ##                       countryCyprus                countryCzech Republic  
    ##                           4.308e-01                            6.295e-01  
    ##                      countryDenmark                       countryEcuador  
    ##                           4.606e-01                            4.120e-01  
    ##                  countryEl Salvador                       countryEstonia  
    ##                           3.326e-01                            1.204e+00  
    ##                      countryFinland                        countryFrance  
    ##                           1.086e+00                            6.399e-01  
    ##                      countryGeorgia                       countryGermany  
    ##                          -6.355e-01                            2.919e-01  
    ##                       countryGreece                       countryGrenada  
    ##                          -7.419e-01                            1.515e+00  
    ##                    countryGuatemala                        countryGuyana  
    ##                          -5.732e-01                            1.989e+00  
    ##                      countryHungary                       countryIceland  
    ##                           1.115e+00                            1.584e+00  
    ##                      countryIreland                        countryIsrael  
    ##                           7.288e-01                            2.862e-01  
    ##                        countryItaly                       countryJamaica  
    ##                          -2.649e-01                           -1.656e+00  
    ##                        countryJapan                    countryKazakhstan  
    ##                           5.233e-01                            1.510e+00  
    ##                       countryKuwait                    countryKyrgyzstan  
    ##                          -6.320e-01                            8.657e-01  
    ##                       countryLatvia                     countryLithuania  
    ##                           1.085e+00                            1.579e+00  
    ##                   countryLuxembourg                      countryMaldives  
    ##                           1.137e+00                            4.831e-01  
    ##                        countryMalta                     countryMauritius  
    ##                           8.186e-01                            7.146e-01  
    ##                       countryMexico                   countryNetherlands  
    ##                          -4.407e-01                            4.324e-01  
    ##                  countryNew Zealand                     countryNicaragua  
    ##                           1.008e+00                            3.776e-01  
    ##                       countryNorway                          countryOman  
    ##                           7.328e-01                           -1.121e+00  
    ##                       countryPanama                      countryParaguay  
    ##                          -2.362e-01                            2.311e-02  
    ##                  countryPhilippines                        countryPoland  
    ##                          -7.819e-01                            5.268e-01  
    ##                     countryPortugal                   countryPuerto Rico  
    ##                           4.272e-01                            2.161e-01  
    ##                        countryQatar             countryRepublic of Korea  
    ##                           1.532e-01                            1.446e+00  
    ##                      countryRomania            countryRussian Federation  
    ##                           5.906e-01                            5.719e-01  
    ##                  countrySaint Lucia  countrySaint Vincent and Grenadines  
    ##                           1.165e+00                            1.677e+00  
    ##                       countrySerbia                    countrySeychelles  
    ##                           6.929e-01                            1.886e+00  
    ##                    countrySingapore                      countrySlovakia  
    ##                           5.833e-01                            6.466e-01  
    ##                     countrySlovenia                  countrySouth Africa  
    ##                           1.204e+00                           -1.648e+00  
    ##                        countrySpain                      countrySuriname  
    ##                          -3.074e-01                            2.180e+00  
    ##                       countrySweden                   countrySwitzerland  
    ##                           7.395e-01                            7.379e-01  
    ##                     countryThailand           countryTrinidad and Tobago  
    ##                          -1.715e-02                            1.039e+00  
    ##                       countryTurkey                  countryTurkmenistan  
    ##                          -7.225e-01                           -5.315e-02  
    ##                      countryUkraine          countryUnited Arab Emirates  
    ##                           9.731e-01                           -5.812e-01  
    ##               countryUnited Kingdom                 countryUnited States  
    ##                          -2.731e-01                           -4.935e-01  
    ##                      countryUruguay                    countryUzbekistan  
    ##                           1.224e+00                            1.333e-01  
    ##                             sexmale                       age25-34 years  
    ##                           1.009e+00                            1.646e-01  
    ##                      age35-54 years                        age5-14 years  
    ##                           2.147e-01                           -1.845e+00  
    ##                      age55-74 years                         age75+ years  
    ##                           4.061e-01                            9.737e-01  
    ##                         suicides_no                           population  
    ##                           2.061e-04                            2.516e-08

We chose a multiple linear regression model because we want to predict
the value of a variable based on multile different independent
variables. Based on backward selection, we found that continent, region,
generation, HDI, gdp/year and gdp/capita, so decided to include country,
sex, age, suicides\_no and population.

# Testing of Interesting Interactions

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country * sex + sex + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)   
    ## 1    960 423.06                                
    ## 2    873 370.40 87    52.658 1.4266 0.008494 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 1.4266 and the p-value is 0.008494, which is small.
We can can conclude that the interaction effect of country and sex is a
significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country * age + sex + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS  Df Sum of Sq      F    Pr(>F)    
    ## 1    960 423.06                                   
    ## 2    525 146.23 435    276.83 2.2847 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.2847 and the p-value is 2.2e-16, which is very
small. We can can conclude that the interaction effect of country and
age is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country * suicides_no + sex + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1    960 423.06                                  
    ## 2    874 254.81 86    168.25 6.7103 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 6.7103 and the p-value is 2.2e-16, which is very
small. We can can conclude that the interaction effect of country and
suicides\_no is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country * population + sex + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1    960 423.06                                  
    ## 2    873 335.59 87    87.473 2.6156 2.103e-12 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.6156 and the p-value is 2.103e-12, which is very
small. We can can conclude that the interaction effect of country and
population is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country + sex * age + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1    960 423.06                                  
    ## 2    955 383.06  5    40.002 19.946 < 2.2e-16 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 19.946 and the p-value is 2.2e-16, which is very
small. We can can conclude that the interaction effect of sex and age is
a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country + sex * suicides_no + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)   
    ## 1    960 423.06                                
    ## 2    959 419.19  1      3.87 8.8535 0.002999 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 8.8535 and the p-value is 0.002999, which is very
small. We can can conclude that the interaction effect of sex and
suicides\_no is a significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country + sex * population + age + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F  Pr(>F)  
    ## 1    960 423.06                              
    ## 2    959 421.75  1    1.3083 2.9748 0.08489 .
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 2.9748 and the p-value is 0.08489, which is larger
than 0.05. We can can conclude that the interaction effect of sex and
population is not significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country + sex + age * suicides_no + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1    960 423.06                                  
    ## 2    955 409.75  5    13.313 6.2058 1.132e-05 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 6.2058 and the p-value is 1.132e-05, which is smaller
than 0.05. We can can conclude that the interaction effect of age and
suicides\_no is significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country + sex + age * population + suicides_no + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F   Pr(>F)   
    ## 1    960 423.06                                
    ## 2    955 415.00  5    8.0611 3.7101 0.002483 **
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 3.7101 and the p-value is 0.002483, which is smaller
than 0.05. We can can conclude that the interaction effect of age and
population is significant predictor.

    ## Analysis of Variance Table
    ## 
    ## Model 1: `suicides/100k pop` ~ country + year + sex + age + suicides_no + 
    ##     population + country - year + HDI + (`gdp_for_year ($)`) + 
    ##     (`gdp_per_capita ($)`) + continent + region + generation
    ## Model 2: `suicides/100k pop` ~ country + sex + age + suicides_no * population + 
    ##     population
    ##   Res.Df    RSS Df Sum of Sq      F    Pr(>F)    
    ## 1    960 423.06                                  
    ## 2    959 404.74  1    18.323 43.415 7.291e-11 ***
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1

The F statistic is 43.415 and the p-value is 7.291e-11, which is smaller
than 0.05. We can can conclude that the interaction effect of
suicides\_no and population is significant predictor.

So, we can conclude that to not include the interaction effect between
sex and population. Our updated model will
be:

|                        term                        |   estimate   | std.error  |  statistic  |  p.value  |
| :------------------------------------------------: | :----------: | :--------: | :---------: | :-------: |
|                    (Intercept)                     |  3.2672257   | 3.2344906  |  1.0101207  | 0.3134220 |
|                  countryArgentina                  |  8.3989892   | 4.4478636  |  1.8883199  | 0.0601502 |
|                   countryArmenia                   | \-4.2036113  | 4.1753237  | \-1.0067749 | 0.3150242 |
|                    countryAruba                    | \-1.1615057  | 3.7435846  | \-0.3102656 | 0.7566195 |
|                  countryAustralia                  |  1.5881153   | 4.0971430  |  0.3876153  | 0.6986332 |
|                   countryAustria                   | \-1.8779508  | 3.4414713  | \-0.5456825 | 0.5857747 |
|                   countryBahamas                   | \-1.9788075  | 4.9490331  | \-0.3998372 | 0.6896206 |
|                   countryBahrain                   | \-1.9570937  | 3.2720068  | \-0.5981325 | 0.5502973 |
|                  countryBarbados                   | \-2.1804055  | 3.6782269  | \-0.5927871 | 0.5538638 |
|                   countryBelarus                   | \-0.1174118  | 3.3383005  | \-0.0351711 | 0.9719716 |
|                   countryBelgium                   | \-1.0342046  | 3.4438490  | \-0.3003049 | 0.7641962 |
|                   countryBelize                    | \-10.4453850 | 9.2049178  | \-1.1347614 | 0.2575709 |
|                   countryBrazil                    |  30.0697420  | 11.9350743 |  2.5194432  | 0.0123835 |
|                  countryBulgaria                   | \-3.3107884  | 3.4250383  | \-0.9666428 | 0.3346643 |
|                   countryCanada                    |  3.4414207   | 3.9827341  |  0.8640850  | 0.3883762 |
|                    countryChile                    |  8.7361327   | 4.2069226  |  2.0766089  | 0.0388676 |
|                  countryColombia                   |  21.1078549  | 5.3024695  |  3.9807594  | 0.0000903 |
|                 countryCosta Rica                  |  4.3135545   | 5.8501169  |  0.7373450  | 0.4616096 |
|                   countryCroatia                   | \-1.9218909  | 3.3917843  | \-0.5666312 | 0.5714772 |
|                    countryCuba                     | \-1.3468675  | 4.6719425  | \-0.2882885 | 0.7733667 |
|                   countryCyprus                    | \-1.2621217  | 4.3220367  | \-0.2920201 | 0.7705154 |
|               countryCzech Republic                | \-1.5844164  | 3.3818594  | \-0.4685045 | 0.6398354 |
|                   countryDenmark                   | \-1.7770246  | 3.5992426  | \-0.4937218 | 0.6219396 |
|                   countryEcuador                   |  11.4539422  | 6.3425974  |  1.8058756  | 0.0721502 |
|                 countryEl Salvador                 |  8.6058865   | 4.5261256  |  1.9013804  | 0.0584113 |
|                   countryEstonia                   | \-2.0265792  | 3.2936775  | \-0.6152937 | 0.5389250 |
|                   countryFinland                   | \-0.8796698  | 3.3871608  | \-0.2597071 | 0.7953052 |
|                   countryFrance                    |  3.4160590   | 4.6770861  |  0.7303819  | 0.4658462 |
|                   countryGeorgia                   | \-7.6616960  | 3.4537487  | \-2.2183710 | 0.0274357 |
|                   countryGermany                   |  4.0473919   | 4.7026790  |  0.8606566  | 0.3902585 |
|                   countryGreece                    | \-2.0906992  | 3.4187308  | \-0.6115425 | 0.5414007 |
|                   countryGrenada                   | \-1.0430697  | 4.7668617  | \-0.2188169 | 0.8269727 |
|                  countryGuatemala                  |  17.9841579  | 5.1701140  |  3.4784838  | 0.0005954 |
|                   countryGuyana                    |  6.3032230   | 5.0251063  |  1.2543462  | 0.2108971 |
|                   countryHungary                   | \-1.4047460  | 3.3409336  | \-0.4204651 | 0.6745098 |
|                   countryIceland                   | \-0.2163723  | 4.3594875  | \-0.0496325 | 0.9604552 |
|                   countryIreland                   | \-0.9712295  | 4.2547471  | \-0.2282696 | 0.8196247 |
|                   countryIsrael                    | \-1.1372287  | 4.1273395  | \-0.2755355 | 0.7831343 |
|                    countryItaly                    |  0.5468072   | 3.9702275  |  0.1377269  | 0.8905680 |
|                   countryJamaica                   | \-4.8540585  | 4.8600180  | \-0.9987738 | 0.3188778 |
|                    countryJapan                    |  8.5084310   | 5.5540297  |  1.5319383  | 0.1268123 |
|                 countryKazakhstan                  |  7.2060451   | 3.9869787  |  1.8073949  | 0.0719124 |
|                   countryKuwait                    | \-2.7234102  | 3.2558041  | \-0.8364785 | 0.4036910 |
|                 countryKyrgyzstan                  |  4.2580417   | 4.8520809  |  0.8775702  | 0.3810263 |
|                   countryLatvia                    | \-2.2332833  | 3.2893562  | \-0.6789424 | 0.4978075 |
|                  countryLithuania                  | \-1.3524384  | 3.3122471  | \-0.4083145 | 0.6833951 |
|                 countryLuxembourg                  | \-0.9820780  | 3.4823528  | \-0.2820157 | 0.7781667 |
|                  countryMaldives                   | \-2.4030734  | 3.5077851  | \-0.6850686 | 0.4939404 |
|                    countryMalta                    | \-1.7404951  | 3.5566631  | \-0.4893618 | 0.6250181 |
|                  countryMauritius                  |  3.1541316   | 4.2874622  |  0.7356640  | 0.4626304 |
|                   countryMexico                    |  35.2092107  | 8.2842716  |  4.2501275  | 0.0000303 |
|                 countryNetherlands                 | \-2.4669184  | 3.5936723  | \-0.6864617 | 0.4930633 |
|                 countryNew Zealand                 |  0.7392207   | 4.1052275  |  0.1800682  | 0.8572461 |
|                  countryNicaragua                  |  9.9757220   | 4.4125215  |  2.2607758  | 0.0246404 |
|                   countryNorway                    | \-1.2605995  | 3.5301493  | \-0.3570952 | 0.7213242 |
|                    countryOman                     | \-4.0449386  | 3.2909072  | \-1.2291257 | 0.2201896 |
|                   countryPanama                    |  10.2896128  | 6.5480730  |  1.5713956  | 0.1173657 |
|                  countryParaguay                   |  6.0940302   | 8.3338388  |  0.7312393  | 0.4653234 |
|                 countryPhilippines                 |  12.9505293  | 7.0648343  |  1.8330974  | 0.0679868 |
|                   countryPoland                    |  1.2673189   | 3.8401742  |  0.3300160  | 0.7416665 |
|                  countryPortugal                   | \-3.3679750  | 3.8384634  | \-0.8774279 | 0.3811034 |
|                 countryPuerto Rico                 |  0.0051061   | 3.9436424  |  0.0012948  | 0.9989680 |
|                    countryQatar                    | \-2.4343795  | 3.2491162  | \-0.7492436 | 0.4544205 |
|              countryRepublic of Korea              |  3.2057098   | 3.9614091  |  0.8092347  | 0.4191558 |
|                   countryRomania                   | \-0.8544537  | 3.5346718  | \-0.2417349 | 0.8091853 |
|             countryRussian Federation              |  20.4069349  | 8.4956406  |  2.4020478  | 0.0170398 |
|                 countrySaint Lucia                 | \-2.0652089  | 7.2369650  | \-0.2853695 | 0.7755993 |
|        countrySaint Vincent and Grenadines         | \-4.7593267  | 4.7000516  | \-1.0126116 | 0.3122326 |
|                   countrySerbia                    | \-5.2375068  | 3.7191141  | \-1.4082673 | 0.1603043 |
|                 countrySeychelles                  |  0.3220372   | 3.5992364  |  0.0894738  | 0.9287776 |
|                  countrySingapore                  | \-2.2507940  | 4.4070401  | \-0.5107269 | 0.6099966 |
|                  countrySlovakia                   | \-2.1516942  | 3.4169877  | \-0.6297050 | 0.5294673 |
|                  countrySlovenia                   | \-2.7140282  | 3.3226791  | \-0.8168192 | 0.4148157 |
|                countrySouth Africa                 |  8.3813656   | 5.2944432  |  1.5830495  | 0.1146846 |
|                    countrySpain                    | \-0.4249737  | 3.7215844  | \-0.1141916 | 0.9091783 |
|                  countrySuriname                   |  3.7649677   | 4.2564872  |  0.8845246  | 0.3772698 |
|                   countrySweden                    | \-0.2515671  | 3.5326572  | \-0.0712119 | 0.9432865 |
|                 countrySwitzerland                 | \-1.7109382  | 3.4657726  | \-0.4936672 | 0.6219782 |
|                  countryThailand                   |  7.0692667   | 4.9101367  |  1.4397291  | 0.1512051 |
|             countryTrinidad and Tobago             |  9.3832507   | 4.8943643  |  1.9171541  | 0.0563673 |
|                   countryTurkey                    |  5.6975569   | 5.5350168  |  1.0293658  | 0.3043107 |
|                countryTurkmenistan                 |  13.8030743  | 5.4005075  |  2.5558846  | 0.0111891 |
|                   countryUkraine                   |  4.1289295   | 3.9862673  |  1.0357884  | 0.3013098 |
|            countryUnited Arab Emirates             | \-2.4901490  | 3.2416955  | \-0.7681625 | 0.4431214 |
|               countryUnited Kingdom                |  4.3083208   | 4.3942089  |  0.9804542  | 0.3278174 |
|                countryUnited States                |  36.7400894  | 17.9604022 |  2.0456162  | 0.0418493 |
|                   countryUruguay                   | \-0.8684474  | 3.5640615  | \-0.2436679 | 0.8076895 |
|                 countryUzbekistan                  |  13.0108571  | 6.5459454  |  1.9876208  | 0.0479535 |
|                      sexmale                       | \-0.0912611  | 0.2183473  | \-0.4179630 | 0.6763358 |
|                   age25-34 years                   | \-0.6476343  | 1.0915233  | \-0.5933307 | 0.5535006 |
|                   age35-54 years                   |  0.3101312   | 1.4354008  |  0.2160590  | 0.8291194 |
|                   age5-14 years                    | \-0.8324497  | 0.6520838  | \-1.2765993 | 0.2029378 |
|                   age55-74 years                   | \-0.7804933  | 0.4757440  | \-1.6405740 | 0.1021535 |
|                    age75+ years                    | \-1.5196293  | 2.5591928  | \-0.5937924 | 0.5531922 |
|                    suicides\_no                    |  0.1142780   | 0.0335731  |  3.4038613  | 0.0007746 |
|                     population                     | \-0.0000113  | 0.0000116  | \-0.9733798 | 0.3313130 |
|              countryArgentina:sexmale              |  0.9059709   | 0.4356431  |  2.0796175  | 0.0385881 |
|               countryArmenia:sexmale               |  0.3506757   | 0.4123070  |  0.8505208  | 0.3958560 |
|                countryAruba:sexmale                |  0.2498571   | 0.2981546  |  0.8380121  | 0.4028308 |
|              countryAustralia:sexmale              |  0.9766629   | 0.3275076  |  2.9821080  | 0.0031479 |
|               countryAustria:sexmale               |  1.1084621   | 0.3513504  |  3.1548619  | 0.0018040 |
|               countryBahamas:sexmale               |  0.3177688   | 0.2922152  |  1.0874481  | 0.2778946 |
|               countryBahrain:sexmale               |  0.1905253   | 0.3094107  |  0.6157682  | 0.5386122 |
|              countryBarbados:sexmale               |  0.2660030   | 0.3040078  |  0.8749874  | 0.3824274 |
|               countryBelarus:sexmale               |  1.3471975   | 0.3373218  |  3.9938049  | 0.0000857 |
|               countryBelgium:sexmale               |  1.1594581   | 0.3437829  |  3.3726461  | 0.0008636 |
|               countryBelize:sexmale                |  0.1529712   | 0.3451782  |  0.4431658  | 0.6580322 |
|               countryBrazil:sexmale                |  1.6015218   | 0.5586769  |  2.8666331  | 0.0045050 |
|              countryBulgaria:sexmale               |  1.1507944   | 0.3427611  |  3.3574240  | 0.0009104 |
|               countryCanada:sexmale                |  0.8888364   | 0.3378396  |  2.6309421  | 0.0090481 |
|                countryChile:sexmale                |  1.1120515   | 0.3664062  |  3.0350242  | 0.0026613 |
|              countryColombia:sexmale               |  1.7308421   | 0.3671303  |  4.7145171  | 0.0000040 |
|             countryCosta Rica:sexmale              |  1.8970785   | 0.3337528  |  5.6840822  | 0.0000000 |
|               countryCroatia:sexmale               |  0.6608540   | 0.3259489  |  2.0274771  | 0.0436831 |
|                countryCuba:sexmale                 |  0.8808179   | 0.3440180  |  2.5603829  | 0.0110491 |
|               countryCyprus:sexmale                |  0.3786296   | 0.3496587  |  1.0828546  | 0.2799246 |
|           countryCzech Republic:sexmale            |  1.3041930   | 0.3282240  |  3.9734851  | 0.0000929 |
|               countryDenmark:sexmale               |  0.7556239   | 0.3319816  |  2.2761021  | 0.0236930 |
|               countryEcuador:sexmale               |  0.7209138   | 0.3490728  |  2.0652246  | 0.0399411 |
|             countryEl Salvador:sexmale             |  0.5123639   | 0.3365944  |  1.5221995  | 0.1292331 |
|               countryEstonia:sexmale               |  0.8658208   | 0.3395049  |  2.5502452  | 0.0113669 |
|               countryFinland:sexmale               |  1.0418258   | 0.3686912  |  2.8257410  | 0.0051013 |
|               countryFrance:sexmale                |  0.9734370   | 0.3488370  |  2.7905212  | 0.0056714 |
|               countryGeorgia:sexmale               |  1.1957780   | 0.3411235  |  3.5054104  | 0.0005409 |
|               countryGermany:sexmale               |  1.2751666   | 0.3798136  |  3.3573488  | 0.0009106 |
|               countryGreece:sexmale                |  0.9524857   | 0.3346615  |  2.8461172  | 0.0047958 |
|               countryGrenada:sexmale               |  0.3353447   | 0.2645907  |  1.2674092  | 0.2061978 |
|              countryGuatemala:sexmale              |  1.5202958   | 0.3393785  |  4.4796464  | 0.0000114 |
|               countryGuyana:sexmale                |  0.5925855   | 0.2899320  |  2.0438779  | 0.0420222 |
|               countryHungary:sexmale               |  1.1452958   | 0.3160669  |  3.6235862  | 0.0003524 |
|               countryIceland:sexmale               |  1.0394457   | 0.4555173  |  2.2819016  | 0.0233429 |
|               countryIreland:sexmale               |  0.7210175   | 0.3361274  |  2.1450722  | 0.0329187 |
|               countryIsrael:sexmale                |  0.6380045   | 0.3882893  |  1.6431163  | 0.1016261 |
|                countryItaly:sexmale                |  1.7390732   | 0.3594791  |  4.8377584  | 0.0000023 |
|               countryJamaica:sexmale               |  0.1219288   | 0.3097970  |  0.3935765  | 0.6942319 |
|                countryJapan:sexmale                |  0.8683306   | 0.4482213  |  1.9372809  | 0.0538466 |
|             countryKazakhstan:sexmale              |  0.4420730   | 0.3692874  |  1.1970974  | 0.2324116 |
|               countryKuwait:sexmale                |  0.1606898   | 0.2951553  |  0.5444245  | 0.5866386 |
|             countryKyrgyzstan:sexmale              |  0.7450229   | 0.3293908  |  2.2618205  | 0.0245748 |
|               countryLatvia:sexmale                |  1.3262470   | 0.3334444  |  3.9774152  | 0.0000915 |
|              countryLithuania:sexmale              |  1.0478452   | 0.3283725  |  3.1910261  | 0.0016005 |
|             countryLuxembourg:sexmale              |  0.8091601   | 0.2988213  |  2.7078399  | 0.0072435 |
|              countryMaldives:sexmale               |  0.1302618   | 0.3218403  |  0.4047404  | 0.6860172 |
|                countryMalta:sexmale                |  0.7343078   | 0.2981550  |  2.4628394  | 0.0144645 |
|              countryMauritius:sexmale              |  0.7417417   | 0.3611480  |  2.0538442  | 0.0410393 |
|               countryMexico:sexmale                |  1.7153191   | 0.4636927  |  3.6992581  | 0.0002663 |
|             countryNetherlands:sexmale             |  1.1674946   | 0.3301644  |  3.5361006  | 0.0004845 |
|             countryNew Zealand:sexmale             |  0.5477635   | 0.3246297  |  1.6873484  | 0.0927936 |
|              countryNicaragua:sexmale              |  1.4037364   | 0.3327981  |  4.2179819  | 0.0000346 |
|               countryNorway:sexmale                |  1.1584151   | 0.4075946  |  2.8420767  | 0.0048550 |
|                countryOman:sexmale                 |  0.2697799   | 0.3137867  |  0.8597556  | 0.3907541 |
|               countryPanama:sexmale                |  0.7465071   | 0.3290946  |  2.2683659  | 0.0241672 |
|              countryParaguay:sexmale               |  0.6243838   | 0.3523050  |  1.7722819  | 0.0775755 |
|             countryPhilippines:sexmale             |  1.7551575   | 0.4296005  |  4.0855569  | 0.0000594 |
|               countryPoland:sexmale                |  1.4176647   | 0.3447530  |  4.1121177  | 0.0000533 |
|              countryPortugal:sexmale               |  0.5745552   | 0.3316495  |  1.7324170  | 0.0844426 |
|             countryPuerto Rico:sexmale             |  1.2063712   | 0.3384559  |  3.5643378  | 0.0004375 |
|                countryQatar:sexmale                | \-0.0663013  | 0.3018261  | \-0.2196671 | 0.8263111 |
|          countryRepublic of Korea:sexmale          |  1.1956663   | 0.4259397  |  2.8071258  | 0.0053958 |
|               countryRomania:sexmale               |  1.2556793   | 0.3186560  |  3.9405486  | 0.0001058 |
|         countryRussian Federation:sexmale          | \-0.9906243  | 0.8650884  | \-1.1451134 | 0.2532661 |
|             countrySaint Lucia:sexmale             |  0.2529138   | 0.3364364  |  0.7517433  | 0.4529183 |
|    countrySaint Vincent and Grenadines:sexmale     |  0.3278564   | 0.2831473  |  1.1579003  | 0.2480186 |
|               countrySerbia:sexmale                |  0.8076558   | 0.3438714  |  2.3487146  | 0.0196240 |
|             countrySeychelles:sexmale              |  0.2995621   | 0.2857574  |  1.0483092  | 0.2955167 |
|              countrySingapore:sexmale              |  0.4294784   | 0.3006851  |  1.4283327  | 0.1544543 |
|              countrySlovakia:sexmale               |  1.4803935   | 0.3234385  |  4.5770478  | 0.0000075 |
|              countrySlovenia:sexmale               |  1.8139172   | 0.3427227  |  5.2926669  | 0.0000003 |
|            countrySouth Africa:sexmale             |  1.0469386   | 0.3502134  |  2.9894301  | 0.0030760 |
|                countrySpain:sexmale                |  1.7237413   | 0.3425590  |  5.0319545  | 0.0000009 |
|              countrySuriname:sexmale               |  0.3574263   | 0.3042555  |  1.1747574  | 0.2412185 |
|               countrySweden:sexmale                |  0.5325497   | 0.3514482  |  1.5153006  | 0.1309698 |
|             countrySwitzerland:sexmale             |  1.1883820   | 0.3384336  |  3.5114181  | 0.0005294 |
|              countryThailand:sexmale               |  1.1549501   | 0.3598723  |  3.2093336  | 0.0015059 |
|         countryTrinidad and Tobago:sexmale         |  0.6725629   | 0.3314769  |  2.0289889  | 0.0435277 |
|               countryTurkey:sexmale                |  1.0529129   | 0.3831840  |  2.7477993  | 0.0064402 |
|            countryTurkmenistan:sexmale             |  0.5249129   | 0.3296360  |  1.5924018  | 0.1125682 |
|               countryUkraine:sexmale               |  0.7877062   | 0.3911911  |  2.0136098  | 0.0451308 |
|        countryUnited Arab Emirates:sexmale         |  0.2162397   | 0.3043557  |  0.7104834  | 0.4780720 |
|           countryUnited Kingdom:sexmale            |  0.7307478   | 0.3435554  |  2.1270156  | 0.0344061 |
|            countryUnited States:sexmale            | \-0.7847091  | 1.4127279  | \-0.5554566 | 0.5790831 |
|               countryUruguay:sexmale               |  0.0824189   | 0.4292270  |  0.1920170  | 0.8478860 |
|             countryUzbekistan:sexmale              |  0.7759032   | 0.3214168  |  2.4140092  | 0.0165032 |
|          countryArgentina:age25-34 years           | \-0.3506630  | 2.2235678  | \-0.1577029 | 0.8748193 |
|           countryArmenia:age25-34 years            |  0.6483345   | 1.1546384  |  0.5615043  | 0.5749608 |
|            countryAruba:age25-34 years             |  0.6725935   | 1.1283911  |  0.5960642  | 0.5516760 |
|          countryAustralia:age25-34 years           |  0.5824572   | 1.3827122  |  0.4212425  | 0.6739428 |
|           countryAustria:age25-34 years            |  0.7409196   | 1.1292377  |  0.6561237  | 0.5123528 |
|           countryBahamas:age25-34 years            |  0.6333816   | 1.2737969  |  0.4972391  | 0.6194610 |
|           countryBahrain:age25-34 years            |  0.8990251   | 1.1467555  |  0.7839728  | 0.4338042 |
|           countryBarbados:age25-34 years           |  0.6118330   | 1.1299657  |  0.5414616  | 0.5886755 |
|           countryBelarus:age25-34 years            |  0.8686234   | 1.1475893  |  0.7569113  | 0.4498215 |
|           countryBelgium:age25-34 years            |  0.9534297   | 1.1458287  |  0.8320875  | 0.4061601 |
|            countryBelize:age25-34 years            |  2.5769045   | 2.2782829  |  1.1310731  | 0.2591169 |
|            countryBrazil:age25-34 years            | \-2.9543947  | 10.8101799 | \-0.2732975 | 0.7848520 |
|           countryBulgaria:age25-34 years           |  0.4964247   | 1.1508960  |  0.4313376  | 0.6665976 |
|            countryCanada:age25-34 years            |  0.5449849   | 1.6964877  |  0.3212431  | 0.7482968 |
|            countryChile:age25-34 years             | \-0.5063179  | 1.3282865  | \-0.3811812 | 0.7033951 |
|           countryColombia:age25-34 years           | \-2.5017903  | 2.6477111  | \-0.9448879 | 0.3456357 |
|          countryCosta Rica:age25-34 years          |  0.2669468   | 1.2184667  |  0.2190842  | 0.8267647 |
|           countryCroatia:age25-34 years            |  0.1809285   | 1.1293043  |  0.1602123  | 0.8728442 |
|             countryCuba:age25-34 years             |  0.6412784   | 1.2212201  |  0.5251129  | 0.5999738 |
|            countryCyprus:age25-34 years            |  0.1766939   | 1.1280841  |  0.1566319  | 0.8756624 |
|        countryCzech Republic:age25-34 years        |  0.7117724   | 1.1864883  |  0.5998984  | 0.5491217 |
|           countryDenmark:age25-34 years            |  0.7055833   | 1.1166175  |  0.6318934  | 0.5280386 |
|           countryEcuador:age25-34 years            | \-1.7072113  | 1.5827462  | \-1.0786387 | 0.2817968 |
|         countryEl Salvador:age25-34 years          | \-2.1136088  | 1.3655540  | \-1.5478032 | 0.1229448 |
|           countryEstonia:age25-34 years            |  0.8719458   | 1.1235256  |  0.7760801  | 0.4384412 |
|           countryFinland:age25-34 years            |  0.7070695   | 1.1173439  |  0.6328128  | 0.5274390 |
|            countryFrance:age25-34 years            |  0.2689466   | 2.5259164  |  0.1064749  | 0.9152917 |
|           countryGeorgia:age25-34 years            |  0.6151628   | 1.1164323  |  0.5510077  | 0.5821245 |
|           countryGermany:age25-34 years            |  0.4194336   | 2.9893123  |  0.1403111  | 0.8885281 |
|            countryGreece:age25-34 years            |  1.0856589   | 1.2274128  |  0.8845100  | 0.3772777 |
|           countryGrenada:age25-34 years            |  0.8445102   | 1.4236473  |  0.5932018  | 0.5535867 |
|          countryGuatemala:age25-34 years           | \-5.3267641  | 1.7325250  | \-3.0745668 | 0.0023439 |
|            countryGuyana:age25-34 years            | \-0.6522750  | 1.3418605  | \-0.4860975 | 0.6273273 |
|           countryHungary:age25-34 years            |  1.0419255   | 1.1630133  |  0.8958845  | 0.3711832 |
|           countryIceland:age25-34 years            |  0.6979584   | 1.1293017  |  0.6180442  | 0.5371133 |
|           countryIreland:age25-34 years            |  0.8014394   | 1.4527589  |  0.5516672  | 0.5816731 |
|            countryIsrael:age25-34 years            |  0.4495859   | 1.1344988  |  0.3962859  | 0.6922349 |
|            countryItaly:age25-34 years             |  1.4933836   | 2.2802290  |  0.6549270  | 0.5131217 |
|           countryJamaica:age25-34 years            |  0.5738363   | 1.3360296  |  0.4295087  | 0.6679260 |
|            countryJapan:age25-34 years             |  1.8918901   | 4.2168744  |  0.4486475  | 0.6540777 |
|          countryKazakhstan:age25-34 years          | \-0.6673589  | 1.3685915  | \-0.4876246 | 0.6262466 |
|            countryKuwait:age25-34 years            | \-0.3430052  | 1.3498337  | \-0.2541092 | 0.7996217 |
|          countryKyrgyzstan:age25-34 years          | \-1.1645128  | 1.4991051  | \-0.7768053 | 0.4380139 |
|            countryLatvia:age25-34 years            |  0.4673942   | 1.1185631  |  0.4178523  | 0.6764166 |
|          countryLithuania:age25-34 years           |  0.6833190   | 1.1171113  |  0.6116839  | 0.5413072 |
|          countryLuxembourg:age25-34 years          |  1.1092238   | 1.1615580  |  0.9549449  | 0.3405355 |
|           countryMaldives:age25-34 years           |  0.6436565   | 1.1486477  |  0.5603602  | 0.5757396 |
|            countryMalta:age25-34 years             |  0.5856539   | 1.1356158  |  0.5157148  | 0.6065131 |
|          countryMauritius:age25-34 years           |  1.1623045   | 1.1305075  |  1.0281263  | 0.3048921 |
|            countryMexico:age25-34 years            | \-5.5529607  | 6.5324825  | \-0.8500537 | 0.3961151 |
|         countryNetherlands:age25-34 years          |  0.8750396   | 1.2082100  |  0.7242446  | 0.4695982 |
|         countryNew Zealand:age25-34 years          |  0.4287711   | 1.1558034  |  0.3709723  | 0.7109748 |
|          countryNicaragua:age25-34 years           | \-1.8520443  | 1.2595035  | \-1.4704558 | 0.1427059 |
|            countryNorway:age25-34 years            |  0.8972319   | 1.1161067  |  0.8038944  | 0.4222279 |
|             countryOman:age25-34 years             |  0.5449363   | 1.1452761  |  0.4758121  | 0.6346271 |
|            countryPanama:age25-34 years            | \-1.6773010  | 1.2051735  | \-1.3917507 | 0.1652449 |
|           countryParaguay:age25-34 years           | \-1.3835275  | 2.0912689  | \-0.6615732 | 0.5088590 |
|         countryPhilippines:age25-34 years          | \-4.2044201  | 5.2857905  | \-0.7954194 | 0.4271302 |
|            countryPoland:age25-34 years            |  0.9714293   | 1.9581931  |  0.4960845  | 0.6202741 |
|           countryPortugal:age25-34 years           |  0.5587664   | 1.2911057  |  0.4327813  | 0.6655498 |
|         countryPuerto Rico:age25-34 years          |  0.7078435   | 1.1175400  |  0.6333943  | 0.5270599 |
|            countryQatar:age25-34 years             |  0.3284446   | 1.1385499  |  0.2884763  | 0.7732232 |
|      countryRepublic of Korea:age25-34 years       |  0.7706344   | 2.3476366  |  0.3282597  | 0.7429923 |
|           countryRomania:age25-34 years            |  0.5567514   | 1.3860859  |  0.4016717  | 0.6882716 |
|      countryRussian Federation:age25-34 years      |  1.6095422   | 6.5763846  |  0.2447458  | 0.8068557 |
|         countrySaint Lucia:age25-34 years          |  0.7718073   | 1.3997881  |  0.5513744  | 0.5818735 |
| countrySaint Vincent and Grenadines:age25-34 years |  1.3727496   | 1.2548346  |  1.0939685  | 0.2750302 |
|            countrySerbia:age25-34 years            |  0.7167287   | 1.1716965  |  0.6117016  | 0.5412955 |
|          countrySeychelles:age25-34 years          |  0.6706477   | 1.1301444  |  0.5934177  | 0.5534425 |
|          countrySingapore:age25-34 years           |  0.7793839   | 1.1790928  |  0.6610031  | 0.5092239 |
|           countrySlovakia:age25-34 years           |  0.7061131   | 1.1442447  |  0.6170997  | 0.5377351 |
|           countrySlovenia:age25-34 years           |  0.8846505   | 1.1470934  |  0.7712105  | 0.4413163 |
|         countrySouth Africa:age25-34 years         | \-1.8098677  | 3.2153214  | \-0.5628886 | 0.5740193 |
|            countrySpain:age25-34 years             |  1.9730908   | 2.1272771  |  0.9275194  | 0.3545587 |
|           countrySuriname:age25-34 years           | \-0.0275368  | 1.2096793  | \-0.0227637 | 0.9818570 |
|            countrySweden:age25-34 years            |  0.5530855   | 1.1380208  |  0.4860065  | 0.6273917 |
|         countrySwitzerland:age25-34 years          |  1.0136044   | 1.1358664  |  0.8923623  | 0.3730638 |
|           countryThailand:age25-34 years           |  0.8102542   | 3.1913627  |  0.2538897  | 0.7997911 |
|     countryTrinidad and Tobago:age25-34 years      |  1.2598564   | 1.1530424  |  1.0926366  | 0.2756136 |
|            countryTurkey:age25-34 years            | \-0.6266855  | 3.9517660  | \-0.1585837 | 0.8741260 |
|         countryTurkmenistan:age25-34 years         | \-3.2497607  | 1.4995446  | \-2.1671651 | 0.0311745 |
|           countryUkraine:age25-34 years            |  0.8203751   | 2.2075681  |  0.3716194  | 0.7104936 |
|     countryUnited Arab Emirates:age25-34 years     |  1.4594334   | 1.4079642  |  1.0365557  | 0.3009526 |
|        countryUnited Kingdom:age25-34 years        |  0.0181429   | 2.6496111  |  0.0068474  | 0.9945421 |
|        countryUnited States:age25-34 years         | \-5.3431683  | 13.2050719 | \-0.4046300 | 0.6860983 |
|           countryUruguay:age25-34 years            |  0.7020363   | 1.1182346  |  0.6278077  | 0.5307076 |
|          countryUzbekistan:age25-34 years          | \-3.3792341  | 2.3865676  | \-1.4159390 | 0.1580481 |
|          countryArgentina:age35-54 years           | \-3.8345927  | 2.8743506  | \-1.3340727 | 0.1834038 |
|           countryArmenia:age35-54 years            | \-1.5042186  | 2.0757860  | \-0.7246501 | 0.4693498 |
|            countryAruba:age35-54 years             | \-1.3684123  | 3.5293013  | \-0.3877290 | 0.6985492 |
|          countryAustralia:age35-54 years           | \-2.0383500  | 3.1039121  | \-0.6567035 | 0.5119805 |
|           countryAustria:age35-54 years            | \-1.9350747  | 2.3928755  | \-0.8086817 | 0.4194733 |
|           countryBahamas:age35-54 years            | \-0.2008051  | 2.6190826  | \-0.0766700 | 0.9389479 |
|           countryBahrain:age35-54 years            | \-0.2644574  | 1.4778689  | \-0.1789451 | 0.8581269 |
|           countryBarbados:age35-54 years           | \-0.9504552  | 2.5790981  | \-0.3685223 | 0.7127982 |
|           countryBelarus:age35-54 years            | \-0.8897944  | 1.7540042  | \-0.5072932 | 0.6123999 |
|           countryBelgium:age35-54 years            | \-1.2263600  | 2.2178143  | \-0.5529588 | 0.5807897 |
|            countryBelize:age35-54 years            | \-0.4051777  | 1.5012875  | \-0.2698868 | 0.7874718 |
|            countryBrazil:age35-54 years            | \-28.0453563 | 13.4019012 | \-2.0926401 | 0.0373979 |
|           countryBulgaria:age35-54 years           | \-2.5507595  | 2.2402574  | \-1.1386011 | 0.2559682 |
|            countryCanada:age35-54 years            | \-2.4891782  | 3.4118811  | \-0.7295618 | 0.4663466 |
|            countryChile:age35-54 years             |  2.7714676   | 2.4183834  |  1.1460001  | 0.2528997 |
|           countryColombia:age35-54 years           | \-1.5903662  | 3.5097096  | \-0.4531333 | 0.6508490 |
|          countryCosta Rica:age35-54 years          |  2.1816362   | 2.5576478  |  0.8529854  | 0.3944905 |
|           countryCroatia:age35-54 years            | \-1.7958454  | 2.0615892  | \-0.8710976 | 0.3845433 |
|             countryCuba:age35-54 years             | \-1.8799218  | 5.1472463  | \-0.3652286 | 0.7152520 |
|            countryCyprus:age35-54 years            | \-0.0417174  | 2.5521303  | \-0.0163461 | 0.9869714 |
|        countryCzech Republic:age35-54 years        | \-1.7357441  | 1.9533306  | \-0.8886074 | 0.3750752 |
|           countryDenmark:age35-54 years            | \-0.4432440  | 2.6250139  | \-0.1688540 | 0.8660492 |
|           countryEcuador:age35-54 years            | \-0.7060753  | 1.8909560  | \-0.3733960 | 0.7091727 |
|         countryEl Salvador:age35-54 years          | \-0.9935813  | 1.4663277  | \-0.6775984 | 0.4986580 |
|           countryEstonia:age35-54 years            | \-0.8733928  | 1.6051995  | \-0.5441023 | 0.5868599 |
|           countryFinland:age35-54 years            | \-1.0306578  | 1.8517585  | \-0.5565833 | 0.5783141 |
|            countryFrance:age35-54 years            | \-8.4292301  | 4.8948226  | \-1.7220706 | 0.0863035 |
|           countryGeorgia:age35-54 years            | \-3.9912247  | 1.8110784  | \-2.2037835 | 0.0284590 |
|           countryGermany:age35-54 years            | \-10.3797556 | 5.6476757  | \-1.8378810 | 0.0672761 |
|            countryGreece:age35-54 years            | \-0.9212539  | 2.5835925  | \-0.3565786 | 0.7217105 |
|           countryGrenada:age35-54 years            |  0.0607589   | 1.4970137  |  0.0405867  | 0.9676580 |
|          countryGuatemala:age35-54 years           | \-7.7655246  | 2.0337677  | \-3.8182948 | 0.0001698 |
|            countryGuyana:age35-54 years            |  1.0327149   | 1.7915264  |  0.5764441  | 0.5648378 |
|           countryHungary:age35-54 years            | \-1.1244520  | 1.8619826  | \-0.6039004 | 0.5464619 |
|           countryIceland:age35-54 years            |  0.7358262   | 2.8308161  |  0.2599343  | 0.7951301 |
|           countryIreland:age35-54 years            | \-0.5722455  | 3.4658508  | \-0.1651097 | 0.8689922 |
|            countryIsrael:age35-54 years            | \-0.9464794  | 1.9575195  | \-0.4835096 | 0.6291606 |
|            countryItaly:age35-54 years             | \-7.3534501  | 4.6286166  | \-1.5886929 | 0.1134038 |
|           countryJamaica:age35-54 years            | \-0.8650821  | 1.7410248  | \-0.4968809 | 0.6197132 |
|            countryJapan:age35-54 years             | \-11.9290370 | 7.3278292  | \-1.6279087 | 0.1048140 |
|          countryKazakhstan:age35-54 years          | \-0.6254191  | 1.9192145  | \-0.3258724 | 0.7447957 |
|            countryKuwait:age35-54 years            | \-0.4499897  | 1.5036706  | \-0.2992608 | 0.7649917 |
|          countryKyrgyzstan:age35-54 years          | \-0.9541692  | 1.4672616  | \-0.6503061 | 0.5160965 |
|            countryLatvia:age35-54 years            | \-1.0807841  | 1.5973776  | \-0.6765990 | 0.4992909 |
|          countryLithuania:age35-54 years           | \-1.0769474  | 1.6501644  | \-0.6526304 | 0.5145991 |
|          countryLuxembourg:age35-54 years          |  1.2577931   | 2.5540580  |  0.4924685  | 0.6228239 |
|           countryMaldives:age35-54 years           | \-0.0647456  | 1.4726157  | \-0.0439664 | 0.9649666 |
|            countryMalta:age35-54 years             | \-0.9009845  | 2.0304415  | \-0.4437382 | 0.6576188 |
|          countryMauritius:age35-54 years           |  3.9167635   | 2.7882794  |  1.4047242  | 0.1613546 |
|            countryMexico:age35-54 years            | \-14.3455845 | 8.0408259  | \-1.7840934 | 0.0756310 |
|         countryNetherlands:age35-54 years          | \-3.9610427  | 2.6398181  | \-1.5004983 | 0.1347574 |
|         countryNew Zealand:age35-54 years          |  0.3125064   | 2.7783546  |  0.1124789  | 0.9105347 |
|          countryNicaragua:age35-54 years           | \-2.0312720  | 1.4928416  | \-1.3606748 | 0.1748518 |
|            countryNorway:age35-54 years            | \-0.3737830  | 2.1821738  | \-0.1712893 | 0.8641360 |
|             countryOman:age35-54 years             | \-0.6411657  | 1.4474638  | \-0.4429580 | 0.6581822 |
|            countryPanama:age35-54 years            |  3.8575234   | 2.7055601  |  1.4257763  | 0.1551904 |
|           countryParaguay:age35-54 years           | \-1.5070477  | 1.5531569  | \-0.9703126 | 0.3328361 |
|         countryPhilippines:age35-54 years          | \-15.8634486 | 6.5305194  | \-2.4291251 | 0.0158465 |
|            countryPoland:age35-54 years            | \-5.0722402  | 2.8558703  | \-1.7760751 | 0.0769466 |
|           countryPortugal:age35-54 years           | \-4.4913685  | 4.1383451  | \-1.0853054 | 0.2788402 |
|         countryPuerto Rico:age35-54 years          |  1.5217054   | 2.3978249  |  0.6346191  | 0.5262619 |
|            countryQatar:age35-54 years             | \-0.7935823  | 1.5494745  | \-0.5121623 | 0.6089933 |
|      countryRepublic of Korea:age35-54 years       | \-7.7923781  | 4.4915911  | \-1.7348815 | 0.0840042 |
|           countryRomania:age35-54 years            | \-3.6325067  | 2.2498236  | \-1.6145740 | 0.1076745 |
|      countryRussian Federation:age35-54 years      | \-11.8358562 | 9.6968608  | \-1.2205864 | 0.2234019 |
|         countrySaint Lucia:age35-54 years          | \-0.3381759  | 3.3960667  | \-0.0995787 | 0.9207592 |
| countrySaint Vincent and Grenadines:age35-54 years | \-1.5151884  | 1.9066104  | \-0.7947027 | 0.4275463 |
|            countrySerbia:age35-54 years            | \-4.7770837  | 2.9782826  | \-1.6039726 | 0.1099928 |
|          countrySeychelles:age35-54 years          |  0.4471049   | 1.9210208  |  0.2327434  | 0.8161526 |
|          countrySingapore:age35-54 years           | \-1.5376709  | 4.6709450  | \-0.3291991 | 0.7422830 |
|           countrySlovakia:age35-54 years           | \-0.6372673  | 1.8553592  | \-0.3434738 | 0.7315330 |
|           countrySlovenia:age35-54 years           | \-0.1530251  | 1.9186351  | \-0.0797573 | 0.9364946 |
|         countrySouth Africa:age35-54 years         | \-8.6039899  | 3.6842158  | \-2.3353653 | 0.0203225 |
|            countrySpain:age35-54 years             | \-5.4488937  | 3.7051971  | \-1.4706084 | 0.1426647 |
|           countrySuriname:age35-54 years           |  1.3659860   | 1.9122591  |  0.7143310  | 0.4756943 |
|            countrySweden:age35-54 years            | \-0.9992956  | 2.0755991  | \-0.4814492 | 0.6306218 |
|         countrySwitzerland:age35-54 years          | \-0.9234454  | 2.5455535  | \-0.3627680 | 0.7170872 |
|           countryThailand:age35-54 years           | \-6.6672473  | 5.3336174  | \-1.2500423 | 0.2124624 |
|     countryTrinidad and Tobago:age35-54 years      |  6.3714069   | 2.8334601  |  2.2486313  | 0.0254144 |
|            countryTurkey:age35-54 years            | \-11.7927915 | 5.2323847  | \-2.2538082 | 0.0250820 |
|         countryTurkmenistan:age35-54 years         | \-0.4455705  | 1.4700435  | \-0.3031002 | 0.7620676 |
|           countryUkraine:age35-54 years            | \-5.0804828  | 3.3180047  | \-1.5311861 | 0.1269980 |
|     countryUnited Arab Emirates:age35-54 years     | \-3.1416106  | 1.7445253  | \-1.8008398 | 0.0729430 |
|        countryUnited Kingdom:age35-54 years        | \-7.8283637  | 4.3389191  | \-1.8042198 | 0.0724101 |
|        countryUnited States:age35-54 years         | \-37.3706932 | 22.6292813 | \-1.6514308 | 0.0999163 |
|           countryUruguay:age35-54 years            | \-0.4905561  | 1.7411713  | \-0.2817391 | 0.7783785 |
|          countryUzbekistan:age35-54 years          | \-5.1217603  | 2.4662620  | \-2.0767300 | 0.0388564 |
|           countryArgentina:age5-14 years           |  0.8679605   | 2.4991697  |  0.3472995  | 0.7286608 |
|            countryArmenia:age5-14 years            |  1.5335003   | 1.1823755  |  1.2969656  | 0.1958483 |
|             countryAruba:age5-14 years             |  0.8629820   | 0.7704815  |  1.1200554  | 0.2637737 |
|           countryAustralia:age5-14 years           | \-1.2725995  | 1.1510648  | \-1.1055846 | 0.2699777 |
|            countryAustria:age5-14 years            | \-1.0990171  | 0.7387862  | \-1.4875983 | 0.1381272 |
|            countryBahamas:age5-14 years            |  1.0506426   | 1.0155982  |  1.0345061  | 0.3019073 |
|            countryBahrain:age5-14 years            |  0.8904691   | 0.6967177  |  1.2780917  | 0.2024120 |
|           countryBarbados:age5-14 years            |  1.0175744   | 0.7070911  |  1.4390994  | 0.1513833 |
|            countryBelarus:age5-14 years            | \-1.8858040  | 0.7719892  | \-2.4427857 | 0.0152731 |
|            countryBelgium:age5-14 years            | \-1.0821194  | 0.7423707  | \-1.4576537 | 0.1462011 |
|            countryBelize:age5-14 years             | \-0.6400819  | 1.6390302  | \-0.3905248 | 0.6964838 |
|            countryBrazil:age5-14 years             |  6.3903253   | 12.4796360 |  0.5120602  | 0.6090645 |
|           countryBulgaria:age5-14 years            | \-0.6573949  | 0.7738807  | \-0.8494784 | 0.3964344 |
|            countryCanada:age5-14 years             | \-1.2974024  | 1.4962375  | \-0.8671099 | 0.3867200 |
|             countryChile:age5-14 years             | \-1.5460581  | 1.0841969  | \-1.4259938 | 0.1551276 |
|           countryColombia:age5-14 years            | \-0.8448387  | 2.9514941  | \-0.2862410 | 0.7749325 |
|          countryCosta Rica:age5-14 years           | \-1.4125256  | 0.8179696  | \-1.7268680 | 0.0854365 |
|            countryCroatia:age5-14 years            | \-1.2023194  | 0.7104195  | \-1.6924077 | 0.0918241 |
|             countryCuba:age5-14 years              | \-0.3610512  | 0.9058638  | \-0.3985712 | 0.6905521 |
|            countryCyprus:age5-14 years             |  0.3277780   | 1.2180381  |  0.2691032  | 0.7880740 |
|        countryCzech Republic:age5-14 years         | \-1.7812890  | 0.7630625  | \-2.3343945 | 0.0203741 |
|            countryDenmark:age5-14 years            | \-1.2596601  | 0.6921996  | \-1.8197932 | 0.0699961 |
|            countryEcuador:age5-14 years            |  0.9562388   | 1.2699557  |  0.7529702  | 0.4521820 |
|          countryEl Salvador:age5-14 years          | \-0.3539503  | 0.8447513  | \-0.4189994 | 0.6755792 |
|            countryEstonia:age5-14 years            | \-0.2389240  | 0.7280538  | \-0.3281680 | 0.7430615 |
|            countryFinland:age5-14 years            | \-2.0980080  | 0.7158216  | \-2.9309090 | 0.0036952 |
|            countryFrance:age5-14 years             |  0.5882396   | 2.7659661  |  0.2126706  | 0.8317586 |
|            countryGeorgia:age5-14 years            |  2.0316830   | 0.7995833  |  2.5409272  | 0.0116663 |
|            countryGermany:age5-14 years            | \-0.7584724  | 2.8591273  | \-0.2652811 | 0.7910133 |
|            countryGreece:age5-14 years             | \-0.7027824  | 0.7300615  | \-0.9626345 | 0.3366686 |
|            countryGrenada:age5-14 years            |  1.1724066   | 0.9692872  |  1.2095555  | 0.2276013 |
|           countryGuatemala:age5-14 years           |  3.4491068   | 1.4980363  |  2.3024187  | 0.0221403 |
|            countryGuyana:age5-14 years             |  1.3657976   | 1.2070425  |  1.1315241  | 0.2589275 |
|            countryHungary:age5-14 years            | \-1.3047001  | 0.7330818  | \-1.7797470 | 0.0763419 |
|            countryIceland:age5-14 years            |  0.2252659   | 0.7579731  |  0.2971951  | 0.7665663 |
|            countryIreland:age5-14 years            | \-0.4023429  | 0.7012170  | \-0.5737780 | 0.5666380 |
|            countryIsrael:age5-14 years             |  0.0622863   | 0.8441896  |  0.0737824  | 0.9412430 |
|             countryItaly:age5-14 years             | \-0.2550128  | 2.0707053  | \-0.1231526 | 0.9020860 |
|            countryJamaica:age5-14 years            |  0.9903967   | 0.7025206  |  1.4097760  | 0.1598587 |
|             countryJapan:age5-14 years             |  0.7309326   | 4.1643800  |  0.1755202  | 0.8608142 |
|          countryKazakhstan:age5-14 years           | \-2.9446718  | 1.2340237  | \-2.3862359 | 0.0177727 |
|            countryKuwait:age5-14 years             |  0.7777052   | 0.7119331  |  1.0923852  | 0.2757239 |
|          countryKyrgyzstan:age5-14 years           | \-1.0646725  | 0.8847612  | \-1.2033445 | 0.2299905 |
|            countryLatvia:age5-14 years             | \-0.6845026  | 0.7270795  | \-0.9414412 | 0.3473949 |
|           countryLithuania:age5-14 years           | \-1.1055551  | 0.7254095  | \-1.5240427 | 0.1287722 |
|          countryLuxembourg:age5-14 years           |  0.7455423   | 0.7054645  |  1.0568105  | 0.2916264 |
|           countryMaldives:age5-14 years            |  1.1763406   | 0.8454679  |  1.3913485  | 0.1653666 |
|             countryMalta:age5-14 years             |  0.7917743   | 0.7857693  |  1.0076422  | 0.3146084 |
|           countryMauritius:age5-14 years           | \-0.6406860  | 0.7411088  | \-0.8644966 | 0.3881505 |
|            countryMexico:age5-14 years             |  5.4051069   | 8.3115143  |  0.6503155  | 0.5160904 |
|          countryNetherlands:age5-14 years          | \-1.0289609  | 0.8886586  | \-1.1578810 | 0.2480265 |
|          countryNew Zealand:age5-14 years          | \-0.9376705  | 0.8089855  | \-1.1590696 | 0.2475426 |
|           countryNicaragua:age5-14 years           | \-0.6182809  | 0.8054924  | \-0.7675813 | 0.4434661 |
|            countryNorway:age5-14 years             | \-1.7091846  | 0.7462879  | \-2.2902484 | 0.0228470 |
|             countryOman:age5-14 years              |  1.0647560   | 0.7001075  |  1.5208463  | 0.1295723 |
|            countryPanama:age5-14 years             |  0.7750111   | 0.9080742  |  0.8534667  | 0.3942241 |
|           countryParaguay:age5-14 years            |  0.8330446   | 1.1552257  |  0.7211098  | 0.4715212 |
|          countryPhilippines:age5-14 years          |  6.2621176   | 6.9573705  |  0.9000696  | 0.3689564 |
|            countryPoland:age5-14 years             | \-1.3589129  | 1.5968132  | \-0.8510156 | 0.3955816 |
|           countryPortugal:age5-14 years            | \-0.6519047  | 0.7380052  | \-0.8833335 | 0.3779116 |
|          countryPuerto Rico:age5-14 years          | \-1.1012575  | 0.7375709  | \-1.4930868 | 0.1366856 |
|             countryQatar:age5-14 years             |  0.8682818   | 0.7084605  |  1.2255896  | 0.2215158 |
|       countryRepublic of Korea:age5-14 years       | \-0.8462707  | 2.1542964  | \-0.3928293 | 0.6947830 |
|            countryRomania:age5-14 years            | \-0.7806420  | 1.0315820  | \-0.7567425 | 0.4499224 |
|      countryRussian Federation:age5-14 years       | \-6.4496287  | 5.9433451  | \-1.0851850 | 0.2788935 |
|          countrySaint Lucia:age5-14 years          |  1.1129305   | 0.8691921  |  1.2804195  | 0.2015939 |
| countrySaint Vincent and Grenadines:age5-14 years  |  1.3235038   | 0.7210731  |  1.8354643  | 0.0676343 |
|            countrySerbia:age5-14 years             | \-0.6967168  | 0.7598640  | \-0.9168967 | 0.3600875 |
|          countrySeychelles:age5-14 years           |  0.9529343   | 0.7327268  |  1.3005315  | 0.1946261 |
|           countrySingapore:age5-14 years           | \-0.5285314  | 0.7523188  | \-0.7025366 | 0.4830035 |
|           countrySlovakia:age5-14 years            | \-0.3184712  | 0.7594786  | \-0.4193287 | 0.6753389 |
|           countrySlovenia:age5-14 years            | \-0.0488704  | 0.7138693  | \-0.0684584 | 0.9454759 |
|         countrySouth Africa:age5-14 years          |  2.2768688   | 3.7434674  |  0.6082246  | 0.5435952 |
|             countrySpain:age5-14 years             | \-0.9492645  | 1.6571752  | \-0.5728208 | 0.5672850 |
|           countrySuriname:age5-14 years            |  0.5298382   | 0.7680007  |  0.6898928  | 0.4909067 |
|            countrySweden:age5-14 years             | \-1.4465626  | 0.7760657  | \-1.8639693 | 0.0635076 |
|          countrySwitzerland:age5-14 years          | \-1.3617547  | 0.7227537  | \-1.8841200 | 0.0607185 |
|           countryThailand:age5-14 years            |  0.1284371   | 3.2332675  |  0.0397236  | 0.9683454 |
|      countryTrinidad and Tobago:age5-14 years      | \-2.3116108  | 0.9899776  | \-2.3350132 | 0.0203412 |
|            countryTurkey:age5-14 years             |  2.7288942   | 4.5256871  |  0.6029790  | 0.5470737 |
|         countryTurkmenistan:age5-14 years          | \-2.0858383  | 0.9876745  | \-2.1118681 | 0.0356981 |
|            countryUkraine:age5-14 years            | \-2.4504500  | 1.8492914  | \-1.3250751 | 0.1863658 |
|     countryUnited Arab Emirates:age5-14 years      | \-0.9423834  | 0.9581665  | \-0.9835278 | 0.3263062 |
|        countryUnited Kingdom:age5-14 years         | \-1.3693966  | 2.6576668  | \-0.5152627 | 0.6068284 |
|         countryUnited States:age5-14 years         |  6.6645431   | 15.0451998 |  0.4429681  | 0.6581750 |
|            countryUruguay:age5-14 years            | \-0.2326925  | 0.7449930  | \-0.3123419 | 0.7550432 |
|          countryUzbekistan:age5-14 years           | \-2.1482442  | 2.3277161  | \-0.9228978 | 0.3569575 |
|          countryArgentina:age55-74 years           | \-5.5259310  | 2.3379967  | \-2.3635324 | 0.0188736 |
|           countryArmenia:age55-74 years            |  0.5301240   | 0.5672973  |  0.9344730  | 0.3509689 |
|            countryAruba:age55-74 years             |  0.4894843   | 1.2666478  |  0.3864407  | 0.6995016 |
|          countryAustralia:age55-74 years           | \-1.6478298  | 1.3998558  | \-1.1771426 | 0.2402671 |
|           countryAustria:age55-74 years            | \-0.1913155  | 1.1018020  | \-0.1736387 | 0.8622911 |
|           countryBahamas:age55-74 years            |  1.0262753   | 1.1271909  |  0.9104716  | 0.3634579 |
|           countryBahrain:age55-74 years            |  0.7304379   | 0.7425063  |  0.9837464  | 0.3261990 |
|           countryBarbados:age55-74 years           |  0.6091027   | 0.7759625  |  0.7849641  | 0.4332238 |
|           countryBelarus:age55-74 years            |  0.0087925   | 0.6685784  |  0.0131510  | 0.9895179 |
|           countryBelgium:age55-74 years            |  0.0021127   | 1.0377193  |  0.0020359  | 0.9983772 |
|            countryBelize:age55-74 years            |  7.1431665   | 5.6386986  |  1.2668112  | 0.2064112 |
|            countryBrazil:age55-74 years            | \-30.3412860 | 12.0756173 | \-2.5126075 | 0.0126198 |
|           countryBulgaria:age55-74 years           | \-0.9574448  | 1.4348140  | \-0.6672954 | 0.5052039 |
|            countryCanada:age55-74 years            | \-2.4957605  | 1.9347687  | \-1.2899529 | 0.1982686 |
|            countryChile:age55-74 years             | \-2.6953262  | 1.0193609  | \-2.6441333 | 0.0087124 |
|           countryColombia:age55-74 years           | \-13.9162378 | 3.1002679  | \-4.4887211 | 0.0000110 |
|          countryCosta Rica:age55-74 years          | \-1.7725094  | 1.6576315  | \-1.0693025 | 0.2859731 |
|           countryCroatia:age55-74 years            | \-0.4376074  | 1.1987164  | \-0.3650634 | 0.7153752 |
|             countryCuba:age55-74 years             |  0.1090329   | 1.2196885  |  0.0893941  | 0.9288409 |
|            countryCyprus:age55-74 years            |  0.5783053   | 0.7493288  |  0.7717643  | 0.4409888 |
|        countryCzech Republic:age55-74 years        | \-0.5173889  | 1.0558885  | \-0.4900034 | 0.6245647 |
|           countryDenmark:age55-74 years            |  0.5990202   | 1.5508264  |  0.3862587  | 0.6996362 |
|           countryEcuador:age55-74 years            | \-6.9269720  | 2.8055707  | \-2.4690064 | 0.0142236 |
|         countryEl Salvador:age55-74 years          | \-4.9775999  | 1.6603652  | \-2.9978946 | 0.0029948 |
|           countryEstonia:age55-74 years            |  0.5245796   | 0.7094743  |  0.7393921  | 0.4603682 |
|           countryFinland:age55-74 years            | \-0.0996226  | 1.0947855  | \-0.0909974 | 0.9275681 |
|            countryFrance:age55-74 years            | \-6.8766171  | 3.3333033  | \-2.0630037 | 0.0401534 |
|           countryGeorgia:age55-74 years            | \-0.3428066  | 0.6681963  | \-0.5130327 | 0.6083851 |
|           countryGermany:age55-74 years            | \-9.1969350  | 4.0099722  | \-2.2935159 | 0.0226553 |
|            countryGreece:age55-74 years            |  0.0023692   | 1.4021138  |  0.0016897  | 0.9986532 |
|           countryGrenada:age55-74 years            |  1.5354352   | 2.0966467  |  0.7323290  | 0.4646593 |
|          countryGuatemala:age55-74 years           | \-14.6913788 | 2.9798899  | \-4.9301750 | 0.0000015 |
|            countryGuyana:age55-74 years            | \-2.5686668  | 1.9804839  | \-1.2969895 | 0.1958402 |
|           countryHungary:age55-74 years            |  0.0858544   | 1.0067453  |  0.0852792  | 0.9321083 |
|           countryIceland:age55-74 years            |  1.1689196   | 0.6998116  |  1.6703349  | 0.0961147 |
|           countryIreland:age55-74 years            |  0.5087545   | 1.0226122  |  0.4975049  | 0.6192739 |
|            countryIsrael:age55-74 years            |  0.0442031   | 0.5868934  |  0.0753170  | 0.9400232 |
|            countryItaly:age55-74 years             | \-5.6564401  | 2.8316132  | \-1.9976034 | 0.0468521 |
|           countryJamaica:age55-74 years            |  0.9140854   | 1.5198563  |  0.6014289  | 0.5481037 |
|            countryJapan:age55-74 years             | \-12.6575223 | 5.8727362  | \-2.1553024 | 0.0321009 |
|          countryKazakhstan:age55-74 years          | \-3.5699722  | 1.3142611  | \-2.7163340 | 0.0070655 |
|            countryKuwait:age55-74 years            |  0.5740111   | 0.6547743  |  0.8766549  | 0.3815225 |
|          countryKyrgyzstan:age55-74 years          | \-3.0412019  | 2.4004848  | \-1.2669115 | 0.2063754 |
|            countryLatvia:age55-74 years            |  0.5719856   | 0.6759127  |  0.8462418  | 0.3982337 |
|          countryLithuania:age55-74 years           |  0.4745468   | 0.6333916  |  0.7492155  | 0.4544374 |
|          countryLuxembourg:age55-74 years          |  1.5770270   | 0.8883152  |  1.7753011  | 0.0770746 |
|           countryMaldives:age55-74 years           |  1.6685806   | 1.2332319  |  1.3530146  | 0.1772831 |
|            countryMalta:age55-74 years             |  0.8920292   | 1.2114623  |  0.7363243  | 0.4622292 |
|          countryMauritius:age55-74 years           |  0.3207176   | 0.6174188  |  0.5194489  | 0.6039110 |
|            countryMexico:age55-74 years            | \-27.9674161 | 7.3158511  | \-3.8228520 | 0.0001669 |
|         countryNetherlands:age55-74 years          | \-1.8388502  | 1.3702564  | \-1.3419752 | 0.1808314 |
|         countryNew Zealand:age55-74 years          |  0.3567641   | 0.7869605  |  0.4533443  | 0.6506972 |
|          countryNicaragua:age55-74 years           | \-7.5458255  | 2.0823857  | \-3.6236445 | 0.0003523 |
|            countryNorway:age55-74 years            |  0.6455658   | 0.8995575  |  0.7176482  | 0.4736497 |
|             countryOman:age55-74 years             |  1.6938207   | 0.7311525  |  2.3166449  | 0.0213386 |
|            countryPanama:age55-74 years            | \-4.9376504  | 2.2767774  | \-2.1687015 | 0.0310562 |
|           countryParaguay:age55-74 years           | \-4.1325136  | 4.3095852  | \-0.9589121 | 0.3385369 |
|         countryPhilippines:age55-74 years          | \-15.6076630 | 5.8590237  | \-2.6638675 | 0.0082310 |
|            countryPoland:age55-74 years            | \-3.7290639  | 1.9859242  | \-1.8777474 | 0.0615893 |
|           countryPortugal:age55-74 years           | \-2.1589882  | 2.5801042  | \-0.8367833 | 0.4035200 |
|         countryPuerto Rico:age55-74 years          |  1.4082299   | 0.7484996  |  1.8814036  | 0.0610884 |
|            countryQatar:age55-74 years             |  1.3188872   | 0.5462835  |  2.4142908  | 0.0164908 |
|      countryRepublic of Korea:age55-74 years       | \-5.5378544  | 2.5537968  | \-2.1684788 | 0.0310733 |
|           countryRomania:age55-74 years            | \-1.8849717  | 1.2429008  | \-1.5165907 | 0.1306437 |
|      countryRussian Federation:age55-74 years      | \-14.4903587 | 7.3622766  | \-1.9681899 | 0.0501602 |
|         countrySaint Lucia:age55-74 years          |  1.0301996   | 2.0927182  |  0.4922782  | 0.6229582 |
| countrySaint Vincent and Grenadines:age55-74 years |  2.8438226   | 1.5603529  |  1.8225509  | 0.0695756 |
|            countrySerbia:age55-74 years            | \-3.0303012  | 2.3174876  | \-1.3075804 | 0.1922266 |
|          countrySeychelles:age55-74 years          |  0.7247411   | 0.8050341  |  0.9002613  | 0.3688546 |
|          countrySingapore:age55-74 years           |  0.6613661   | 0.9990147  |  0.6620184  | 0.5085741 |
|           countrySlovakia:age55-74 years           |  0.6316614   | 0.6875455  |  0.9187194  | 0.3591350 |
|           countrySlovenia:age55-74 years           |  1.4972344   | 0.9231987  |  1.6217899  | 0.1061189 |
|         countrySouth Africa:age55-74 years         | \-10.1242662 | 3.7033222  | \-2.7338335 | 0.0067113 |
|            countrySpain:age55-74 years             | \-3.3999105  | 2.0981376  | \-1.6204421 | 0.1064081 |
|           countrySuriname:age55-74 years           | \-0.8586166  | 1.2715908  | \-0.6752303 | 0.5001585 |
|            countrySweden:age55-74 years            | \-0.1603431  | 1.1763026  | \-0.1363111 | 0.8916860 |
|         countrySwitzerland:age55-74 years          |  0.5195287   | 1.1942941  |  0.4350090  | 0.6639342 |
|           countryThailand:age55-74 years           | \-7.4092196  | 3.3190140  | \-2.2323557 | 0.0264849 |
|     countryTrinidad and Tobago:age55-74 years      | \-0.5365627  | 0.6469325  | \-0.8293952 | 0.4076784 |
|            countryTurkey:age55-74 years            | \-9.5205850  | 4.1583482  | \-2.2895113 | 0.0228904 |
|         countryTurkmenistan:age55-74 years         | \-9.9900721  | 2.8760530  | \-3.4735354 | 0.0006060 |
|           countryUkraine:age55-74 years            | \-4.3938693  | 2.2882482  | \-1.9201891 | 0.0559810 |
|     countryUnited Arab Emirates:age55-74 years     |  1.3014469   | 0.6191707  |  2.1019193  | 0.0365691 |
|        countryUnited Kingdom:age55-74 years        | \-6.7607678  | 3.2234837  | \-2.0973482 | 0.0369754 |
|        countryUnited States:age55-74 years         | \-37.9439555 | 16.9667792 | \-2.2363676 | 0.0262174 |
|           countryUruguay:age55-74 years            |  0.3846521   | 0.6129195  |  0.6275737  | 0.5308607 |
|          countryUzbekistan:age55-74 years          | \-11.1187638 | 4.0942357  | \-2.7157117 | 0.0070784 |
|           countryArgentina:age75+ years            | \-7.1178444  | 3.7183700  | \-1.9142378 | 0.0567406 |
|            countryArmenia:age75+ years             |  2.9924171   | 3.1072560  |  0.9630417  | 0.3364647 |
|             countryAruba:age75+ years              |  2.5950746   | 2.8285514  |  0.9174571  | 0.3597945 |
|           countryAustralia:age75+ years            | \-1.1650445  | 3.0134009  | \-0.3866212 | 0.6993682 |
|            countryAustria:age75+ years             |  2.0208105   | 2.5984808  |  0.7776892  | 0.4374935 |
|            countryBahamas:age75+ years             |  2.6860470   | 3.9715399  |  0.6763238  | 0.4994653 |
|            countryBahrain:age75+ years             |  2.6358209   | 2.6582764  |  0.9915526  | 0.3223823 |
|            countryBarbados:age75+ years            |  2.1313253   | 2.7264334  |  0.7817265  | 0.4351210 |
|            countryBelarus:age75+ years             |  1.0447470   | 2.6193969  |  0.3988502  | 0.6903468 |
|            countryBelgium:age75+ years             |  1.3395689   | 2.6058091  |  0.5140702  | 0.6076606 |
|             countryBelize:age75+ years             |  11.2206544  | 8.3895766  |  1.3374518  | 0.1823005 |
|             countryBrazil:age75+ years             | \-29.9261867 | 11.9285535 | \-2.5087859 | 0.0127536 |
|            countryBulgaria:age75+ years            |  2.6950666   | 2.5885429  |  1.0411520  | 0.2988189 |
|             countryCanada:age75+ years             | \-2.7942374  | 3.0871872  | \-0.9051079 | 0.3662867 |
|             countryChile:age75+ years              | \-7.0007770  | 3.3265501  | \-2.1045157 | 0.0363401 |
|            countryColombia:age75+ years            | \-20.4195364 | 4.6969342  | \-4.3474180 | 0.0000201 |
|           countryCosta Rica:age75+ years           | \-4.6835505  | 4.8535431  | \-0.9649756 | 0.3354971 |
|            countryCroatia:age75+ years             |  2.2671992   | 2.5871798  |  0.8763207  | 0.3817037 |
|              countryCuba:age75+ years              |  1.8613354   | 3.2835566  |  0.5668656  | 0.5713182 |
|             countryCyprus:age75+ years             |  1.1984093   | 3.1459829  |  0.3809332  | 0.7035789 |
|         countryCzech Republic:age75+ years         |  1.6098373   | 2.6186875  |  0.6147497  | 0.5392837 |
|            countryDenmark:age75+ years             |  2.0859589   | 2.6471034  |  0.7880156  | 0.4314401 |
|            countryEcuador:age75+ years             | \-10.5320996 | 5.4381393  | \-1.9367102 | 0.0539167 |
|          countryEl Salvador:age75+ years           | \-7.5330492  | 3.7728579  | \-1.9966427 | 0.0469571 |
|            countryEstonia:age75+ years             |  2.5037481   | 2.5812860  |  0.9699615  | 0.3330107 |
|            countryFinland:age75+ years             |  1.0624649   | 2.5913465  |  0.4100049  | 0.6821563 |
|             countryFrance:age75+ years             | \-3.6026142  | 3.8201573  | \-0.9430539 | 0.3465711 |
|            countryGeorgia:age75+ years             |  4.6790369   | 2.6544452  |  1.7627174  | 0.0791799 |
|            countryGermany:age75+ years             | \-4.6527992  | 4.2627139  | \-1.0915110 | 0.2761074 |
|             countryGreece:age75+ years             |  0.9113570   | 2.5854631  |  0.3524928  | 0.7247681 |
|            countryGrenada:age75+ years             |  3.0264515   | 3.9479661  |  0.7665850  | 0.4440574 |
|           countryGuatemala:age75+ years            | \-18.4904287 | 4.5761473  | \-4.0406104 | 0.0000712 |
|             countryGuyana:age75+ years             | \-4.2425661  | 4.3580667  | \-0.9734973 | 0.3312548 |
|            countryHungary:age75+ years             |  2.1868609   | 2.5998093  |  0.8411620  | 0.4010675 |
|            countryIceland:age75+ years             |  1.1384505   | 3.1098283  |  0.3660815  | 0.7146164 |
|            countryIreland:age75+ years             |  0.6901672   | 3.0898981  |  0.2233625  | 0.8234373 |
|             countryIsrael:age75+ years             |  1.1182025   | 3.1178413  |  0.3586464  | 0.7201648 |
|             countryItaly:age75+ years              | \-1.9889233  | 3.3743604  | \-0.5894223 | 0.5561146 |
|            countryJamaica:age75+ years             |  2.4872416   | 3.8114518  |  0.6525707  | 0.5146375 |
|             countryJapan:age75+ years              | \-7.7101443  | 5.5611360  | \-1.3864333 | 0.1668597 |
|           countryKazakhstan:age75+ years           | \-5.2239748  | 3.2828351  | \-1.5912998 | 0.1128160 |
|             countryKuwait:age75+ years             |  2.9024689   | 2.6116320  |  1.1113622  | 0.2674888 |
|           countryKyrgyzstan:age75+ years           | \-3.2634915  | 4.1767362  | \-0.7813497 | 0.4353421 |
|             countryLatvia:age75+ years             |  2.2894615   | 2.5813651  |  0.8869189  | 0.3759818 |
|           countryLithuania:age75+ years            |  2.1262453   | 2.5851939  |  0.8224703  | 0.4115994 |
|           countryLuxembourg:age75+ years           |  2.0177248   | 2.6337124  |  0.7661143  | 0.4443369 |
|            countryMaldives:age75+ years            |  3.6135127   | 2.9678132  |  1.2175674  | 0.2245456 |
|             countryMalta:age75+ years              |  1.8711896   | 2.6815506  |  0.6978013  | 0.4859552 |
|           countryMauritius:age75+ years            | \-2.0695289  | 3.4487111  | \-0.6000876 | 0.5489958 |
|             countryMexico:age75+ years             | \-34.2188173 | 7.8879694  | \-4.3381022 | 0.0000209 |
|          countryNetherlands:age75+ years           |  1.3297685   | 2.7016253  |  0.4922106  | 0.6230059 |
|          countryNew Zealand:age75+ years           |  0.0283810   | 2.9886988  |  0.0094961  | 0.9924310 |
|           countryNicaragua:age75+ years            | \-9.8632738  | 3.7743101  | \-2.6132653 | 0.0095162 |
|             countryNorway:age75+ years             |  1.1171953   | 2.6404290  |  0.4231113  | 0.6725807 |
|              countryOman:age75+ years              |  3.7911843   | 2.6579309  |  1.4263667  | 0.1550201 |
|             countryPanama:age75+ years             | \-8.5891398  | 5.4626020  | \-1.5723532 | 0.1171435 |
|            countryParaguay:age75+ years            | \-5.6573608  | 7.4478614  | \-0.7595953 | 0.4482179 |
|          countryPhilippines:age75+ years           | \-14.2697547 | 6.6733683  | \-2.1383137 | 0.0334688 |
|             countryPoland:age75+ years             | \-1.5340673  | 3.1695584  | \-0.4840003 | 0.6288127 |
|            countryPortugal:age75+ years            |  1.6361289   | 2.5899552  |  0.6317209  | 0.5281511 |
|          countryPuerto Rico:age75+ years           |  0.3195387   | 2.9039017  |  0.1100377  | 0.9124685 |
|             countryQatar:age75+ years              |  4.3371337   | 2.5962509  |  1.6705372  | 0.0960746 |
|       countryRepublic of Korea:age75+ years        | \-2.2286051  | 3.4099308  | \-0.6535631 | 0.5139988 |
|            countryRomania:age75+ years             |  0.4485934   | 2.7767391  |  0.1615540  | 0.8717886 |
|       countryRussian Federation:age75+ years       | \-16.3900632 | 8.0298139  | \-2.0411511 | 0.0422945 |
|          countrySaint Lucia:age75+ years           |  2.7664675   | 5.5828353  |  0.4955309  | 0.6206642 |
|  countrySaint Vincent and Grenadines:age75+ years  |  6.1213661   | 3.9061005  |  1.5671297  | 0.1183594 |
|             countrySerbia:age75+ years             |  3.5377182   | 2.6113165  |  1.3547642  | 0.1767255 |
|           countrySeychelles:age75+ years           |  1.6943646   | 2.8962718  |  0.5850157  | 0.5590690 |
|           countrySingapore:age75+ years            |  2.9230950   | 3.3477548  |  0.8731509  | 0.3834255 |
|            countrySlovakia:age75+ years            |  2.0276211   | 2.6552318  |  0.7636324  | 0.4458122 |
|            countrySlovenia:age75+ years            |  3.0437654   | 2.5827498  |  1.1784980  | 0.2397276 |
|          countrySouth Africa:age75+ years          | \-9.8267126  | 4.8065277  | \-2.0444515 | 0.0419651 |
|             countrySpain:age75+ years              | \-0.5767764  | 3.0603684  | \-0.1884663 | 0.8506652 |
|            countrySuriname:age75+ years            | \-1.0330342  | 3.5390912  | \-0.2918925 | 0.7706128 |
|             countrySweden:age75+ years             |  0.7328703   | 2.6283801  |  0.2788297  | 0.7806079 |
|          countrySwitzerland:age75+ years           |  1.9031670   | 2.5990933  |  0.7322427  | 0.4647119 |
|            countryThailand:age75+ years            | \-7.0390230  | 4.3480843  | \-1.6188791 | 0.1067443 |
|      countryTrinidad and Tobago:age75+ years       | \-7.3244547  | 3.9466149  | \-1.8558828 | 0.0646565 |
|             countryTurkey:age75+ years             | \-6.8888539  | 5.0153859  | \-1.3735441 | 0.1708236 |
|          countryTurkmenistan:age75+ years          | \-13.3611293 | 4.7458864  | \-2.8153074 | 0.0052645 |
|            countryUkraine:age75+ years             | \-2.9191792  | 3.4033777  | \-0.8577300 | 0.3918697 |
|      countryUnited Arab Emirates:age75+ years      |  3.3894636   | 2.5842880  |  1.3115657  | 0.1908796 |
|         countryUnited Kingdom:age75+ years         | \-4.6986589  | 3.8557426  | \-1.2186132 | 0.2241490 |
|         countryUnited States:age75+ years          | \-33.8646513 | 16.3348693 | \-2.0731510 | 0.0391910 |
|            countryUruguay:age75+ years             |  1.5619912   | 2.6786287  |  0.5831309  | 0.5603351 |
|           countryUzbekistan:age75+ years           | \-13.2926749 | 5.9092188  | \-2.2494809 | 0.0253596 |
|           countryArgentina:suicides\_no            | \-0.1105852  | 0.0335823  | \-3.2929626 | 0.0011358 |
|            countryArmenia:suicides\_no             |  0.0652636   | 0.0957715  |  0.6814509  | 0.4962221 |
|             countryAruba:suicides\_no              |  0.4504267   | 0.1839131  |  2.4491278  | 0.0150131 |
|           countryAustralia:suicides\_no            | \-0.1102024  | 0.0335648  | \-3.2832700 | 0.0011739 |
|            countryAustria:suicides\_no             | \-0.1082976  | 0.0335709  | \-3.2259424 | 0.0014245 |
|            countryBahamas:suicides\_no             |  0.4674172   | 0.2088257  |  2.2383129  | 0.0260886 |
|            countryBahrain:suicides\_no             |  0.4197138   | 0.1945267  |  2.1576160  | 0.0319183 |
|            countryBarbados:suicides\_no            |  0.5279980   | 0.1648695  |  3.2025204  | 0.0015405 |
|            countryBelarus:suicides\_no             | \-0.1103575  | 0.0335659  | \-3.2877898 | 0.0011560 |
|            countryBelgium:suicides\_no             | \-0.1106194  | 0.0335684  | \-3.2953408 | 0.0011267 |
|             countryBelize:suicides\_no             |  0.3608408   | 0.1342054  |  2.6887207  | 0.0076589 |
|             countryBrazil:suicides\_no             | \-0.1120376  | 0.0335886  | \-3.3355850 | 0.0009816 |
|            countryBulgaria:suicides\_no            | \-0.1055323  | 0.0336530  | \-3.1358951 | 0.0019200 |
|             countryCanada:suicides\_no             | \-0.1107233  | 0.0335682  | \-3.2984612 | 0.0011147 |
|             countryChile:suicides\_no              | \-0.1101160  | 0.0335681  | \-3.2803792 | 0.0011855 |
|            countryColombia:suicides\_no            | \-0.1131862  | 0.0335860  | \-3.3700381 | 0.0008715 |
|           countryCosta Rica:suicides\_no           | \-0.1090338  | 0.0339069  | \-3.2156800 | 0.0014743 |
|            countryCroatia:suicides\_no             | \-0.1018634  | 0.0336165  | \-3.0301628 | 0.0027029 |
|              countryCuba:suicides\_no              | \-0.1083550  | 0.0335608  | \-3.2286166 | 0.0014118 |
|             countryCyprus:suicides\_no             |  0.1155725   | 0.0880187  |  1.3130446  | 0.1903815 |
|         countryCzech Republic:suicides\_no         | \-0.1093249  | 0.0335555  | \-3.2580341 | 0.0012787 |
|            countryDenmark:suicides\_no             | \-0.1021242  | 0.0337753  | \-3.0236342 | 0.0027598 |
|            countryEcuador:suicides\_no             | \-0.1057157  | 0.0336947  | \-3.1374586 | 0.0019102 |
|          countryEl Salvador:suicides\_no           | \-0.1104200  | 0.0349945  | \-3.1553559 | 0.0018010 |
|            countryEstonia:suicides\_no             | \-0.0774653  | 0.0344552  | \-2.2482877 | 0.0254367 |
|            countryFinland:suicides\_no             | \-0.1081648  | 0.0335996  | \-3.2192269 | 0.0014569 |
|             countryFrance:suicides\_no             | \-0.1113025  | 0.0335786  | \-3.3146883 | 0.0010546 |
|            countryGeorgia:suicides\_no             | \-0.0220031  | 0.0382608  | \-0.5750828 | 0.5657566 |
|            countryGermany:suicides\_no             | \-0.1115589  | 0.0335789  | \-3.3222880 | 0.0010275 |
|             countryGreece:suicides\_no             | \-0.0936712  | 0.0337171  | \-2.7781547 | 0.0058849 |
|           countryGuatemala:suicides\_no            | \-0.1270199  | 0.0346979  | \-3.6607353 | 0.0003073 |
|             countryGuyana:suicides\_no             | \-0.0773987  | 0.0340260  | \-2.2746927 | 0.0237788 |
|            countryHungary:suicides\_no             | \-0.1100551  | 0.0335625  | \-3.2791063 | 0.0011906 |
|            countryIceland:suicides\_no             | \-0.0504765  | 0.0941475  | \-0.5361432 | 0.5923401 |
|            countryIreland:suicides\_no             | \-0.0994827  | 0.0336964  | \-2.9523285 | 0.0034564 |
|             countryIsrael:suicides\_no             | \-0.0936011  | 0.0339295  | \-2.7586928 | 0.0062357 |
|             countryItaly:suicides\_no              | \-0.1116426  | 0.0335726  | \-3.3254031 | 0.0010166 |
|            countryJamaica:suicides\_no             |  0.9188381   | 0.3259958  |  2.8185578  | 0.0052131 |
|             countryJapan:suicides\_no              | \-0.1115877  | 0.0335841  | \-3.3226361 | 0.0010263 |
|           countryKazakhstan:suicides\_no           | \-0.1104927  | 0.0335773  | \-3.2906960 | 0.0011446 |
|             countryKuwait:suicides\_no             |  0.2441590   | 0.1515830  |  1.6107280  | 0.1085110 |
|           countryKyrgyzstan:suicides\_no           | \-0.1005487  | 0.0337291  | \-2.9810654 | 0.0031583 |
|             countryLatvia:suicides\_no             | \-0.0971527  | 0.0336522  | \-2.8869629 | 0.0042329 |
|           countryLithuania:suicides\_no            | \-0.1056457  | 0.0335637  | \-3.1476181 | 0.0018475 |
|           countryLuxembourg:suicides\_no           | \-0.0355064  | 0.0418184  | \-0.8490633 | 0.3966649 |
|            countryMaldives:suicides\_no            |  0.4207086   | 0.4966591  |  0.8470771  | 0.3977688 |
|             countryMalta:suicides\_no              |  0.0596230   | 0.0442523  |  1.3473412  | 0.1791001 |
|           countryMauritius:suicides\_no            | \-0.0583356  | 0.0414993  | \-1.4057013 | 0.1610644 |
|             countryMexico:suicides\_no             | \-0.1122679  | 0.0335923  | \-3.3420695 | 0.0009599 |
|          countryNetherlands:suicides\_no           | \-0.1107748  | 0.0335665  | \-3.3001611 | 0.0011083 |
|          countryNew Zealand:suicides\_no           | \-0.1006718  | 0.0338955  | \-2.9700678 | 0.0032695 |
|           countryNicaragua:suicides\_no            | \-0.1148620  | 0.0342191  | \-3.3566649 | 0.0009128 |
|             countryNorway:suicides\_no             | \-0.1103459  | 0.0343685  | \-3.2106674 | 0.0014992 |
|              countryOman:suicides\_no              |  0.1683083   | 0.1254730  |  1.3413902  | 0.1810209 |
|             countryPanama:suicides\_no             | \-0.0444417  | 0.0350177  | \-1.2691207 | 0.2055878 |
|            countryParaguay:suicides\_no            | \-0.0744727  | 0.0364761  | \-2.0416821 | 0.0422414 |
|          countryPhilippines:suicides\_no           | \-0.1118872  | 0.0335973  | \-3.3302461 | 0.0009998 |
|             countryPoland:suicides\_no             | \-0.1113726  | 0.0335733  | \-3.3172960 | 0.0010452 |
|            countryPortugal:suicides\_no            | \-0.1025696  | 0.0337191  | \-3.0418840 | 0.0026035 |
|          countryPuerto Rico:suicides\_no           | \-0.1009433  | 0.0349073  | \-2.8917525 | 0.0041710 |
|             countryQatar:suicides\_no              |  0.0812889   | 0.1156703  |  0.7027639  | 0.4828620 |
|       countryRepublic of Korea:suicides\_no        | \-0.1114727  | 0.0335753  | \-3.3200790 | 0.0010353 |
|            countryRomania:suicides\_no             | \-0.1103345  | 0.0335670  | \-3.2869985 | 0.0011591 |
|       countryRussian Federation:suicides\_no       | \-0.1118516  | 0.0335873  | \-3.3301786 | 0.0010000 |
|          countrySaint Lucia:suicides\_no           |  0.6230977   | 0.1873274  |  3.3262494  | 0.0010136 |
|  countrySaint Vincent and Grenadines:suicides\_no  |  0.2232315   | 0.1148997  |  1.9428375  | 0.0531675 |
|             countrySerbia:suicides\_no             | \-0.1038246  | 0.0336215  | \-3.0880435 | 0.0022439 |
|           countrySeychelles:suicides\_no           |  0.4223973   | 0.1294500  |  3.2630158  | 0.0012573 |
|           countrySingapore:suicides\_no            | \-0.0877508  | 0.0342425  | \-2.5626333 | 0.0109796 |
|            countrySlovakia:suicides\_no            | \-0.1062086  | 0.0335825  | \-3.1626188 | 0.0017584 |
|            countrySlovenia:suicides\_no            | \-0.1101728  | 0.0337872  | \-3.2607852 | 0.0012669 |
|          countrySouth Africa:suicides\_no          | \-0.1015241  | 0.0339548  | \-2.9899779 | 0.0030707 |
|             countrySpain:suicides\_no              | \-0.1117527  | 0.0335661  | \-3.3293367 | 0.0010029 |
|            countrySuriname:suicides\_no            | \-0.0536684  | 0.0375993  | \-1.4273773 | 0.1547291 |
|             countrySweden:suicides\_no             | \-0.1053803  | 0.0335787  | \-3.1383094 | 0.0019048 |
|          countrySwitzerland:suicides\_no           | \-0.1100180  | 0.0336055  | \-3.2738079 | 0.0012122 |
|            countryThailand:suicides\_no            | \-0.1111606  | 0.0335783  | \-3.3104883 | 0.0010699 |
|      countryTrinidad and Tobago:suicides\_no       | \-0.0789107  | 0.0351335  | \-2.2460235 | 0.0255834 |
|             countryTurkey:suicides\_no             | \-0.1088842  | 0.0335747  | \-3.2430417 | 0.0013450 |
|          countryTurkmenistan:suicides\_no          | \-0.0903267  | 0.0358077  | \-2.5225507 | 0.0122774 |
|            countryUkraine:suicides\_no             | \-0.1113432  | 0.0335783  | \-3.3159294 | 0.0010501 |
|      countryUnited Arab Emirates:suicides\_no      | \-0.1839277  | 0.1421653  | \-1.2937589 | 0.1969523 |
|         countryUnited Kingdom:suicides\_no         | \-0.1104690  | 0.0335693  | \-3.2907699 | 0.0011443 |
|         countryUnited States:suicides\_no          | \-0.1115031  | 0.0336050  | \-3.3180524 | 0.0010425 |
|            countryUruguay:suicides\_no             | \-0.0867334  | 0.0342058  | \-2.5356304 | 0.0118396 |
|           countryUzbekistan:suicides\_no           | \-0.1090372  | 0.0336206  | \-3.2431696 | 0.0013444 |
|            countryArgentina:population             |  0.0000081   | 0.0000116  |  0.6960672  | 0.4870386 |
|             countryArmenia:population              |  0.0000129   | 0.0000144  |  0.8956920  | 0.3712858 |
|              countryAruba:population               |  0.0000156   | 0.0002819  |  0.0551830  | 0.9560371 |
|            countryAustralia:population             |  0.0000090   | 0.0000117  |  0.7699080  | 0.4420872 |
|             countryAustria:population              |  0.0000110   | 0.0000118  |  0.9281699  | 0.3542219 |
|             countryBahamas:population              | \-0.0000143  | 0.0001078  | \-0.1325218 | 0.8946791 |
|             countryBahrain:population              | \-0.0000074  | 0.0000146  | \-0.5086140 | 0.6114750 |
|             countryBarbados:population             |  0.0000038   | 0.0000906  |  0.0414520  | 0.9669689 |
|             countryBelarus:population              |  0.0000091   | 0.0000116  |  0.7795308  | 0.4364104 |
|             countryBelgium:population              |  0.0000101   | 0.0000117  |  0.8630483  | 0.3889448 |
|              countryBelize:population              |  0.0002532   | 0.0002610  |  0.9700116  | 0.3329858 |
|              countryBrazil:population              |  0.0000094   | 0.0000116  |  0.8079443  | 0.4198970 |
|             countryBulgaria:population             |  0.0000129   | 0.0000118  |  1.0856398  | 0.2786925 |
|              countryCanada:population              |  0.0000089   | 0.0000116  |  0.7648286  | 0.4451008 |
|              countryChile:population               |  0.0000037   | 0.0000117  |  0.3204310  | 0.7489115 |
|             countryColombia:population             |  0.0000058   | 0.0000116  |  0.4977556  | 0.6190974 |
|            countryCosta Rica:population            | \-0.0000056  | 0.0000164  | \-0.3392499 | 0.7347086 |
|             countryCroatia:population              |  0.0000122   | 0.0000122  |  1.0057259  | 0.3155277 |
|               countryCuba:population               |  0.0000100   | 0.0000123  |  0.8118092  | 0.4176796 |
|              countryCyprus:population              | \-0.0000079  | 0.0000428  | \-0.1845005 | 0.8537716 |
|          countryCzech Republic:population          |  0.0000104   | 0.0000117  |  0.8899648  | 0.3743473 |
|             countryDenmark:population              |  0.0000096   | 0.0000125  |  0.7733278  | 0.4400649 |
|             countryEcuador:population              |  0.0000015   | 0.0000121  |  0.1219073  | 0.9030712 |
|           countryEl Salvador:population            | \-0.0000051  | 0.0000123  | \-0.4147364 | 0.6786934 |
|             countryEstonia:population              |  0.0000129   | 0.0000133  |  0.9680639  | 0.3339556 |
|             countryFinland:population              |  0.0000102   | 0.0000120  |  0.8520865  | 0.3949882 |
|              countryFrance:population              |  0.0000098   | 0.0000116  |  0.8410245  | 0.4011444 |
|             countryGeorgia:population              |  0.0000207   | 0.0000120  |  1.7237046  | 0.0860074 |
|             countryGermany:population              |  0.0000098   | 0.0000116  |  0.8470687  | 0.3977735 |
|              countryGreece:population              |  0.0000089   | 0.0000117  |  0.7620785  | 0.4467373 |
|             countryGrenada:population              | \-0.0000158  | 0.0003032  | \-0.0521980 | 0.9584130 |
|            countryGuatemala:population             | \-0.0000015  | 0.0000117  | \-0.1261157 | 0.8997425 |
|              countryGuyana:population              | \-0.0000930  | 0.0000583  | \-1.5964927 | 0.1116523 |
|             countryHungary:population              |  0.0000102   | 0.0000117  |  0.8756159  | 0.3820862 |
|             countryIceland:population              | \-0.0000330  | 0.0001316  | \-0.2506261 | 0.8023107 |
|             countryIreland:population              |  0.0000083   | 0.0000148  |  0.5589608  | 0.5766928 |
|              countryIsrael:population              |  0.0000085   | 0.0000123  |  0.6941717  | 0.4882243 |
|              countryItaly:population               |  0.0000100   | 0.0000116  |  0.8612131  | 0.3899526 |
|             countryJamaica:population              |  0.0000097   | 0.0000177  |  0.5466534  | 0.5851084 |
|              countryJapan:population               |  0.0000095   | 0.0000116  |  0.8156772  | 0.4154675 |
|            countryKazakhstan:population            |  0.0000057   | 0.0000116  |  0.4889778  | 0.6252895 |
|              countryKuwait:population              |  0.0000053   | 0.0000119  |  0.4442797  | 0.6572278 |
|            countryKyrgyzstan:population            |  0.0000006   | 0.0000129  |  0.0431514  | 0.9656155 |
|              countryLatvia:population              |  0.0000130   | 0.0000122  |  1.0634278  | 0.2886224 |
|            countryLithuania:population             |  0.0000113   | 0.0000119  |  0.9495315  | 0.3432748 |
|            countryLuxembourg:population            | \-0.0000201  | 0.0000448  | \-0.4481184 | 0.6544590 |
|             countryMaldives:population             | \-0.0000004  | 0.0000393  | \-0.0109745 | 0.9912526 |
|              countryMalta:population               | \-0.0000002  | 0.0000553  | \-0.0032495 | 0.9974099 |
|            countryMauritius:population             | \-0.0000424  | 0.0000308  | \-1.3766875 | 0.1698504 |
|              countryMexico:population              |  0.0000078   | 0.0000116  |  0.6742274  | 0.5007947 |
|           countryNetherlands:population            |  0.0000114   | 0.0000117  |  0.9796804  | 0.3281986 |
|           countryNew Zealand:population            |  0.0000045   | 0.0000137  |  0.3309883  | 0.7409328 |
|            countryNicaragua:population             | \-0.0000079  | 0.0000124  | \-0.6419361 | 0.5215076 |
|              countryNorway:population              |  0.0000099   | 0.0000124  |  0.7968219  | 0.4263167 |
|               countryOman:population               |  0.0000097   | 0.0000119  |  0.8172395  | 0.4145760 |
|              countryPanama:population              | \-0.0000312  | 0.0000214  | \-1.4611114 | 0.1452507 |
|             countryParaguay:population             | \-0.0000034  | 0.0000168  | \-0.2011675 | 0.8407325 |
|           countryPhilippines:population            |  0.0000095   | 0.0000116  |  0.8208953  | 0.4124943 |
|              countryPoland:population              |  0.0000098   | 0.0000116  |  0.8462253  | 0.3982428 |
|             countryPortugal:population             |  0.0000127   | 0.0000121  |  1.0496223  | 0.2949136 |
|           countryPuerto Rico:population            |  0.0000017   | 0.0000138  |  0.1257353  | 0.9000433 |
|              countryQatar:population               |  0.0000054   | 0.0000130  |  0.4201289  | 0.6747550 |
|        countryRepublic of Korea:population         |  0.0000097   | 0.0000116  |  0.8336584  | 0.4052757 |
|             countryRomania:population              |  0.0000102   | 0.0000116  |  0.8800218  | 0.3796995 |
|        countryRussian Federation:population        |  0.0000090   | 0.0000116  |  0.7756613  | 0.4386880 |
|           countrySaint Lucia:population            | \-0.0000005  | 0.0004078  | \-0.0012699 | 0.9989878 |
|   countrySaint Vincent and Grenadines:population   |  0.0003370   | 0.0003338  |  1.0095778  | 0.3136816 |
|              countrySerbia:population              |  0.0000172   | 0.0000123  |  1.3941229  | 0.1645283 |
|            countrySeychelles:population            | \-0.0002065  | 0.0002315  | \-0.8920247 | 0.3732444 |
|            countrySingapore:population             |  0.0000111   | 0.0000163  |  0.6803953  | 0.4968889 |
|             countrySlovakia:population             |  0.0000102   | 0.0000119  |  0.8582545  | 0.3915806 |
|             countrySlovenia:population             |  0.0000144   | 0.0000132  |  1.0897706  | 0.2768720 |
|           countrySouth Africa:population           |  0.0000088   | 0.0000116  |  0.7604345  | 0.4477173 |
|              countrySpain:population               |  0.0000100   | 0.0000116  |  0.8648247  | 0.3879707 |
|             countrySuriname:population             | \-0.0000874  | 0.0000614  | \-1.4229317 | 0.1560126 |
|              countrySweden:population              |  0.0000088   | 0.0000118  |  0.7440619  | 0.4575434 |
|           countrySwitzerland:population            |  0.0000104   | 0.0000119  |  0.8745691  | 0.3826545 |
|             countryThailand:population             |  0.0000092   | 0.0000116  |  0.7966139  | 0.4264373 |
|       countryTrinidad and Tobago:population        | \-0.0000882  | 0.0000355  | \-2.4839252 | 0.0136556 |
|              countryTurkey:population              |  0.0000098   | 0.0000116  |  0.8469443  | 0.3978427 |
|           countryTurkmenistan:population           | \-0.0000183  | 0.0000137  | \-1.3332663 | 0.1836678 |
|             countryUkraine:population              |  0.0000093   | 0.0000116  |  0.8037140  | 0.4223318 |
|       countryUnited Arab Emirates:population       |  0.0000118   | 0.0000118  |  1.0040239  | 0.3163457 |
|          countryUnited Kingdom:population          |  0.0000096   | 0.0000116  |  0.8276144  | 0.4086846 |
|          countryUnited States:population           |  0.0000094   | 0.0000116  |  0.8088807  | 0.4193591 |
|             countryUruguay:population              |  0.0000072   | 0.0000128  |  0.5620125  | 0.5746151 |
|            countryUzbekistan:population            |  0.0000063   | 0.0000117  |  0.5424211  | 0.5880155 |
|               sexmale:age25-34 years               |  0.0227997   | 0.0742235  |  0.3071766  | 0.7589667 |
|               sexmale:age35-54 years               | \-0.6350461  | 0.1179638  | \-5.3833978 | 0.0000002 |
|               sexmale:age5-14 years                | \-0.4628014  | 0.0794061  | \-5.8282867 | 0.0000000 |
|               sexmale:age55-74 years               | \-0.1955288  | 0.1060675  | \-1.8434372 | 0.0664583 |
|                sexmale:age75+ years                |  0.3589252   | 0.1120540  |  3.2031435  | 0.0015373 |
|                sexmale:suicides\_no                | \-0.0010401  | 0.0004765  | \-2.1828021 | 0.0299886 |
|            age25-34 years:suicides\_no             | \-0.0006882  | 0.0002148  | \-3.2042590 | 0.0015316 |
|            age35-54 years:suicides\_no             | \-0.0009266  | 0.0003605  | \-2.5702291 | 0.0107479 |
|             age5-14 years:suicides\_no             |  0.0452195   | 0.0116516  |  3.8809529  | 0.0001334 |
|            age55-74 years:suicides\_no             | \-0.0009255  | 0.0004145  | \-2.2327926 | 0.0264556 |
|             age75+ years:suicides\_no              | \-0.0009009  | 0.0009173  | \-0.9820932 | 0.3270110 |
|             age25-34 years:population              |  0.0000002   | 0.0000006  |  0.3128892  | 0.7546278 |
|             age35-54 years:population              |  0.0000017   | 0.0000007  |  2.5268532  | 0.0121318 |
|              age5-14 years:population              | \-0.0000006  | 0.0000008  | \-0.8027469 | 0.4228896 |
|             age55-74 years:population              |  0.0000018   | 0.0000007  |  2.4392759  | 0.0154186 |
|              age75+ years:population               |  0.0000015   | 0.0000008  |  1.9848390  | 0.0482643 |
|              suicides\_no:population               |  0.0000000   | 0.0000000  | \-0.0014712 | 0.9988274 |
>>>>>>> Trilok

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
