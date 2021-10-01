# data

The data file is `olympics_data.csv`.

This dataset was accessed on Kaggle.com and includes data scraped in May 2018 from Sports Reference/OlympStats, sports statistics sites, by Randi Griffin, a Senior Data Scientist at Boston Consulting Group. Moreover, it was selected as part of the TidyTuesday challenge on 7/27/21. Citation information is included at the bottom of this section.

## Olympics

|variable         |description |
|:----------------|:-----------|
|ID               | This is an athlete-specific number. Each athlete is assigned one unique identifying number in the dataset |
|Name             | The name of the athlete competing |
|Sex              | Indicated whether the athlete is Male (M) or Female (F)        | 
|Age            | The age of the athlete in years |
|Height             | The height of the athlete in centimeters|
|Weight             | The weight of the athlete in kilograms |
|Team              | The team (same as the country in most cases) the athlete represents |
|NOC              | The 3-letter National Olympic Committee code associated with each team (indicative of country in most cases) |
|Year              | The year (1896-2016) in which the event took place |
|Season              | The season (Summer or Winter) in which the event took place |
|Games              | The year (1896-2016) and season (Summer or Winter) in which the event took place. This is a character combination of `Year` and `Season`. It is important to note that the Summer and Winter games currently alternate every two years, but used to take place in the same year |
| City             | The city in which the Olympic games for that year/season were hosted  |
| Sport             | The sport the athlete is competing in |
| Event             |  The event the athlete is competing in within a sport|
| Medal             |  Indicates whether a Gold, Silver, or Bronze medal was won. Responses can also take the form NA if no medal was won or there is incomplete information |

## References

Sports Reference 2018, *120 years of Olympic history: athletes and results*, electronic dataset, Kaggle, viewed 16 September 2021, <https://www.kaggle.com/heesoo37/120-years-of-olympic-history-athletes-and-results>
