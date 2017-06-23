<div style='position:relative;float:right;'><img src='r-pinnacle-data-sm.png'></div>

[![CRAN Status Badge](https://www.r-pkg.org/badges/version/pinnacle.data)](https://cran.r-project.org/package=pinnacle.data) [![CRAN Total Downloads](http://cranlogs.r-pkg.org/badges/grand-total/pinnacle.data)](https://cran.r-project.org/package=pinnacle.data) [![CRAN Monthly Downloads](http://cranlogs.r-pkg.org/badges/pinnacle.data)](https://cran.r-project.org/package=pinnacle.data)

# Installing
devtools::install_github('marcoblume/pinnacle.data')

# First steps

```{r}
library(pinnacle.data)
MLB2016

# A tibble: 2,460 × 8
         EventDateTime            TeamName1                     TeamName2 StartingPitcher1 StartingPitcher2 GameScoreTeam1 GameScoreTeam2              Lines
                <dttm>                <chr>                         <chr>            <chr>            <chr>          <int>          <int>             <list>
1  2016-04-03 17:05:00  St. Louis Cardinals            Pittsburgh Pirates     A WAINWRIGHT        F LIRIANO              1              4  <tibble [82 × 9]>
2  2016-04-03 20:05:00    Toronto Blue Jays                Tampa Bay Rays        M STROMAN         C ARCHER              5              3 <tibble [114 × 9]>
3  2016-04-04 00:35:00        New York Mets            Kansas City Royals         M HARVEY        E VOLQUEZ              3              4 <tibble [105 × 9]>
4  2016-04-04 19:05:00      Minnesota Twins             Baltimore Orioles        E SANTANA        C TILLMAN              2              3  <tibble [89 × 9]>
5  2016-04-04 20:05:00     Seattle Mariners                 Texas Rangers      F HERNANDEZ         C HAMELS              2              3 <tibble [114 × 9]>
6  2016-04-04 20:10:00 Washington Nationals                Atlanta Braves       M SCHERZER        J TEHERAN              4              3  <tibble [82 × 9]>
7  2016-04-04 23:05:00  Los Angeles Dodgers              San Diego Padres        C KERSHAW           T ROSS             15              0  <tibble [54 × 9]>
8  2016-04-05 02:05:00         Chicago Cubs Los Angeles Angels of Anaheim        J ARRIETA       G RICHARDS              9              0  <tibble [64 × 9]>
9  2016-04-05 02:05:00    Chicago White Sox             Oakland Athletics           C SALE           S GRAY              4              3  <tibble [92 × 9]>
10 2016-04-05 17:05:00       Houston Astros              New York Yankees        D KEUCHEL          MTANAKA              5              3  <tibble [89 × 9]>
# ... with 2,450 more rows
```

You could compare how the expected runs change depending on which team is home or away.
For example

```{r}
library(tidyverse)
df <- rbind(
MLB2016 %>% 
  filter(TeamName1 == "Toronto Blue Jays",
         TeamName2 == "Boston Red Sox",
         StartingPitcher1 == "M ESTRADA",
         StartingPitcher2 == "R PORCELLO")
,
MLB2016 %>% 
  filter(TeamName2 == "Toronto Blue Jays",
         TeamName1 == "Boston Red Sox",
         StartingPitcher2 == "M ESTRADA",
         StartingPitcher1 == "R PORCELLO")
)

> df$Lines[[1]]$TotalPoints
 [1]  NA 9.5 9.5 9.5 9.5 9.5 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0
[23] 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5
[45] 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5
> df$Lines[[2]]$TotalPoints
 [1]  NA 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 8.5 9.0 9.0 9.0 9.0 9.0
[23] 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0
[45] 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0
[67] 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0 9.0
[89] 9.0 9.0 9.0 9.0 9.0 9.0
```


US 2016 Presidential Election data is also available now

```{r}
> data("USA_Election_2016")
> head(USA_Election_2016)
# A tibble: 6 × 11
      EnteredDateTime      TeamName1    TeamName2 SpreadTeam1 SpreadUS1 SpreadUS2 MoneyUS1 MoneyUS2 TotalPoints TotalUSOver TotalUSUnder
               <dttm>          <chr>        <chr>       <lgl>     <lgl>     <lgl>    <dbl>    <dbl>       <lgl>       <lgl>        <lgl>
1 2016-07-18 02:34:38 Hilary Clinton Donald Trump          NA        NA        NA     -243      212          NA          NA           NA
2 2016-07-18 12:15:42 Hilary Clinton Donald Trump          NA        NA        NA     -251      218          NA          NA           NA
3 2016-07-18 21:49:41 Hilary Clinton Donald Trump          NA        NA        NA     -260      226          NA          NA           NA
4 2016-07-19 14:48:05 Hilary Clinton Donald Trump          NA        NA        NA     -281      243          NA          NA           NA
5 2016-07-21 10:47:46 Hilary Clinton Donald Trump          NA        NA        NA     -275      238          NA          NA           NA
6 2016-07-21 13:09:50 Hilary Clinton Donald Trump          NA        NA        NA     -271      235          NA          NA           NA
```
