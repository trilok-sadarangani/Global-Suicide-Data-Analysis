The Effect of Socio-Economics on Suicide Rates
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

With suicide being one of the leading causes of death for teens in
America, we thought it would be interesting to see how the U.S. stacks
up against other countries all over the world in terms of the number of
suicides that occur, as well as what factors may contribute to the
significant number of suicides in the U.S. and other countries.\[1\] We
want to explore how economic status, along with variables such as age,
sex, and human development index, affects suicide rates all across the
world. Our hypothesis is that generally, in poorer countries we predict
that suicide rates will lower.

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

``` r
glimpse(suicide)
```

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

### Section 4 - References

\[1\] <https://www.cdc.gov/nchs/fastats/adolescent-health.htm> \[2\]
<http://hdr.undp.org/en/content/human-development-index-hdi>
