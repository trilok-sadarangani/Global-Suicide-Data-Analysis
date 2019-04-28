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
age, sex, country, year, HDI for year, gdp\_for\_year, gdp\_per\_capita,
and generation. Age is the age an individual was when they passed, sex
is the gender of that individual, country is the country they are from,
year is the year they passed, HDI for year is the human development
index for a given country and year, gdp\_for\_year is the GDP for a
given country and year, gdp\_per\_capita is the GDP per capita for a
given country and year, and generation is the generation that an
individual belongs to. We wish to understand how the number of suicides
per 100,000 people in a certain country and year changes as year, GDP,
GDP per capita, and HDI increase or decreases, meaning we want to
understand the population coefficients for year, gdp\_for\_year,
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

The countries that do not have HDI calculated for them are Aruba, Puerto
Rico, Korea, and Russia.

Later on in this EDA, we will want to do a boxplot of the countries;
however, that will be indiscernable based on the number of countries.
Instead, we should group countries into regions and their continents.

We will use the gapminder dataset for countries and regions. We will
extract the country, continent, and region from gapMinder, change the
names of differing countries, and then merge.

To see the shape of the distribution of the number of suicides per
100,000 people, we can plot a histogram of the suicides/100k pop
variable.

    ## Skim summary statistics
    ##  n obs: 58848 
    ##  n variables: 14 
    ## 
    ## ── Variable type:character ─────────────────────────────────────────
    ##      variable missing complete     n min max empty n_unique
    ##           age       0    58848 58848   9  11     0        6
    ##       country       0    58848 58848   4  28     0       88
    ##  country-year       0    58848 58848   8  32     0       88
    ##    generation       0    58848 58848   6  12     0        4
    ##           sex       0    58848 58848   4   6     0        2
    ## 
    ## ── Variable type:factor ────────────────────────────────────────────
    ##   variable missing complete     n n_unique
    ##  continent      24    58824 58848        5
    ##     region      24    58824 58848       16
    ##                                     top_counts ordered
    ##  Eur: 23256, Ame: 18468, Asi: 13680, Afr: 2052   FALSE
    ##     Nor: 6840, Wes: 6840, Car: 6156, Sou: 6156   FALSE
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────
    ##            variable missing complete     n          mean            sd
    ##    gdp_for_year ($)       0    58848 58848       6.1e+11       1.8e+12
    ##  gdp_per_capita ($)       0    58848 58848   24125.76      22633.48   
    ##        HDI for year    2736    56112 58848       0.79          0.087  
    ##          population       0    58848 58848 1929582.68    4088895.06   
    ##         suicides_no       0    58848 58848     230.6         813.66   
    ##   suicides/100k pop       0    58848 58848      11.28         17.01   
    ##                year       0    58848 58848    2010             0      
    ##          p0       p25          p50           p75         p100     hist
    ##     6.8e+08  2e+10         9.8e+10       3.9e+11      1.5e+13 ▇▁▁▁▁▁▁▁
    ##   991         7066     13817.5       36869       111328       ▇▂▂▂▁▁▁▁
    ##     0.61         0.73      0.8           0.88         0.94    ▃▃▆▇▆▆▇▇
    ##  1015       113923    462298       1588670            4.3e+07 ▇▁▁▁▁▁▁▁
    ##     0            2        23           110        11767       ▇▁▁▁▁▁▁▁
    ##     0            0.84      4.91         14.38       182.32    ▇▁▁▁▁▁▁▁
    ##  2010         2010      2010          2010         2010       ▁▁▁▇▁▁▁▁

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->

    ## 
    ## Skim summary statistics
    ## 
    ## ── Variable type:numeric ───────────────────────────────────────────
    ##                     variable missing complete     n  mean    sd p0  p25
    ##  suicide$`suicides/100k pop`       0    58848 58848 11.28 17.01  0 0.84
    ##   p50   p75   p100     hist
    ##  4.91 14.38 182.32 ▇▁▁▁▁▁▁▁

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

![](project-writeup_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

From log transforming suicides/100k pop, we can already see that the
extreme outliers have disappeared, and the histogram seems to be
approximately normally distributed.

It is important to note that in the dataset, some of the suicides/100k
pop values are -inf. This is because there were 0 suicides in that year
and country, and thus dividing by 0 when calculating the number of
suicides per 100,000 people resulted in -inf. In the future, we will
change all -inf to 0, since if there were 0 suicides in that year and
country for the entire population, then there must have been 0 suicides
in that year and country for every 100,000 people.

Note: suicides/100k pop is now log transformed for all plot below.

We will now look at an overview of the relationships that suicides/100k
pop has with each of the quantitative predictor variables (age, sex,
country, year, HDI for year, gdp\_for\_year, gdp\_per\_capita, and
generation), as well as the relationships these variables have with each
other.

![](project-writeup_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

From the pairs plot, it looks as if year, HDI for year, and
gdp\_for\_year do not have a clear linear relationship with
suicides/100k pop. However, gdp\_per\_capita seems to be positively
correlated with suicides/100k pop, meaning as gdp\_per\_capita
increases, so does suicides/100k pop. Additionally, it looks as if HDI
for year and gdp\_per\_capita seem to have a strong non-linear
relationship, indicating that we should continue looking into this
relationship and perhaps include an interaction term between these two
variables. Similarly, HDI for year and gdp\_for\_year also seem to have
a strong non-linear relationship, so we should include an interaction
term between these two variables as
    well.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Computation failed in `stat_bin()`:
    ## `binwidth` must be positive

![](project-writeup_files/figure-gfm/unnamed-chunk-8-1.png)<!-- --> The
distribution of year appears to be normal with two outliers around 1992
and 2008. There appears to be a general increase in suicide rate as year
increases.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

    ## Warning: Removed 2736 rows containing non-finite values (stat_bin).

![](project-writeup_files/figure-gfm/unnamed-chunk-9-1.png)<!-- --> The
distribution of HDI for year shows that as HDI for year increases,
suicide rate increases until about .75 and then begins to slightly
decrease.

![](project-writeup_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

By examining these boxplots, we can tell that as age increases, suicide
rate tends to increase in general.

![](project-writeup_files/figure-gfm/unnamed-chunk-11-1.png)<!-- -->

Because there are so many countries, it is hard to tell what the general
trend is for suicide rates. We will further examine this potential
relationship in our project.

![](project-writeup_files/figure-gfm/unnamed-chunk-12-1.png)<!-- -->

From this boxplot, we notice that males have a higher suicide rate/100k
people than females. However, there are many outliers in this data set
so we must explore further.

![](project-writeup_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

From this boxplot, we see that the average suicide rate/100k people is
varies among gneeration. More specifically, we notice that Generation Z
and Millienials have lower ates than the average value of around
    2.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-14-1.png)<!-- -->

Log transforming the data set, we notice that the distribution of GDPs
of countries has a bimodal
    distribution.

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](project-writeup_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

Like the GDP of the country, the GDP Per Capita has a non-normal
distribution. Rather, it is skewed to the left. Since these variables
are so similar, there could be mulitcollinearity between the two.

![](project-writeup_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

As mentioned before, we do see evidence of multicollinearity that we
must address in the model.

We plan to do a multiple linear regression because suicides/100k pop is
a quantitative variable (there are no levels to it, since it is a
continuous variable).

Based on the variables, we plan to predict suicide rate in the future
for certain countries, as well as what generation someone who commits
suicide is in given other variables.

## Section 3. Data

    ## Observations: 58,848
    ## Variables: 14
    ## $ country              <chr> "Albania", "Albania", "Albania", "Albania",…
    ## $ year                 <dbl> 2010, 2010, 2010, 2010, 2010, 2010, 2010, 2…
    ## $ sex                  <chr> "female", "female", "female", "female", "fe…
    ## $ age                  <chr> "15-24 years", "15-24 years", "15-24 years"…
    ## $ suicides_no          <dbl> 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6…
    ## $ population           <dbl> 263581, 263581, 263581, 263581, 263581, 263…
    ## $ `suicides/100k pop`  <dbl> 2.28, 2.28, 2.28, 2.28, 2.28, 2.28, 2.28, 2…
    ## $ `country-year`       <chr> "Albania2010", "Albania2010", "Albania2010"…
    ## $ `HDI for year`       <dbl> 0.722, 0.722, 0.722, 0.722, 0.722, 0.722, 0…
    ## $ `gdp_for_year ($)`   <dbl> 11926953259, 11926953259, 11926953259, 1192…
    ## $ `gdp_per_capita ($)` <dbl> 4359, 4359, 4359, 4359, 4359, 4359, 4359, 4…
    ## $ generation           <chr> "Millenials", "Millenials", "Millenials", "…
    ## $ continent            <fct> Europe, Europe, Europe, Europe, Europe, Eur…
    ## $ region               <fct> Southern Europe, Southern Europe, Southern …

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
