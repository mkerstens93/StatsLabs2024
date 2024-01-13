Lab 1 Kerstens and Rodne
================
2024-01-12

## Assignment

Sir Ronald Fisher measured the length and width of two flower parts,
sepals and petals, from two species of iris growing one spring in a
pasture on the Gaspé Peninsula. He wanted to determine how the means of
the distributions of the measurements of these flower parts differed
between the two species, although he did not define what size of
difference would be practically meaningful. Since field botanists often
use ranges of measures of plant characters to distinguish species, he
was also particularly interested in whether these measures could be used
to distinguish the two species in the field.

The data for this assignment consist of sepal and petal lengths and
widths (in mm) measured on 50 individuals each for two species of iris,
*Iris versicolor* and *Iris setosa*. All measurements were taken at the
widest point of the respective flower part. The data are in four
separate files, `setosa_sepal.txt`, `setosa_petal.txt`,
`versi_sepal.txt` and `versi_petal.txt`, representing measurements on
sepals and petals from *I. setosa* and *I. versicolor*, respectively.
Each data set contains three variables: `plant id`, `flower part width`
(mm), and `flower part length` (mm).

# Section I: Analysis

Reading in the data

    ## Warning: package 'tidyverse' was built under R version 4.3.2

    ## Warning: package 'dplyr' was built under R version 4.3.2

    ## Warning: package 'stringr' was built under R version 4.3.2

    ## Warning: package 'forcats' was built under R version 4.3.2

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.4     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.1
    ## ✔ ggplot2   3.4.4     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.3     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

    ## Warning: package 'here' was built under R version 4.3.2

    ## here() starts at C:/Users/skrod/Documents/GitHub/StatsLabs2024

``` r
setosa_sepal <- read_table(here("Data/setosa_sepal.txt"))
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   `"plantid"` = col_double(),
    ##   `"swidth"` = col_double(),
    ##   `"slength"` = col_double()
    ## )

``` r
setosa_petal <- read_table(here("Data/setosa_petal.txt"))
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   `"plantid"` = col_double(),
    ##   `"pwidth"` = col_double(),
    ##   `"plength"` = col_double()
    ## )

``` r
versi_sepal <- read_table(here("Data/versi_sepal.txt"))
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   `"plantid"` = col_double(),
    ##   `"swidth"` = col_double(),
    ##   `"slength"` = col_double()
    ## )

``` r
versi_petal <- read_table(here("Data/versi_petal.txt"))
```

    ## 
    ## ── Column specification ────────────────────────────────────────────────────────
    ## cols(
    ##   `"plantid"` = col_double(),
    ##   `"pwidth"` = col_double(),
    ##   `"plength"` = col_double()
    ## )

Rename columns

``` r
colnames(setosa_petal) <- c("plantid", "pwidth", "plength")
colnames(setosa_sepal) <- c("plantid", "swidth", "slength")
colnames(versi_petal) <- c("plantid", "pwidth", "plength")
colnames(versi_sepal) <- c("plantid", "swidth", "slength")
```

Combining the petal and sepal measurements for each species into 2
datasets

``` r
setosa <- inner_join(
x = setosa_petal,
y = setosa_sepal,
by = "plantid"
)
versi <- inner_join(
x = versi_petal,
y = versi_sepal,
by = "plantid"
)
```

Naming a separate column in setosa and versi dataframe that
distinguishes the two. This must be done before joining into the single
dataframe (setosa_versi).

``` r
setosa <- setosa %>%
mutate(.,
iris = "setosa"
)
versi <- versi %>%
mutate(.,
iris = "versi"
)
```

Join “setosa” and “versi” into “setosa_versi”. This contains all sepal
and petal measurements for all flowers.

``` r
setosa_versi <- rbind(setosa, versi)
```

Exploring the all flower measurements by iris species

petal width

``` r
qplot(
x = iris,
y = pwidth,
data = setosa_versi)
```

    ## Warning: `qplot()` was deprecated in ggplot2 3.4.0.
    ## This warning is displayed once every 8 hours.
    ## Call `lifecycle::last_lifecycle_warnings()` to see where this warning was
    ## generated.

![](Lab-01-Intro-to-R_Kerstens-Rodne_files/figure-gfm/unnamed-chunk-7-1.png)<!-- -->

sepal width

``` r
qplot(
x = iris,
y = swidth,
data = setosa_versi)
```

![](Lab-01-Intro-to-R_Kerstens-Rodne_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

petal length

``` r
qplot(
x = iris,
y = plength,
data = setosa_versi)
```

![](Lab-01-Intro-to-R_Kerstens-Rodne_files/figure-gfm/unnamed-chunk-9-1.png)<!-- -->

sepal length

``` r
qplot(
x = iris,
y = slength,
data = setosa_versi)
```

![](Lab-01-Intro-to-R_Kerstens-Rodne_files/figure-gfm/unnamed-chunk-10-1.png)<!-- -->

unequal variance assumed option

``` r
(resp_uneq <- t.test(pwidth ~ iris, data = setosa_versi))
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  pwidth by iris
    ## t = 34.325, df = 97.995, p-value < 2.2e-16
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##   9.987177 11.212823
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                15.86                 5.26

``` r
(resp_uneq <- t.test(swidth ~ iris, data = setosa_versi))
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  swidth by iris
    ## t = -7.2293, df = 65.689, p-value = 6.473e-10
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##  -8.831311 -5.008689
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                28.34                35.26

``` r
(resp_uneq <- t.test(plength ~ iris, data = setosa_versi))
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  plength by iris
    ## t = 37.657, df = 64.967, p-value < 2.2e-16
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##  26.07939 29.00061
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                44.54                17.00

``` r
(resp_uneq <- t.test(slength ~ iris, data = setosa_versi))
```

    ## 
    ##  Welch Two Sample t-test
    ## 
    ## data:  slength by iris
    ## t = 8.5731, df = 97.463, p-value = 1.552e-13
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##  5.563988 8.916012
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                59.30                52.06

equal variance assumed option

``` r
(resp_eq <- t.test(pwidth ~ iris, var.equal = T, data = setosa_versi))
```

    ## 
    ##  Two Sample t-test
    ## 
    ## data:  pwidth by iris
    ## t = 34.325, df = 98, p-value < 2.2e-16
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##   9.987178 11.212822
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                15.86                 5.26

``` r
(resp_eq <- t.test(swidth ~ iris, var.equal = T, data = setosa_versi))
```

    ## 
    ##  Two Sample t-test
    ## 
    ## data:  swidth by iris
    ## t = -7.2293, df = 98, p-value = 1.074e-10
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##  -8.819563 -5.020437
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                28.34                35.26

``` r
(resp_eq <- t.test(plength ~ iris, var.equal = T, data = setosa_versi))
```

    ## 
    ##  Two Sample t-test
    ## 
    ## data:  plength by iris
    ## t = 37.657, df = 98, p-value < 2.2e-16
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##  26.08867 28.99133
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                44.54                17.00

``` r
(resp_eq <- t.test(slength ~ iris, var.equal = T, data = setosa_versi))
```

    ## 
    ##  Two Sample t-test
    ## 
    ## data:  slength by iris
    ## t = 8.5731, df = 98, p-value = 1.497e-13
    ## alternative hypothesis: true difference in means between group setosa and group versi is not equal to 0
    ## 95 percent confidence interval:
    ##  5.564104 8.915896
    ## sample estimates:
    ## mean in group setosa  mean in group versi 
    ##                59.30                52.06

# Section II: Results

1.  Restate Fisher’s two research questions in the order they appear in
    the study description.

A. The questions that Fisher was asking in his study were: 1) If the
means of the distributions for the two iris species sepals and petals
were different? 2) If the measurements of the sepals and petals could be
used to distinguish the two species apart in the field.

2.  What analysis did you use to answer Fisher’s first research
    question? Be specific.

A. The first analysis to be used will help answer the first question. We
will use a t-test to quantify whether there is a significant difference
between the measurements of sepals and petals for the two species.

3.  How did you check the assumptions for the analysis you defined in
    question 2?

<!-- -->

1.  

<!-- -->

4.  Write a short paragraph that clearly presents the results for the
    analysis from part 2. Any estimate used for inference should be
    accompanied by a confidence interval for that estimate, and any test
    statistic reported should be accompanied by appropriate information
    on degrees of freedom.

<!-- -->

1.  

<!-- -->

5.  Write a short paragraph to answer Fisher’s second research question.
    Present any additional information you need to support your
    conclusion. You can include tables and graphics, with appropriate
    captions and clear labels, as necessary. Do not include any
    non-graphical output directly from R. Relevant output you want to
    report should be put into a table or written out within the text. Do
    not include any results that are not relevant or not referred to in
    your text. Part of your grade will be on neatness, clarity, and
    appropriateness of presentation; your grade will be reduced if you
    include superfluous output. See below for the grading rubric.

<!-- -->

1.  

### Section III: Short answer (4 points)

Describe and justify the scope of inference based on the description of
Fisher’s data. If you choose to extend the scope of inference, be sure
to justify this choice. If you do not, what gave you pause?
