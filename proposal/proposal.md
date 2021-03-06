Project proposal
================
Mr. Palmer’s Penguins

``` r
library(tidyverse)

# load data from tidytuesday site and write to csv in data folder
readr::read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-07-27/olympics.csv") %>%
  write_csv(file = paste0(here::here(), "/data/olympics_data.csv"))

# read data from csv
olympics <- read_csv(file = paste0(here::here(), "/data/olympics_data.csv"))
```

## Dataset

This dataset was accessed on Kaggle.com and includes data scraped in May
2018 from Sports Reference/OlympStats, sports statistics sites, by Randi
Griffin, a Senior Data Scientist at Boston Consulting Group. Moreover,
it was selected as part of the TidyTuesday challenge on 7/27/21.
Citation information is included at the bottom of this section.

The set, which includes 15 variables and 271116 observations, provides
insight into the athletes that competed in and the results of the
Olympic games from Athens 1896 to Rio 2016. Each observation includes
information about an athlete on a per event basis. Therefore, if an
athlete competes in multiple different events, there will be multiple
different observations reflecting each event an individual participated
in. Each observation details medal results (Gold, Silver, Bronze, or
NA), the athlete’s background (age, sex, height, weight, team, etc.),
and context about the event (where and when it was held, season, etc.).

The full list of variables are included here and described below:

``` r
glimpse(olympics)
```

    ## Rows: 271,116
    ## Columns: 15
    ## $ id     <dbl> 1, 2, 3, 4, 5, 5, 5, 5, 5, 5, 6, 6, 6, 6, 6, 6, 6, 6, 7, 7, 7, …
    ## $ name   <chr> "A Dijiang", "A Lamusi", "Gunnar Nielsen Aaby", "Edgar Lindenau…
    ## $ sex    <chr> "M", "M", "M", "M", "F", "F", "F", "F", "F", "F", "M", "M", "M"…
    ## $ age    <dbl> 24, 23, 24, 34, 21, 21, 25, 25, 27, 27, 31, 31, 31, 31, 33, 33,…
    ## $ height <dbl> 180, 170, NA, NA, 185, 185, 185, 185, 185, 185, 188, 188, 188, …
    ## $ weight <dbl> 80, 60, NA, NA, 82, 82, 82, 82, 82, 82, 75, 75, 75, 75, 75, 75,…
    ## $ team   <chr> "China", "China", "Denmark", "Denmark/Sweden", "Netherlands", "…
    ## $ noc    <chr> "CHN", "CHN", "DEN", "DEN", "NED", "NED", "NED", "NED", "NED", …
    ## $ games  <chr> "1992 Summer", "2012 Summer", "1920 Summer", "1900 Summer", "19…
    ## $ year   <dbl> 1992, 2012, 1920, 1900, 1988, 1988, 1992, 1992, 1994, 1994, 199…
    ## $ season <chr> "Summer", "Summer", "Summer", "Summer", "Winter", "Winter", "Wi…
    ## $ city   <chr> "Barcelona", "London", "Antwerpen", "Paris", "Calgary", "Calgar…
    ## $ sport  <chr> "Basketball", "Judo", "Football", "Tug-Of-War", "Speed Skating"…
    ## $ event  <chr> "Basketball Men's Basketball", "Judo Men's Extra-Lightweight", …
    ## $ medal  <chr> NA, NA, NA, "Gold", NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…

`ID` - This is an athlete-specific number. Each athlete is assigned one
unique identifying number in the dataset

`Name` - The name of the athlete competing.

`Sex` - Indicated whether the athlete is Male (M) or Female (F)

`Age` - The age of the athlete in years

`Height` - The height of the athlete in centimeters

`Weight` - The weight of the athlete in kilograms

`Team` - The team (same as the country in most cases) the athlete
represents

`NOC` - The 3-letter National Olympic Committee code associated with
each team (indicative of country in most cases)

`Games` - The year (1896-2016) and season (Summer or Winter) in which
the event took place. This is a character combination of `Year` and
`Season`. It is important to note that the Summer and Winter games
currently alternate every two years, but used to take place in the same
year.

`Year` - The year (1896-2016) in which the event took place.

`Season` - The season (Summer or Winter) in which the event took place.

`City` - The city in which the Olympic games for that year/season were
hosted.

`Sport` - The sport the athlete is competing in.

`Event` - The event the athlete is competing in within a sport.

`Medal` - Indicates whether a Gold, Silver, or Bronze medal was won.
Responses can also take the form NA if no medal was won or there is
incomplete information.

We chose this dataset because we think it can provide a lot of good
insights into some of the trends at the Olympics over the past century
as well as provide strong opportunities for our group to develop our
visualization capabilities.

These data offer many avenues to explore when analyzing, such as
medalwinning success on an athlete-level scale, on a country-level
scale, or for a particular sport over time, etc. Complementing this
variety of potential analysis paradigms is the medley of variable types.
Several variable types such as categorical, ordinal, time-series, and
ratio are well represented in the data. This also affords us the
opportunity to calculate new variables, such as converting the medal
variable into a logical medal winner or non-medal winner.

Finally, aside from the properties of the data itself, we chose to
analyze data from the Olympic games due to the recency of the 2020/2021
Tokyo Games and the role of the Games in reflecting the global culture
of a time period. Historic events like the 1980 Moscow Games that were
boycotted by the US and many other countries, the several instances of
Games that were canceled during the World Wars, and the late 1980s
advent of professional superstar Olympians all potentially provide
insights into the story told by the data.

#### Sources

[TidyTuesday](https://github.com/rfordatascience/tidytuesday/tree/master/data/2021#readme7c70d95441aec295a1e92da9d71e2872877d663c)

[Kaggle](https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results)

## Questions

The two questions you want to answer.

1.  How have the physical characteristics (height-to-weight ratio, age,
    and sex) of Olympic participants changed over time and do they
    differ by sport?

Variables: `height`, `weight`, `age`, `sex`, `sport`, `year`

2.  How has the success of different countries in a particular sport
    changed with time?

Variables: `year`, `NOC`, `medal count`, `sport`, `country`

## Analysis plan

Here is a plan for answering each of the questions:

### For Question 1

We are interested in exploring the physical characteristics of Olympic
athletes. Therefore, to answer our first question, we will visualize the
variables `height`, `weight`, `age`, `sex`, `sport`, and `year`.

#### Plot 1:

We are all used to hearing that Olympic athletes have certain favorable
physical condition, but those characteristics differ by sport. For
example, volleyball and basketball players are usually exceptionally
tall, while wrestlers are usually shorter and built. Therefore, for our
first plot, we plan to explore how size characteristics (either using
`height`, `weight`, or the `height:weight` ratio) differ by `sport` and
`sex`. In other words, we plan to use boxplots to plot the distribution
of a size characteristic by `sex` (since characteristics tend to differ
by division) and faceting by `sport`.

Since we are unsure which of the `height`, `weight`, or the
`height:weight` ratio will be most telling, we will start by making 3
plots (each with one of these on the y-axis) and then select the plot
where the trends are most insightful.

In order to plot the height-weight-ratio, we will have to create a new
variable and divide height by weight.

Based on the results, in addition to narrowing in on a size
characteristic, we might pick a few select sports to focus in on
(i.e. most popular sports) or group the sports based on common
characteristics (ex: contact vs. non-contact, etc.) since there are 66
sports in the dataset.

#### Plot 2:

For our second plot, we will look more closely at how size
characteristics have changed over time, using `year` to make a time
series line plots for these different values. In other words, we will
plot one of the size characteristics (`height`, `weight`, or the
height:weight ratio) on the y-axis vs. time on the x-axis. Lines by
`sex` will connect the observations. We might also facet these plots by
`age` to see if, for example, height of athletes has changed more or
less over time for younger athletes vs. older athletes. In order to
facet by `age`, we will have to make `age` a categorical variable by
setting different cutoffs in which we group observations.

The ages in the dataset range from 10 to 97 years old. Therefore, we
will plot a histogram and do summary statistics to understand which
cutoffs make the most sense given the data. Since athletes tend to be in
their mid 20s, we’ll likely have smaller differences in ages in the
20-30 age range whereas all athletes 40-97, for example, might be
grouped together. However, as mentioned, this would depend on the
distribution of the data.

Like in Plot 1, we will evaluate which of `height`, `weight`, or the
`height:weight` ratio provides the most insightful visualization.
Ideally, the variable we choose in Plot 1 will be the same as in Plot 2;
however, we understand creating visualizations is an iterative process
are open to evaluating all options as we plot.

### For Question 2

#### Data wrangling

The original variables we will use to answer this question are `noc`,
`medal`, `sport` (perhaps `event` if some higher granularity proves
informative rather than overwhelming), and `year` and `season`. Both
`year` and `season` are important for placing each Olympics in time and
will require some cleaning in conversion to an accurate variable `date`.
Many of us are familiar with even recent anomalies in Olympic labeling
(such as these recent 2020 Summer Olympics, which took place in 2021).
The exact begin and end dates of each Olympics are not the goal of this
step. We simply wish to be able to correctly order the games
chronologically, which may require more information than just the year
and season in some cases.

Next, we will mutate `medal` from a categorical variable with ‘Gold’,
‘Silver’, ‘Bronze’, and NA as outcomes to either a numeric indicator
(medal = 1 for any win and medal = 0 for no medal received) or a score
that rewards the most points for Gold, then Silver, then Bronze. Through
iterative visualization we will determine whether examining success only
based on medal count or differentiating gold, silver, and bronze
victories allows for a more meaningful display of trends. We will also
later group the observations by region of National Olympic Committee, or
`noc`, which reflects what we understand to be country identities today
more accurately than `team` does. Merging in this [secondary
dataset](https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results?select=noc_regions.csv)
provided with the athlete-event level data by Kaggle will allow us to
expand our country labeling from three-letter NOC abbreviations to
complete country names. Additionally, the dataframe in the package
[countrycode](https://vincentarelbundock.github.io/countrycode/) links
countries by their names in various formats to their unicode flag
emojis. Merging this data in will assist us with our visualizations of
this question.

After the above merging and necessary cleaning, we will group the data
by `country`, `sport`, and `date` to compute a new variable called
`medals_total` by taking the sum of either our medal-won indicator or
our medal score assigned to differentiate gold, silver and bronze
victories. These steps should allow us to begin an initial approach to
visualization.

#### Plot 1:

In our first visualization, we will plot `medals_total` on the y-axis
and `date` on the x-axis with lines grouped by `country` and faceting by
`sport`. We will select just a few sports of interest to compare and use
selective color mapping for countries of interest and transparency to
strongly highlight a few countries and make the remaining lines
indistinguishable in the background. If this technique remains visually
overwhelming after prototyping our plot, we will filter to select just a
few countries of interest in each sport and color map only those.

#### Plot 2:

Our second visualization will require historical GDP per capita data by
country. We are interested in attempting to understand how the
nationwide economic factors may be associated with trends in countries’
Olympic performance over time. The external data we have chosen to merge
in comes from the Maddison Project Database, a compilation of
researchers’ work estimating economic growth for individual countries
([Bolt and van
Zanden, 2020](https://ourworldindata.org/grapher/gdp-per-capita-maddison-2020)).

We will create a scatterplot with `gdp_per_capita` on the x axis and
`medals_total` on the y axis. We plan to highlight interesting outliers
with country emojis, and we will facet by `season` only if that reveals
an interesting difference between the economic indicator-athletic
performance association. We will also use an iterative approach to
determine whether selecting one or a few year(s) of interest to maintain
a one-to-one ratio of points to countries or plotting all the data
points (one for each country-year combination) will appear more
informative to the viewer. Alternatively, if we are permitted to produce
an animated plot and animation is feasible given our other aesthetic
goals, we will animate the plot with each frame representing a single
Olympics and year (or Olympics and season if faceting by season proves
to be uninformative).

#### A note on faceting

It is important to note that for several of our proposed plots, we
mention mapping categorical variables with many levels–such as `country`
or `sport`–to visualization tools like faceting and `geom_line()`. It is
crucial to clarify that we will carefully, intentionally choose a subset
of possible countries or sports to visualize in each of these cases
(based on population size, medal count, compelling trends, etc.). We
acknowledge that failing to do so may lead to messy plots that are
difficult to interpret, and thus will prioritize legibility and meaning
in our ultimate visualizations.
