---
title: "Wealth and Life Expectancy (Gapminder)"
author: "Polisma Yadav"
date: "November 30, 2021"
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






## Background

Things learned while making the plot:
Europe has the highest GDP and life Expectancy and Lowest GDP per capita and Life Expectancy is of Africa.
Americas come second to Europe and majority of population is Asia lie under the bottom half of the plot

## Image


```r
gapminder %>%
 filter(country != "Kuwait") %>%
ggplot(mapping = aes(x=lifeExp, y=gdpPercap)) + 
  geom_point(mapping = aes(x=lifeExp, y=gdpPercap, color=continent, size=pop/100000)) +
  facet_wrap(~ year, nrow=1) + 
  scale_y_continuous(trans = "sqrt") + 
  labs(x = "Life Expectancy", y="GDP per capita",color = "Continent", size = "Population (100k)")
```

![](case02_files/figure-html/tidy_data-1.png)<!-- -->


```r
ggsave("image1.png", width = 15, units = "in")
```
