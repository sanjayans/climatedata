Visualize Canadian Climate data
================
Sanjayan Sachithanantham
April 13, 2019

Introduction
------------

This is an example of using R to visualize Canadian climate data. The graph below shows the hourly temperature values at Morden, MB.

``` r
library(weathercan)
library(plotly)
library(data.table)
library(ggplot2)
# downloading weather data for 2018 for Morden, MB. 
#morden_hourly <- weather_dl(station_ids = 29593, start = "2018-01-01", end = "2018-12-31")
#morden_daily <- weather_dl(station_ids = c(3626), interval = "day")

morden_hourly <- read.csv("C:/Users/Sanjay/Desktop/R/climatedata/morden_hourly.csv", stringsAsFactors=FALSE)
morden_hourly <- as.data.table(morden_hourly)
morden_hourly[, time := as.POSIXct(time, format = "%Y-%m-%d %H:%M")]

morden_daily <- read.csv("C:/Users/Sanjay/Desktop/R/climatedata/morden_daily.csv", stringsAsFactors=FALSE)
morden_daily <- as.data.table(morden_daily)
morden_daily[, date := as.POSIXct(date, format = "%Y-%m-%d")]

plot1 <- ggplot(morden_hourly, aes(x = time,
                                  y = temp)) + 
  geom_point()
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-1-1.png)

Let's change the colour of the plot to red.

``` r
plot1 <- ggplot(morden_hourly, aes(x = time,
                                  y = temp)) + 
  geom_point( colour = "red")
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-2-1.png)

Now we can change it to gradient of colours based on temperature.

``` r
plot1 <- ggplot(morden_hourly, aes(x = time,
                                  y = temp, colour = temp)) + 
  geom_point()
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-3-1.png)

Now we add a trendline to see the seasonal changes in temperature.

``` r
plot1 <- ggplot(morden_hourly, aes(x = time,
                                  y = temp, colour = temp)) + 
  geom_point()+
  geom_smooth()
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-4-1.png)

Now we will specify the colours of the gradient we want use it for the temperature. In this example low temperatures in blue and high temperatures in red.

``` r
plot1 <- ggplot(morden_hourly, aes(x = time,
                                  y = temp)) + 
  geom_point(aes(colour = temp)) +
  scale_color_continuous(name = "Temperature",
                         low = "blue", high = "red") +
  geom_smooth()
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-5-1.png)

``` r
longterm_mean <- morden_daily[ , mean(mean_temp, na.rm = TRUE), by = c("month", "day")]
longterm_mean[ , DOY := .I]

plot1 <- ggplot(longterm_mean, aes(x = DOY,
                                  y = V1)) + 
  geom_point(aes(colour = V1)) +
  scale_color_continuous(name = "Temperature",
                         low = "blue", high = "red")
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-6-1.png)

``` r
longterm_mean <- morden_daily[ , mean(mean_temp, na.rm = TRUE), by = c("year")]
longterm_mean[ , DOY := .I]

plot1 <- ggplot(longterm_mean, aes(x = year,
                                  y = V1)) + 
  geom_point(aes(colour = V1)) +
  scale_color_continuous(name = "Temperature",
                         low = "blue", high = "red")
plot1
```

![](Climate_data_files/figure-markdown_github/unnamed-chunk-7-1.png)

<!-- ## Including Plots -->
<!-- You can also embed plots, for example: -->
<!-- ```{r pressure, echo=FALSE} -->
<!-- plot(pressure) -->
<!-- ``` -->
<!-- Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot. -->
