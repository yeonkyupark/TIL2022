# 2022년 09월  

## TIL20220901  

### 시계열 그래프

```r
if(!require(fpp3)) { install.packages("fpp3"); library(fpp3); }
if(!require(tidyverse)) { install.packages("tidyverse"); library(tidyverse); }
```

```r
mn <- read.csv("metaverse_nft.csv", header = T)
list(head(mn), tail(mn))
```

```r
mn$date <- as_date(mn$date)
mn_ts <- mn %>% 
  mutate(Month = yearweek(date)) %>%
  as_tsibble(index = Month)
mn_ts %>% 
  gg_season(metaverse, labels = "both") +
  labs(y = "hits", title = "Google Trends")
```

```r
mn_ts %>% 
  mutate(Month = yearweek(date)) %>% 
  gg_season(nft, labels = "both") +
  labs(y = "hits", title = "Google Trends")
```
