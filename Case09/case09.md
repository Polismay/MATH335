---
title: "It's About Time"
author: "Polisma Yadav"
date: "November 13, 2021"
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
sales <- read_csv(url("https://byuistats.github.io/M335/data/sales.csv")) %>% 
  mutate(timezone = with_tz(Time, Sys.timezone(location = TRUE))) %>% 
  mutate(hourtime = floor_date(timezone, unit = "second")) %>% 
  mutate(hour_in_day = hour(hourtime)) %>% 
  filter(Amount >= 0)

sales$Name <- str_trim(sales$Name, "both") 
sales$Name <- str_replace_all(sales$Name, "Missing", "NA")

sales <- sales %>% 
  filter(Name != "NA")
```

## Background

We have transaction data for a few businesses that have been in operation for three months. Each of these companies has come to your investment company for a loan to expand their business. Your boss has asked you to go through the transactions for each business and provide daily, weekly, and monthly gross revenue summaries and comparisons. Your boss would like a short write-up with tables and visualizations that help with the decision of which company did the best over the three-month period. You will also need to provide a short paragraph with your recommendation after building your analysis.

This course only looks at understanding and visualizing recorded time series data. If you would like to learn more about forecasting I would recommend Forecasting: Principles and Practice (Links to an external site.) and for a quick introduction read Exploring and Visualizing Time Series.

## Data Wrangling & Visualization


```r
sales %>%  
ggplot(aes(x = timezone, y = Amount)) +
  geom_point() + 
  theme_bw()
```

![](case09_files/figure-html/tidy_plot-1.png)<!-- -->

```r
sales %>% 
ggplot(aes(x = hour_in_day, y = Amount)) + 
  geom_point() +
  theme_bw()
```

![](case09_files/figure-html/tidy_plot-2.png)<!-- -->

```r
sales %>% 
ggplot(aes(x = hour_in_day, y = Amount)) + 
  geom_col() +
  theme_bw()
```

![](case09_files/figure-html/tidy_plot-3.png)<!-- -->

```r
sales %>% 
ggplot(aes(x = hour_in_day, y = Amount)) + 
  geom_point() +
  facet_wrap(~Name) + 
  theme_bw()  
```

![](case09_files/figure-html/tidy_plot-4.png)<!-- -->

```r
sales %>% 
ggplot(aes(x = hour_in_day, y = Amount, color = Name)) + 
  geom_point() +
  geom_line() + 
  theme_bw()  
```

![](case09_files/figure-html/tidy_plot-5.png)<!-- -->


## Conclusions

Plot 1 shows inaccuracies. 

Plot 2 shows the answer to provide an understanding and recommendation for hours of operation. 

Plot 3 shows the solution to we don’t have employee numbers, but sales traffic can help. Provide some visualizations on customer traffic. 

Plot 4 provides a final comparison of the six companies and a final recommendation.

Plot 5 provides a final comparison of the six companies and a final recommendation.