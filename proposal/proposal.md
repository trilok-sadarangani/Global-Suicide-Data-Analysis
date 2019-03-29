Suicide Rates
================
Cam Fam
March 29, 2019

``` r
library(nnet)
library(tidyverse)
```

    ## ── Attaching packages ────────── tidyverse 1.2.1 ──

    ## ✔ ggplot2 3.1.0     ✔ purrr   0.2.5
    ## ✔ tibble  2.0.0     ✔ dplyr   0.7.8
    ## ✔ tidyr   0.8.2     ✔ stringr 1.3.1
    ## ✔ readr   1.3.1     ✔ forcats 0.3.0

    ## ── Conflicts ───────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(knitr)
library(broom)
```

## Section 1. Introduction

We want to explore how economic status, along with variables such as
age, sex, and human development index, affects suicide rates all across
the world. Our hypothesis is that generally, in poorer countries we
predict that suicide rates will lower.

## Section 2. Analysis plan

Our response variable will be suicides/100k pop, which is the number of
suicides per 100,000 people in a country, which is a double in our
dataset. Our predictors variables will be age, sex, country, year, HDI
for year, gdp\_for\_year, gdp\_per\_capita, and generation. COEFFICIENTS
??

Description.

EDA.

We plan to do a multiple linear regression because suicides/100k pop is
a quantitative variable (there are no levels to it).

Based on variables, we plan to predict suicide rate in the future for
certain countries, as well as what generation someone who commits
suicide is in given other variables.

## Section 3. Data

``` r
suicide <- read_csv("/cloud/project/data/master.csv")
```

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
