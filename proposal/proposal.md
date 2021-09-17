Project proposal
================
Mr. Palmer’s Penguins

``` r
library(tidyverse)

# load data from tidytuesday site and write to csv in data folder
readr::read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2021/2021-07-27/olympics.csv') %>%
  write_csv(file = paste0(here::here(), "/data/olympics_data.csv"))

# read data from csv
olympics <- read_csv(file = paste0(here::here(), "/data/olympics_data.csv"))
```

## Sarab

## Drew

This dataset was accessed on Kaggle.com and includes data scraped in May
2018 from Sports Reference/OlympStats, sports statistics sites, by Randi
Griffin, a Senior Data Scientist at Boston Consulting Group.

The set, which includes 15 variables and 271,116 observations, provides
insight into the athletes that competed in and results of the Olympic
games from Athens 1896 to Rio 2016. Each observation includes
information about an athlete on a per event basis. Therefore, if an
athlete competes in multiple different athletic events, there will be
multiple observations with each reflecting an individual event. Each
observation details medal results, the athlete’s background (age, sex,
height, weight, team, etc.), and context about the event (where and when
it was held, season, etc.).

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

`ID` - This is a number assigned uniquely to each athlete. A unique
number associated with each athlete

`Name` - The name of the athlete competing.

`Sex` - Indicated whether the athlete is Male (M) or Female (F)

`Age` - The age of the athlete in years.

`Height` - The height of the athlete in centimeters.

`Weight` - The weight of the athlete in kilograms.

`Team` - The team (country in most cases) the athlete represents.

`NOC` - The 3-letter National Olympic Committee associated wit each team
(country in most cases)

`Games` - The year (1896-2016) and season (Summer or Winter) in which
the event took place. This is a character combination of `Year` and
`Season`. It is important to note that the Summer and Winter games
currently alternate every two years, but used to take place in the same
year.

`Year` - The year (1896-2016) in which the event took place. `Season` -
The season (Summer or Winter) in which the event took place.

`City` - The city in which the Olympic games for that year/season were
hosted.

`Sport` - The sport the athlete is competing in.

`Event` - The event the athlete is competing in.

`Medal` - Indicates whether a Gold, Silver, or Bronze medal was one.
Responses can also take the form NA if no medal was won or there is
incomplete information.

We chose this dataset

The reason why you chose this dataset.

We chose this dataset because we think it can provide a lot of good
insights into some of the trends at the Olympics over the past century
as well as provide strong opportunities for our group to develop our
visualization capabilities.

The Olympics have always been a special global event. Countries from
around the world come together to compete in a range of events. This
share commitment to uniting the global community has time and time
allowed ath Ahtletes = what makes them successful Country information
Historical information about events Outcomes

Diversity of information (categorical and numeric = good for analysis,
opportunities to recode some of the existing variables

  - Just finished the olympics

  - Bringing together the global community, often reflective of broader
    social, cultural, and economic happenings in our world

  - 
The two questions you want to answer.

A plan for answering each of the questions including the variables
involved, variables to be created (if any), external data to be merged
in (if any).

## Dataset

A brief description of your dataset including its provenance,
dimensions, etc. as well as the reason why you chose this dataset.

Make sure to load the data and use inline code for some of this
information.

## Questions

The two questions you want to answer.

1.  
## Analysis plan

A plan for answering each of the questions including the variables
involved, variables to be created (if any), external data to be merged
in (if any).
