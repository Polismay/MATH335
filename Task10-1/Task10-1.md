---
title: "My Investment is Better Than Yours"
author: "Polisma Yadav"
date: "November 14, 2021"
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

AAPL <- tq_get("AAPL", get = "stock.prices", from = "2020-10-01", to = "2021-11-12") %>%
  select(symbol, date, adjusted)
end <- as_date("2021-11-12")

SE <- tq_get("SE", get = "stock.prices", from = "2020-10-01", to = "2021-11-12") %>%
  select(symbol, date, adjusted)
end <- as_date("2021-11-12")

JMIA <- tq_get("JMIA", get = "stock.prices", from = "2020-10-01", to = "2021-11-12") %>%
  select(symbol, date, adjusted)
end <- as_date("2021-11-12")

WMT <- tq_get("WMT", get = "stock.prices", from = "2020-10-01", to = "2021-11-12") %>%
  select(symbol, date, adjusted)
end <- as_date("2021-11-12")

TSLA <- tq_get("TSLA", get = "stock.prices", from = "2020-10-01", to = "2021-11-12") %>%
  select(symbol, date, adjusted)
end <- as_date("2021-11-12")

MSFT <- tq_get("MSFT", get = "stock.prices", from = "2020-10-01", to = "2021-11-12") %>%
  select(symbol, date, adjusted)
end <- as_date("2021-11-12")
```

## Background

The stock market is overflowing with data. There are many packages in R that allow us to get quick access to information on publicly traded companies. Imagine that you and a friend each purchased about $1,000 of stock in three different stocks at the start of October last year, and you want to compare your performance up to this week. Use the stock shares purchased and share prices to demonstrate how each of you fared over the period you were competing (assuming that you did not change your allocations).

## Data Wrangling and Visualization


```r
# Use this R-Chunk to clean & wrangle your data!

p1 <- AAPL %>%
ggplot(aes(x = date, y = adjusted, color = symbol)) +
  geom_smooth(method = loess, formula = y ~ x, se = FALSE) +
  facet_wrap(~ symbol) +
  scale_color_manual(values = c("blue")) + 
  theme_bw() +
  theme(legend.position = "none")

p2 <- WMT %>%
ggplot(aes(x = date, y = adjusted, color = symbol)) +
  geom_smooth(method = loess, formula = y ~ x, se = FALSE) +
  facet_wrap(~ symbol) +
  scale_color_manual(values = c("red")) + 
  theme_bw() +
  theme(legend.position = "none")

p3 <- JMIA %>%
ggplot(aes(x = date, y = adjusted, color = symbol)) +
  geom_smooth(method = loess, formula = y ~ x, se = FALSE) +
  facet_wrap(~ symbol) +
  scale_color_manual(values = c("blue")) + 
  theme_bw() +
  theme(legend.position = "none")

p4 <- TSLA %>%
ggplot(aes(x = date, y = adjusted, color = symbol)) +
  geom_smooth(method = loess, formula = y ~ x, se = FALSE) +
  facet_wrap(~ symbol) +
  scale_color_manual(values = c("red")) + 
  theme_bw() +
  theme(legend.position = "none")

p5 <- SE %>%
ggplot(aes(x = date, y = adjusted, color = symbol)) +
  geom_smooth(method = loess, formula = y ~ x, se = FALSE) + 
  facet_wrap(~ symbol) +
  scale_color_manual(values = c("blue")) + 
  theme_bw() +
  theme(legend.position = "none")

p6 <- MSFT %>%
ggplot(aes(x = date, y = adjusted, color = symbol)) +
  geom_smooth(method = loess, formula = y ~ x, se = FALSE) + 
  facet_wrap(~ symbol) +
  scale_color_manual(values = c("red")) + 
  theme_bw() +
  theme(legend.position = "none")

grid.arrange(p1, p2, p3, p4, p5, p6, ncol = 2, nrow = 3)
```

![](Task10-1_files/figure-html/plot_data-1.png)<!-- -->
## Conclusions

Beginning of October,2021 me and my friend decided to buy $1000 worth of stock and invest in 3 different stocks each. 

I choose the stocks graphed in Blue, I invested $200 in AAPL, $400 in JMIA and $400 in SE.

My friend choose the stocks graphed in Red, she invested $500 in WMT, $100 in TSLA and $400 in MSFT.

When we compared our earnings, eventhough her charts show a high growth, the amount invested and amount returned were not high as she spent most of her money in buying Walmart(WMT) stock which did not do much good. Me on the other hand invested $400 in JMIA which went from $6 in oct,2020 to $20 in current market which made me a combined total of more money than my friend.