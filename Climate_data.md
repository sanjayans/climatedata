Visualize Canadian Climate data
================
Sanjayan S
April 13, 2019

Introduction
------------

This is an example of using R to visualize Canadian climate data.

``` r
library(weathercan)
library(weathercan)
library(plotly)
library(data.table)
# plotting Temperature data from Kamloops, BC
weather_data <- as.data.table(weathercan::kamloops)
plot(weather_data$time, weather_data$temp)
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-1-1.png)

<!-- ## Including Plots -->
<!-- You can also embed plots, for example: -->
<!-- ```{r pressure, echo=FALSE} -->
<!-- plot(pressure) -->
<!-- ``` -->
<!-- Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot. -->
