---
title: "Task 09"
author: "Polisma Yadav"
date: "November 11, 2021"
output:
  html_document:  
    keep_md: true
    toc: true
    toc_float: true
    code_folding: hide
    fig_height: 6
    fig_width: 12
    fig_align: 'center'
---






```r
# Use this R-Chunk to import all your datasets!
carwash <- read_csv(url("https://byuistats.github.io/M335/data/carwash.csv")) %>% 
  mutate(mountain_time = with_tz(time, tzone = "America/Denver")) %>% 
  mutate(hour_time = ceiling_date(mountain_time, unit = "hour")) %>% 
  select(amount, hour_time) %>% 
  na.omit()
```

## Background

A car wash business wants to see if the temperature hurts their bottom line. They have a point of sale data for the months of April, May, June, and July. You will need to aggregate the data into hourly sales totals and merge the sales data together with the temperature data to provide insight into the relationship between temperature and car wash sales. 

## Data Wrangling


```r
temperature_RXE <- riem_measures(station = "RXE",  date_start  = "2016-05-13" ,  date_end  = "2016-07-08" ) %>% 
  mutate(hour_time = ceiling_date(valid, unit = "hour")) %>% 
  select(hour_time, tmpf) %>% 
  na.omit()
```


```r
car_temp <- left_join(carwash, temperature_RXE) %>% 
  mutate(hour_in_day = hour(hour_time))
```



## Data Visualization


```r
car_temp %>% 
ggplot(aes(x = as.factor(hour_in_day), y = amount)) +
  geom_boxplot() +
  geom_jitter(aes(color = tmpf)) +
  labs(x = "Hours of Day", y = "Sales", color = "Temperature") + 
  theme_grey()
```

![](task09_files/figure-html/plot-1.png)<!-- -->

## Conclusions

Graph plot pushed with rest of the files
