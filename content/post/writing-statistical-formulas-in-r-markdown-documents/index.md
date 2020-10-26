---
title: Writing statistical formulas in R Markdown documents
author: Michael McCarthy
date: '2020-10-26'
slug: writing-statistical-formulas-in-r-markdown-documents
categories:
  - Tutorial
tags:
  - Statistics
  - R Markdown
  - LaTeX
  - MathJax
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

If you are taking a statistics course or writing methods-based scientific papers, it is likely that you will need to write a statistical formula at some point. R Markdown has built-in support for writing beautiful math expressions using [LaTeX mathematics](https://en.wikibooks.org/wiki/LaTeX/Mathematics) syntax, where any math expression is wrapped in a pair of dollar signs (for inline expressions) or double dollar signs (for display style expressions). This syntax can be used to render math expressions in any of R Markdown's output formats. Additionally, you can embed inline R code within any math expression, which can be useful for demonstrating mathematical proofs or showing your work on a statistics assignment.

If you want to dive deeper into writing math expressions in R Markdown documents, the [R Markdown: The Definitive Guide](https://bookdown.org/yihui/rmarkdown/markdown-syntax.html#math-expressions) book contains details on the various ways math expressions can be formatted in R Markdown documents, and [this post](https://math.meta.stackexchange.com/questions/5020/mathjax-basic-tutorial-and-quick-reference) on StackExchange has a handy reference guide for various math symbols in [MathJax](https://www.mathjax.org) (an open-source JavaScript display engine for LaTeX math expressions).

{{% alert note %}}
To see how any math expression was written on the web, simply right-click the expression and choose "Show Math As > TeX Commands".
{{% /alert %}}

## Mean

The formula for the mean is:

```math
$$\bar{X} = \frac{\sum_{i=1}^{n} x_{i}}{n}$$
```

$$\bar{X} = \frac{\sum_{i=1}^{n} x_{i}}{n},$$

where $x_{i}$ is the $i^{th}$ score in a group, and $n$ is the number of observations in a group.

In balanced designs, the grand mean can be calculated as either the mean of means (i.e., the average of each group's mean) or as the mean of all scores in the sample.

## Variance

The formula for variance is:

```math
$$s^{2} = \frac{SS}{N - 1} = \frac{\sum (x_{i} - \bar{x})^{2}}{N - 1}$$
```

$$s^{2} = \frac{SS}{N - 1} = \frac{\sum (x_{i} - \bar{x})^{2}}{N - 1},$$

where $SS$ is is the sum of squared errors; $N$ is the number of observations in the group; $x_{i}$ is the $i^{th}$ score in a group; and $\bar{x}$ is the mean of the group.

## Standard Deviation

The formula for the standard deviation is:

```math
$$s = \sqrt{s^{2}} = \sqrt{\frac{SS}{N - 1}} = \sqrt{\frac{\sum (x_{i} - \bar{x})^{2}}{N - 1}}$$
```

$$s = \sqrt{s^{2}} = \sqrt{\frac{SS}{N - 1}} = \sqrt{\frac{\sum (x_{i} - \bar{x})^{2}}{N - 1}},$$

where $s^{2}$ is the variance; $SS$ is is the sum of squared errors; $N$ is the number of observations in the group; $x_{i}$ is the $i^{th}$ score in a group; and $\bar{x}$ is the mean of the group.

## Standard Error (of the Mean)

The formula for the standard error is:

```math
$$\sigma_{\bar{X}} = \frac{s}{\sqrt{N}}$$
```

$$\sigma_{\bar{X}} = \frac{s}{\sqrt{N}},$$

where $s$ is the sample standard deviation, and $N$ is the sample size.

## Confidence Intervals

The formula for confidence intervals when samples are large is:

```math
$$\mathrm{CI} = \bar{X} \pm (z_{\frac{1 - p}{2}} \times \sigma_{\bar{X}})$$
```

$$\mathrm{CI} = \bar{X} \pm (z_{\frac{1 - p}{2}} \times \sigma_{\bar{X}cell}),$$

where $\bar{X}$ is the sample mean; $\sigma_{\bar{X}}$ is the standard error of the cell (i.e., $\frac{s_{cell}}{\sqrt{n_{cell}}} $); and $z$ is the absolute value for the z-score in the table of the standard normal distribution that corresponds to the area to the left (for lower bounds) or right (for upper bounds) of that z-score, $\frac{1 - p}{2}$, for a given probability value for the confidence interval, $p$. The exact value of $z$ can be computed in R with `abs(qnorm((1-p)/2))`, otherwise the value can be estimated with the table of the standard normal distribution.

The formula for confidence intervals when samples are small is:

```math
$$\mathrm{CI} = \bar{X} \pm (t_{n - 1} \times \sigma_{\bar{X}})$$
```

$$\mathrm{CI} = \bar{X} \pm (t_{n - 1} \times \sigma_{\bar{X}cell}),$$

where $\bar{X}$ is the sample mean; $\sigma_{\bar{X}cell}$ is the standard error of the cell (i.e., $\frac{s_{cell}}{\sqrt{n_{cell}}} $); and $t$ is the value of $t_{critical}$ in the t-table at degrees of freedom $n - 1$ for a given probability value (e.g., $p < .05$ in the t-table corresponds to a 95% CI). The exact value of $t$ can be computed in R with `abs(qt(1-(p/2), df))`, otherwise the value can be estimated with the table of the t-distribution.
