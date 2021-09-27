Project title
================
by Team name

    ## Warning in system("timedatectl", intern = TRUE): running command 'timedatectl'
    ## had status 1

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──

    ## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
    ## ✓ tibble  3.1.4     ✓ dplyr   1.0.7
    ## ✓ tidyr   1.1.3     ✓ stringr 1.4.0
    ## ✓ readr   2.0.1     ✓ forcats 0.5.1

    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

    ## Rows: 271116 Columns: 15

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (10): name, sex, team, noc, games, season, city, sport, event, medal
    ## dbl  (5): id, age, height, weight, year

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

## Introduction

(1-2 paragraphs) Brief introduction to the dataset. You may repeat some
of the information about the dataset provided in the introduction to the
dataset on the TidyTuesday repository, paraphrasing on your own terms.
Imagine that your project is a standalone document and the grader has no
prior knowledge of the dataset.

## Does the optimal build of an Olympic athlete differ by sex or by sport? How have the trends in height and weight of Olympic athletes evolved over time?

### Introduction

(1-2 paragraphs) Introduction to the question and what parts of the
dataset are necessary to answer the question. Also discuss why you’re
interested in this question.

We are interested in exploring the physical characteristics of Olympic
athletes. The Olympic Games is unique in showcasing a variety of
disciplines and the body types of athletes who succeed at them. For
example, imagine a typical male Olympic wrestler, versus a typical
female gymnast. Pretty disparate builds, right? Even within one sport,
say gymnastics, we hypothesize that there may be different optimal
heights and weights for successful athletes of different genders
Therefore, to answer our first question, we will visualize the variables
`height`, `weight`, `age`, `sex`, `sport`, and `year`.

### Approach

(1-2 paragraphs) Describe what types of plots you are going to make to
address your question. For each plot, provide a clear explanation as to
why this plot (e.g. boxplot, barplot, histogram, etc.) is best for
providing the information you are asking about. The two plots should be
of different types, and at least one of the two plots needs to use
either color mapping or facets.

For our first plot, we plan to use boxplots to plot the distribution of
a size characteristic by `sex` (since characteristics tend to differ
among males and females) and faceting by `sport`. We are unsure which of
the `height`, `weight`, `height / weight`, or `bmi` ratio will be most
telling when examined across sexes and sports. We will start by making 4
plots (each with one of these on the y-axis) and then select the plot
where the trends are most insightful.

Two of these variables require new calculations in the data wrangling
step. In order to plot the height-weight-ratio, we will have to create
two new calculated columns. First, a `height_weight_ratio` column that
simply divides an athlete’s `height` by their `weight`, and a more
complicated `BMI` column that represents an existing
metric–[BMI](https://en.wikipedia.org/wiki/Body_mass_index)–that
integrates height and weight into a single measure. .

Based on the results from these preliminary plots, in addition to
narrowing in on a size characteristic, we might pick a few select sports
to focus in on (i.e. most popular sports) or group the sports based on
common characteristics (ex: contact vs. non-contact, etc.) since there
are 66 sports in the dataset.

### Analysis

``` r
# Create new calculated variables to represent physical build
olympics <- olympics %>%
  mutate(height_weight_ratio = height / weight,
         BMI = 10000 * weight / (height * height))

# Create plot to examine BMIs and how they vary between sexes, then comparing these trends across sports
ggplot(olympics, mapping = aes(y = sport, x = BMI, color = sex)) +
  geom_boxplot()
```

    ## Warning: Removed 64263 rows containing non-finite values (stat_boxplot).

![](README_files/figure-gfm/generate-plot-one-1.png)<!-- -->

``` r
# I tried all 4, and i like BMI the best. As well as these sports:
# wrestling, weightlifting, judo (these three have weight classes as it's very apparent in the spread)
# boxing (they also have weight classes, but surprisingly, there is no difference? what?)
# gymnastics, trampolining (our original hypothesis; the boxes don't overlap! also the lower range of the female being like 12 makes me sad), 
# shooting, archery (very wide range, makes sense as you body type doesn't really matter as much as a steady hand. shooting showing more disparity than archery, as well)
# rowing, athletics (between coxswains in rowing, then sprinting vs throwing in althetics, no surprise that these are the top variables!)

# create helper vector of these sports
chosen_sports <- c("Wrestling", "Weightlifting", "Judo", "Boxing", "Gymnastics", "Trampolining", "Shooting", "Archery", "Rowing", "Athletics")

# try plotting again with just these sports, remember to keep each athlete only once!
olympics %>%
  filter(sport %in% chosen_sports) %>%
  mutate(category = case_when(
    sport %in% c("Wrestling", "Weightlifting", "Judo", "Boxing") ~ "weightclass",
    sport %in% c("Gymnastics", "Trampolining") ~ "lightweight",
    sport %in% c("Shooting", "Archery") ~ "coordination",
    TRUE ~ "diverse"
  )) %>%
  distinct(id, .keep_all = TRUE) %>%
  mutate(sport = factor(sport, levels = rev(chosen_sports)),
         sex = factor(sex, labels = c("Female", "Male"))) %>%
ggplot(mapping = aes(y = sport, x = BMI, color = sex)) +
  geom_boxplot() +
  labs(x = "Body Mass Index",
       y = "Sport",
       color = "Sex",
       title = "Sport vs Body Mass Index Distribution",
       subtitle = "Of selected Olympic sports from 1912-2020",,
       caption = "Source: Sports Reference & OlympStats\nAccessed from kaggle.com") +
  facet_grid(category ~ ., scales = "free_y", space = "free") +
  theme(strip.background = element_blank(),
        strip.text.y = element_blank())
```

    ## Warning: Removed 14145 rows containing non-finite values (stat_boxplot).

![](README_files/figure-gfm/generate-plot-one-2.png)<!-- -->

(2-3 code blocks, 2 figures, text/code comments as needed) In this
section, provide the code that generates your plots. Use scale functions
to provide nice axis labels and guides. You are welcome to use theme
functions to customize the appearance of your plot, but you are not
required to do so. All plots must be made with ggplot2. Do not use base
R or lattice plotting functions.

### Discussion

(1-3 paragraphs) In the Discussion section, interpret the results of
your analysis. Identify any trends revealed (or not revealed) by the
plots. Speculate about why the data looks the way it does.

## Question 2 \<- Update title to relate to the question you’re answering

### Introduction

(1-2 paragraphs) Introduction to the question and what parts of the
dataset are necessary to answer the question. Also discuss why you’re
interested in this question.

### Approach

(1-2 paragraphs) Describe what types of plots you are going to make to
address your question. For each plot, provide a clear explanation as to
why this plot (e.g. boxplot, barplot, histogram, etc.) is best for
providing the information you are asking about. The two plots should be
of different types, and at least one of the two plots needs to use
either color mapping or facets.

### Analysis

(2-3 code blocks, 2 figures, text/code comments as needed) In this
section, provide the code that generates your plots. Use scale functions
to provide nice axis labels and guides. You are welcome to use theme
functions to customize the appearance of your plot, but you are not
required to do so. All plots must be made with ggplot2. Do not use base
R or lattice plotting functions.

### Discussion

(1-3 paragraphs) In the Discussion section, interpret the results of
your analysis. Identify any trends revealed (or not revealed) by the
plots. Speculate about why the data looks the way it does.

## Presentation

Our presentation can be found [here](presentation/presentation.html).

## Data

Include a citation for your data here. See
<http://libraryguides.vu.edu.au/c.php?g=386501&p=4347840> for guidance
on proper citation for datasets. If you got your data off the web, make
sure to note the retrieval date.

## References

List any references here. You should, at a minimum, list your data
source.
