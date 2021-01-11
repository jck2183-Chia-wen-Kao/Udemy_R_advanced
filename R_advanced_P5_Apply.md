R\_advanced\_P5\_Apply
================

## Import Data

``` r
Chicago_F = read.csv("./data/Weather Data/Chicago-F.csv", row.names = 1)
NewYork_F = read.csv("./data/Weather Data/NewYork-F.csv", row.names = 1)
Houston_F = read.csv("./data/Weather Data/Houston-F.csv", row.names = 1)
SanFrancisco_F = read.csv("./data/Weather Data/SanFrancisco-F.csv", row.names = 1)
```

``` r
is.data.frame(Chicago_F)
```

    ## [1] TRUE

### Let’s convert to matrices:

``` r
Chicago_F = as.matrix(Chicago_F)
NewYork_F = as.matrix(NewYork_F)
Houston_F = as.matrix(Houston_F)
SanFrancisco_F = as.matrix(SanFrancisco_F)
```

check:

``` r
is.matrix(Chicago_F)
```

    ## [1] TRUE

## Put all of these data into a list:

``` r
weather_F = list(Chicago = Chicago_F, Houston = Houston_F, NewYork = NewYork_F, SanFrancisco = SanFrancisco_F) 
```

Try

``` r
weather_F[[3]] %>% knitr::kable()
```

|                 |   Jan |    Feb |    Mar |    Apr |    May |   Jun |    Jul |    Aug |    Sep |    Oct |    Nov |    Dec |
| :-------------- | ----: | -----: | -----: | -----: | -----: | ----: | -----: | -----: | -----: | -----: | -----: | -----: |
| AvgHigh\_F      |  39.0 |  42.00 |  50.00 |  60.00 |  71.00 |  79.0 |  85.00 |  83.00 |  76.00 |  65.00 |  54.00 |  44.00 |
| AvgLow\_F       |  26.0 |  29.00 |  35.00 |  44.00 |  55.00 |  64.0 |  70.00 |  69.00 |  61.00 |  50.00 |  41.00 |  32.00 |
| AvgPrecip\_inch |   3.9 |   2.95 |   4.06 |   3.94 |   4.45 |   3.5 |   4.53 |   4.13 |   3.98 |   3.39 |   3.82 |   3.58 |
| DaysWithPrecip  |  11.0 |  10.00 |  12.00 |  11.00 |  11.00 |  10.0 |  11.00 |  10.00 |   8.00 |   8.00 |   9.00 |  10.00 |
| HoursOfSunshine | 154.0 | 171.00 | 213.00 | 237.00 | 268.00 | 289.0 | 302.00 | 271.00 | 235.00 | 213.00 | 169.00 | 155.00 |

``` r
weather_F$NewYork %>% knitr::kable()
```

|                 |   Jan |    Feb |    Mar |    Apr |    May |   Jun |    Jul |    Aug |    Sep |    Oct |    Nov |    Dec |
| :-------------- | ----: | -----: | -----: | -----: | -----: | ----: | -----: | -----: | -----: | -----: | -----: | -----: |
| AvgHigh\_F      |  39.0 |  42.00 |  50.00 |  60.00 |  71.00 |  79.0 |  85.00 |  83.00 |  76.00 |  65.00 |  54.00 |  44.00 |
| AvgLow\_F       |  26.0 |  29.00 |  35.00 |  44.00 |  55.00 |  64.0 |  70.00 |  69.00 |  61.00 |  50.00 |  41.00 |  32.00 |
| AvgPrecip\_inch |   3.9 |   2.95 |   4.06 |   3.94 |   4.45 |   3.5 |   4.53 |   4.13 |   3.98 |   3.39 |   3.82 |   3.58 |
| DaysWithPrecip  |  11.0 |  10.00 |  12.00 |  11.00 |  11.00 |  10.0 |  11.00 |  10.00 |   8.00 |   8.00 |   9.00 |  10.00 |
| HoursOfSunshine | 154.0 | 171.00 | 213.00 | 237.00 | 268.00 | 289.0 | 302.00 | 271.00 | 235.00 | 213.00 | 169.00 | 155.00 |

## Apply Family

  - `apply()` : use on a matrix, either the rows or columns.
  - `tapply()` : use on a vector to extract subgroups and apply a
    function to them by - use on data frames. Same concept as in group
    by in SQL.
  - `eapply()` : use on an environment.
  - `lapply()` : apply a function to elements of a list.
  - `sapply()` : a version of lapply. Can simplify S the result so it’s
    not presented as a list.
  - vapply()\` : has a pre-specified type of return value(V).
  - *replicate* : run a function several times. Usually used with
    generation of random variables.
  - `mapply()`: multivariate version of sapply. Arguments can be
    recycled.
  - `rapply()` : recursive version of lapply.

## Using `apply()`

``` r
apply(Chicago_F, 1, mean)
```

check:

``` r
mean(Chicago_F["DaysWithPrecip", ])
```

    ## [1] 9.916667

Analyze one city:

``` r
apply(Chicago_F, 1, max)
apply(Chicago_F, 1, min)
```

for practice:

``` r
apply(Chicago_F, 2, max) #doesn't make sense, but good practice
apply(Chicago_F, 2, min)
```

Comparison:

``` r
apply(Chicago_F, 1, mean)
apply(Houston_F, 1, mean)
apply(NewYork_F, 1, mean)
apply(SanFrancisco_F, 1, mean)
```

## Recreating the apply function with loops

Find the mean of each row : \#1- via loop.

``` r
output = NULL
for(i in 1:5) { #run cycle
   output[i] = mean(Chicago_F[i,])
}

names(output) = rownames(Chicago_F)
```

2: via apply function:

``` r
apply(Chicago_F, 1, mean)
```

## Using `lapply()`

``` r
t(Chicago_F)
weather_F
t(weather_F$Chicago)
newlist = lapply(weather_F, t) #list (t(weather_F$Chicago), t(weather_F$NewYork)...)
```

Example 2:

``` r
rbind(Chicago_F, NewRow = 1:12)
lapply(weather_F, rbind, NewRow = 1:12)
```

Example 3:

``` r
rowMeans(Chicago_F) # = apply(Chicago_F, 1, mean)
lapply(weather_F, rowMeans)
```

  - `rowMeans()`
  - `colMeans()`
  - `rowSums()`
  - `colSums()`

## Combining `lapply()` with the `[ ]`operator:

``` r
weather_F[[1]][1, 1]
weather_F$Chicago[1, 1]
lapply(weather_F, "[", 1, 1)
lapply(weather_F, "[", 1, )
lapply(weather_F, "[", , 3)
```

## Adding own function

``` r
lapply(weather_F, rowMeans)
lapply(weather_F, function(x) x[1, ])
lapply(weather_F, function(x) x[5, ])
lapply(weather_F, function(x) x[ ,12])
lapply(weather_F, function(z) z[1, ] - z[2, ])
lapply(weather_F, function(z) round((z[1,] - z[2,]) / z[2, ], 2))
```

## Using `sapply()`

AvgHigh\_F for July:

``` r
lapply(weather_F, "[", 1, 7) %>% knitr::kable()
```

<table class="kable_wrapper">

<tbody>

<tr>

<td>

|  x |
| -: |
| 84 |

</td>

<td>

|  x |
| -: |
| 94 |

</td>

<td>

|  x |
| -: |
| 85 |

</td>

<td>

|  x |
| -: |
| 67 |

</td>

</tr>

</tbody>

</table>

``` r
sapply(weather_F, "[", 1, 7) %>% knitr::kable()
```

|              |  x |
| :----------- | -: |
| Chicago      | 84 |
| Houston      | 94 |
| NewYork      | 85 |
| SanFrancisco | 67 |

AvgHigh\_F for 4th quarter:

``` r
lapply(weather_F, "[", 1, 10:12) %>% knitr::kable()
```

<table class="kable_wrapper">

<tbody>

<tr>

<td>

|     |  x |
| :-- | -: |
| Oct | 63 |
| Nov | 48 |
| Dec | 36 |

</td>

<td>

|     |  x |
| :-- | -: |
| Oct | 82 |
| Nov | 73 |
| Dec | 64 |

</td>

<td>

|     |  x |
| :-- | -: |
| Oct | 65 |
| Nov | 54 |
| Dec | 44 |

</td>

<td>

|     |  x |
| :-- | -: |
| Oct | 69 |
| Nov | 63 |
| Dec | 57 |

</td>

</tr>

</tbody>

</table>

``` r
sapply(weather_F, "[", 1, 10:12) %>% knitr::kable()
```

|     | Chicago | Houston | NewYork | SanFrancisco |
| :-- | ------: | ------: | ------: | -----------: |
| Oct |      63 |      82 |      65 |           69 |
| Nov |      48 |      73 |      54 |           63 |
| Dec |      36 |      64 |      44 |           57 |

Another Example:

``` r
lapply(weather_F, rowMeans) %>% knitr::kable()
```

<table class="kable_wrapper">

<tbody>

<tr>

<td>

|                 |          x |
| :-------------- | ---------: |
| AvgHigh\_F      |  59.333333 |
| AvgLow\_F       |  43.250000 |
| AvgPrecip\_inch |   3.253333 |
| DaysWithPrecip  |   9.916667 |
| HoursOfSunshine | 208.666667 |

</td>

<td>

|                 |          x |
| :-------------- | ---------: |
| AvgHigh\_F      |  79.666667 |
| AvgLow\_F       |  60.166667 |
| AvgPrecip\_inch |   4.131667 |
| DaysWithPrecip  |   8.250000 |
| HoursOfSunshine | 214.500000 |

</td>

<td>

|                 |         x |
| :-------------- | --------: |
| AvgHigh\_F      |  62.33333 |
| AvgLow\_F       |  48.00000 |
| AvgPrecip\_inch |   3.85250 |
| DaysWithPrecip  |  10.08333 |
| HoursOfSunshine | 223.08333 |

</td>

<td>

|                 |          x |
| :-------------- | ---------: |
| AvgHigh\_F      |  63.833333 |
| AvgLow\_F       |  50.750000 |
| AvgPrecip\_inch |   1.970000 |
| DaysWithPrecip  |   5.666667 |
| HoursOfSunshine | 245.833333 |

</td>

</tr>

</tbody>

</table>

``` r
sapply(weather_F, rowMeans) %>% round(digits = 2) %>% knitr::kable() #<<Deliverable 1
```

|                 | Chicago | Houston | NewYork | SanFrancisco |
| :-------------- | ------: | ------: | ------: | -----------: |
| AvgHigh\_F      |   59.33 |   79.67 |   62.33 |        63.83 |
| AvgLow\_F       |   43.25 |   60.17 |   48.00 |        50.75 |
| AvgPrecip\_inch |    3.25 |    4.13 |    3.85 |         1.97 |
| DaysWithPrecip  |    9.92 |    8.25 |   10.08 |         5.67 |
| HoursOfSunshine |  208.67 |  214.50 |  223.08 |       245.83 |

Another example:

``` r
lapply(weather_F, function(z) round((z[1,] - z[2,]) / z[2, ], 2)) %>% knitr:: kable()
```

<table class="kable_wrapper">

<tbody>

<tr>

<td>

|     |    x |
| :-- | ---: |
| Jan | 0.78 |
| Feb | 0.71 |
| Mar | 0.53 |
| Apr | 0.44 |
| May | 0.35 |
| Jun | 0.29 |
| Jul | 0.24 |
| Aug | 0.24 |
| Sep | 0.32 |
| Oct | 0.37 |
| Nov | 0.41 |
| Dec | 0.57 |

</td>

<td>

|     |    x |
| :-- | ---: |
| Jan | 0.47 |
| Feb | 0.40 |
| Mar | 0.38 |
| Apr | 0.36 |
| May | 0.26 |
| Jun | 0.23 |
| Jul | 0.25 |
| Aug | 0.25 |
| Sep | 0.29 |
| Oct | 0.34 |
| Nov | 0.40 |
| Dec | 0.42 |

</td>

<td>

|     |    x |
| :-- | ---: |
| Jan | 0.50 |
| Feb | 0.45 |
| Mar | 0.43 |
| Apr | 0.36 |
| May | 0.29 |
| Jun | 0.23 |
| Jul | 0.21 |
| Aug | 0.20 |
| Sep | 0.25 |
| Oct | 0.30 |
| Nov | 0.32 |
| Dec | 0.38 |

</td>

<td>

|     |    x |
| :-- | ---: |
| Jan | 0.24 |
| Feb | 0.28 |
| Mar | 0.27 |
| Apr | 0.29 |
| May | 0.25 |
| Jun | 0.25 |
| Jul | 0.24 |
| Aug | 0.24 |
| Sep | 0.27 |
| Oct | 0.28 |
| Nov | 0.26 |
| Dec | 0.24 |

</td>

</tr>

</tbody>

</table>

``` r
sapply(weather_F, function(z) round((z[1,] - z[2,]) / z[2, ], 2)) %>% knitr::kable()
```

|     | Chicago | Houston | NewYork | SanFrancisco |
| :-- | ------: | ------: | ------: | -----------: |
| Jan |    0.78 |    0.47 |    0.50 |         0.24 |
| Feb |    0.71 |    0.40 |    0.45 |         0.28 |
| Mar |    0.53 |    0.38 |    0.43 |         0.27 |
| Apr |    0.44 |    0.36 |    0.36 |         0.29 |
| May |    0.35 |    0.26 |    0.29 |         0.25 |
| Jun |    0.29 |    0.23 |    0.23 |         0.25 |
| Jul |    0.24 |    0.25 |    0.21 |         0.24 |
| Aug |    0.24 |    0.25 |    0.20 |         0.24 |
| Sep |    0.32 |    0.29 |    0.25 |         0.27 |
| Oct |    0.37 |    0.34 |    0.30 |         0.28 |
| Nov |    0.41 |    0.40 |    0.32 |         0.26 |
| Dec |    0.57 |    0.42 |    0.38 |         0.24 |

``` r
#<<Deliverable 2
```

By the way:

``` r
sapply(weather_F, rowMeans, simplify = FALSE) %>% knitr::kable()# same as lapply
```

<table class="kable_wrapper">

<tbody>

<tr>

<td>

|                 |          x |
| :-------------- | ---------: |
| AvgHigh\_F      |  59.333333 |
| AvgLow\_F       |  43.250000 |
| AvgPrecip\_inch |   3.253333 |
| DaysWithPrecip  |   9.916667 |
| HoursOfSunshine | 208.666667 |

</td>

<td>

|                 |          x |
| :-------------- | ---------: |
| AvgHigh\_F      |  79.666667 |
| AvgLow\_F       |  60.166667 |
| AvgPrecip\_inch |   4.131667 |
| DaysWithPrecip  |   8.250000 |
| HoursOfSunshine | 214.500000 |

</td>

<td>

|                 |         x |
| :-------------- | --------: |
| AvgHigh\_F      |  62.33333 |
| AvgLow\_F       |  48.00000 |
| AvgPrecip\_inch |   3.85250 |
| DaysWithPrecip  |  10.08333 |
| HoursOfSunshine | 223.08333 |

</td>

<td>

|                 |          x |
| :-------------- | ---------: |
| AvgHigh\_F      |  63.833333 |
| AvgLow\_F       |  50.750000 |
| AvgPrecip\_inch |   1.970000 |
| DaysWithPrecip  |   5.666667 |
| HoursOfSunshine | 245.833333 |

</td>

</tr>

</tbody>

</table>

## Nesting `apply()` functions

``` r
apply(Chicago_F, 1, max) %>% knitr::kable()
```

|                 |      x |
| :-------------- | -----: |
| AvgHigh\_F      |  84.00 |
| AvgLow\_F       |  68.00 |
| AvgPrecip\_inch |   4.13 |
| DaysWithPrecip  |  11.00 |
| HoursOfSunshine | 318.00 |

Apply across whole list:

``` r
lapply(weather_F, apply, 1, max) %>% knitr::kable() #preferred
lapply(weather_F, function(x) apply(x, 1, max)) %>% knitr::kable()
```

Tidy up :

``` r
sapply(weather_F, apply, 1, max) %>% knitr::kable()
```

|                 | Chicago | Houston | NewYork | SanFrancisco |
| :-------------- | ------: | ------: | ------: | -----------: |
| AvgHigh\_F      |   84.00 |   94.00 |   85.00 |        70.00 |
| AvgLow\_F       |   68.00 |   75.00 |   70.00 |        55.00 |
| AvgPrecip\_inch |    4.13 |    5.91 |    4.53 |         4.57 |
| DaysWithPrecip  |   11.00 |   10.00 |   12.00 |        11.00 |
| HoursOfSunshine |  318.00 |  294.00 |  302.00 |       330.00 |

``` r
sapply(weather_F, apply, 1, min) %>% knitr::kable()
```

|                 | Chicago | Houston | NewYork | SanFrancisco |
| :-------------- | ------: | ------: | ------: | -----------: |
| AvgHigh\_F      |   32.00 |   63.00 |   39.00 |           57 |
| AvgLow\_F       |   18.00 |   43.00 |   26.00 |           46 |
| AvgPrecip\_inch |    1.93 |    3.19 |    2.95 |            0 |
| DaysWithPrecip  |    8.00 |    6.00 |    8.00 |            1 |
| HoursOfSunshine |  106.00 |  142.00 |  154.00 |          156 |

## `which.max()` and `which.min()` functions

``` r
Chicago_F[1, ] %>% which.max() %>% names()
```

    ## [1] "Jul"

By the sound of it: we will have apply- to iterate over rows of the
matrix, and we will have `lapply()` or `sapply()` - to iterate the
components of the list.

``` r
apply(Chicago_F, 1, function(x) names(which.max(x))) %>% 
    knitr::kable()
```

|                 | x   |
| :-------------- | :-- |
| AvgHigh\_F      | Jul |
| AvgLow\_F       | Jul |
| AvgPrecip\_inch | May |
| DaysWithPrecip  | Mar |
| HoursOfSunshine | Jul |

``` r
lapply(weather_F, function(y) apply(y, 1, function(x) names(which.max(x)))) %>% knitr::kable()
```

<table class="kable_wrapper">

<tbody>

<tr>

<td>

|                 | x   |
| :-------------- | :-- |
| AvgHigh\_F      | Jul |
| AvgLow\_F       | Jul |
| AvgPrecip\_inch | May |
| DaysWithPrecip  | Mar |
| HoursOfSunshine | Jul |

</td>

<td>

|                 | x   |
| :-------------- | :-- |
| AvgHigh\_F      | Jul |
| AvgLow\_F       | Jul |
| AvgPrecip\_inch | Jun |
| DaysWithPrecip  | Jun |
| HoursOfSunshine | Jul |

</td>

<td>

|                 | x   |
| :-------------- | :-- |
| AvgHigh\_F      | Jul |
| AvgLow\_F       | Jul |
| AvgPrecip\_inch | Jul |
| DaysWithPrecip  | Mar |
| HoursOfSunshine | Jul |

</td>

<td>

|                 | x   |
| :-------------- | :-- |
| AvgHigh\_F      | Sep |
| AvgLow\_F       | Aug |
| AvgPrecip\_inch | Dec |
| DaysWithPrecip  | Jan |
| HoursOfSunshine | Jun |

</td>

</tr>

</tbody>

</table>

``` r
sapply(weather_F, function(y) apply(y, 1, function(x) names(which.max(x)))) %>% knitr::kable()
```

|                 | Chicago | Houston | NewYork | SanFrancisco |
| :-------------- | :------ | :------ | :------ | :----------- |
| AvgHigh\_F      | Jul     | Jul     | Jul     | Sep          |
| AvgLow\_F       | Jul     | Jul     | Jul     | Aug          |
| AvgPrecip\_inch | May     | Jun     | Jul     | Dec          |
| DaysWithPrecip  | Mar     | Jun     | Mar     | Jan          |
| HoursOfSunshine | Jul     | Jul     | Jul     | Jun          |
