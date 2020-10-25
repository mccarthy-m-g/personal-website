---
title: Simulating experimental data in R
author: ''
date: '2020-10-25'
slug: simulating-experimental-data-in-r
categories:
  - Tutorial
tags:
  - R
  - Statistics
  - Science
  - Experiment
  - Data Science
  - R-bloggers
subtitle: ''
summary: ''
authors: []
lastmod: ''
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

Knowing how to simulate experimental data is an incredibly useful skill. Practically, it allows you to generate data that you can use to test your analysis scripts, making it easier to [preregister](https://www.cos.io/initiatives/prereg) those scripts along with your study plan. Theoretically, it provides you with an excellent opportunity to test your intuition about how data behaves in different experimental designs. Fortunately, R makes it quite easy to simulate data for a variety of experimental designs.

## Functions for simulating data in R

Base R provides a number of functions that can be used to simulate continuous and categorical data. We will focus on three here: `set.seed()`, which specifies the seed to use for random number generation, ensuring that the data you simulate retains the same values each time a simulation function is run; `rnorm()`, which generates random deviates from a given mean, creating a normal distribution; and `rep()`, which replicates values or patterns of values (such as character strings). By using these last two functions in the context of a data frame (or a [tibble](https://tibble.tidyverse.org) as I do below), you can simulate data for a variety of experimental designs:

```r
# seed for random number generation
set.seed(42)
```

### Independent t-test

```r
# create dataset
df_ind_t.test <- tibble(ID = 1:100,
                        IV = c(rep("A", 50),
                               rep("B", 50)
                               ),
                        DV = c(rnorm(n = 50, mean = 100, sd = 17), # A
                               rnorm(n = 50, mean = 120, sd = 15)  # B
                               )
                        )
# encode IV as a factor
df_ind_t.test$IV <- factor(df_ind_t.test$IV, levels = c("A", "B"))
```

The independent t-test, which tests whether the values in two distinct unrelated groups significantly differ from each other, is the simplest experimental design you can simulate. The resulting data frame consists of three columns: **ID** (the participant's ID number), **IV** (the independent variable), and **DV** (the dependent variable). Each row of the data frame corresponds to the data for a given participant.

Here the simulated experimental data consists of 100 participants, 50 of which belong to level A of the IV and 50 of which belong to level B of the IV. Scores on the DV are normally distributed for both levels of the IV, however, their means and standard deviations are different, with level A having a mean of approximately 100 and a standard deviation of approximately 17 and with level B having a mean of approximately 120 and a standard deviation of approximately 15.

### Dependent t-test

```r
# create dataset
df_dep_t.test <- tibble(ID = rep(1:50, 2),
                        IV = c(rep("A", 50),
                               rep("B", 50)
                               ),
                        DV = c(rnorm(n = 50, mean = 100, sd = 17), # A
                               rnorm(n = 50, mean = 120, sd = 15)  # B
                               )
                        )
# encode IV as a factor
df_dep_t.test$IV <- factor(df_dep_t.test$IV, levels = c("A", "B"))
```

Data for the dependent t-test, which tests whether the values within the same group (or a matched group) significantly differ across two contexts, can be simulated by changing the 100 independent observations from the independent t-test simulation into 50 dependent observations. Using `rep()` in the **ID** column of the data frame makes this easy to accomplish.

### Independent one-way ANOVA

```r
# create dataset
df_ind_1way_3 <- tibble(ID = 1:150,
                        IV = c(rep("A", 50),
                               rep("B", 50),
                               rep("C", 50)
                               ),
                        DV = c(rnorm(n = 50, mean = 100, sd = 15), # A
                               rnorm(n = 50, mean = 110, sd = 12), # B
                               rnorm(n = 50, mean =  90, sd = 18)  # C
                               )
                        )
# encode IV as a factor
df_ind_1way_3$IV <- factor(df_ind_1way_3$IV, levels = c("A", "B", "C"))
```

Data for the independent one-way ANOVA, which tests for an overall effect between two or more distinct unrelated groups without specifying what the effect is, can be simulated by adding more levels of the **IV** and more values of the **DV** to the independent t-test simulation.

Here the simulated experimental data consists of 150 participants, 50 of which belong to level A of the IV, 50 of which belong to level B of the IV, and 50 of which belong to level C of the IV.

### Dependent one-way ANOVA

```r
# create dataset
df_dep_1way_3 <- tibble(ID = rep(1:50, 3),
                        IV = c(rep("A", 50),
                               rep("B", 50),
                               rep("C", 50)
                               ),
                        DV = c(rnorm(n = 50, mean =  90, sd = 15), # A
                               rnorm(n = 50, mean = 110, sd = 12), # B
                               rnorm(n = 50, mean = 100, sd = 18)  # C
                               )
                        )
# encode IV as a factor
df_dep_1way_3$IV <- factor(df_dep_1way_3$IV, levels = c("A", "B", "C"))
```

Data for the dependent one-way ANOVA, which tests for an overall effect within the same group (or a matched group) across two or more contexts without specifying what the effect is, can be simulated by making the same changes to the **ID** column that were done in the dependent t-test simulation above.

### Independent two-way ANOVA

```r
# create dataset
df_2way_3x2 <- tibble(ID  = 1:150,
                      IV1 = c(rep("A", 50),
                              rep("B", 50),
                              rep("C", 50)
                              ),
                      IV2 = c(rep(c("a", "b"),
                                  each = 25,
                                  length.out = 150
                                  )
                              ),
                      DV  = c(rnorm(n = 25, mean = 100, sd = 10), # A*a
                              rnorm(n = 25, mean = 100, sd = 10), # A*b
                              rnorm(n = 25, mean = 100, sd = 10), # B*a
                              rnorm(n = 25, mean = 100, sd = 10), # B*b
                              rnorm(n = 25, mean = 100, sd = 10), # C*a
                              rnorm(n = 25, mean = 100, sd = 10)  # C*b
                              )
                      )
# encode IV1 as a factor
df_2way_3x2$IV1 <- factor(df_2way_3x2$IV1, levels = c("A", "B", "C"))
# encode IV2 as a factor
df_2way_3x2$IV2 <- factor(df_2way_3x2$IV2, levels = c("a", "b"))
```

Data for the independent two-way ANOVA, which tests for a main effect and an interaction effect of two independent variables on a dependent variable without specifying what the effect is, can be simulated by adding a second independent variable, **IV2**, and more values of the **DV** to the independent one-way ANOVA simulation.

Here the simulated data consists of a 3x2 ANOVA with 150 participants assigned to one of six cells representing unique combinations of **IV1** and **IV2**. 25 participants belong to each cell. 

## Simulating non-normal distributions

For most simulations of experimental data you likely want to use normally distributed data, since parametric tests assume data is normally distributed. However, if you want to break those assumptions you can do so by using non-normal distributions. Base R provides functions to simulate a number of distributions; you can see them all by running `?distributions` in the console.

### Bimodal distribution

```r
# create dataset
df_ind_t.test <- tibble(ID = 1:100,
                        IV = c(rep("A", 50),
                               rep("B", 50)
                               ),
                        DV = c(rnorm(n = 25, mean =  80, sd = 10), # A
                               rnorm(n = 25, mean = 120, sd = 10), # A
                               rnorm(n = 50, mean = 100, sd = 15)  # B
                               )
                        )
# encode IV as a factor
df_ind_t.test$IV <- factor(df_ind_t.test$IV, levels = c("A", "B"))
```

Simulating a bimodal distribution within a given level of the IV is fairly straightforward: Using `rnorm()`, simulate two normal distributions that have different means and half the number of observations as a given level of the IV. The means of the two distributions will need to be far enough for this to work (or the standard deviations will need to be reduced).

Here the simulated data has a bimodal distribution for level A of the IV, and a normal distribution for level B of the IV. 

<!--
### Skew-normal distribution

```r
# create dataset
df_ind_t.test <- tibble(ID = 1:100,
                        IV = c(rep("A", 50),
                               rep("B", 50)
                               ),
                        DV = c(sn::rsn(50, dp = sn::cp2dp(c(mean =  80,
                                                            sd = 17,
                                                            skew = 1.6,
                                                            kurtosis = 9), 
                                                          family="ST")), # A
                               sn::rsn(50, dp = sn::cp2dp(c(mean = 100,
                                                            sd = 17,
                                                            skew = -1,
                                                            kurtosis = 7), 
                                                          family="ST"))  # B
                               )
                        )
# encode IV as a factor
df_ind_t.test$IV <- factor(df_ind_t.test$IV, levels = c("A", "B"))
```

Simulating a skew-normal distribution is slightly less straightforward than simulating a normal distribution, particularly if the distribution needs to have certain parameters. Fortunately, the [`sn`](https://cran.r-project.org/web/packages/sn/index.html) package provides functions to accomplish this. The code above has been adapted from the package's [vignette](https://cran.r-project.org/web/packages/sn/vignettes/how_to_sample.pdf).

Here the simulated data has a positvely skewed distribution for level A of the IV, and a negatively skewed distribution for level B of the IV.
-->
