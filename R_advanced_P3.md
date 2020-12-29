R\_advanced\_P3
================

## Import Data

``` r
fin = read_csv("./data/Future500.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   ID = col_double(),
    ##   Name = col_character(),
    ##   Industry = col_character(),
    ##   Inception = col_double(),
    ##   Employees = col_double(),
    ##   State = col_character(),
    ##   City = col_character(),
    ##   Revenue = col_character(),
    ##   Expenses = col_character(),
    ##   Profit = col_double(),
    ##   Growth = col_character()
    ## )

``` r
head(fin)
```

    ## # A tibble: 6 x 11
    ##      ID Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <dbl> <chr> <chr>        <dbl>     <dbl> <chr> <chr> <chr>   <chr>     <dbl>
    ## 1     1 Over… Software      2006        25 TN    Fran… $9,684… 1,130,7… 8.55e6
    ## 2     2 Unim… IT Serv…      2009        36 PA    Newt… $14,01… 804,035… 1.32e7
    ## 3     3 Gree… Retail        2012        NA SC    Gree… $9,746… 1,044,3… 8.70e6
    ## 4     4 Blac… IT Serv…      2011        66 CA    Oran… $15,35… 4,631,8… 1.07e7
    ## 5     5 Year… Software      2013        45 WI    Madi… $8,567… 4,374,8… 4.19e6
    ## 6     6 Indi… IT Serv…      2013        60 NJ    Mana… $12,80… 4,626,2… 8.18e6
    ## # … with 1 more variable: Growth <chr>

``` r
tail(fin)
```

    ## # A tibble: 6 x 11
    ##      ID Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <dbl> <chr> <chr>        <dbl>     <dbl> <chr> <chr> <chr>   <chr>     <dbl>
    ## 1   495 Rawf… Financi…      2012       124 CA    Los … $10,62… 2,951,1… 7.67e6
    ## 2   496 Bure… IT Serv…      2009        93 ME    Port… $15,40… 2,833,1… 1.26e7
    ## 3   497 Inve… Constru…      2009        24 MN    Wood… $9,144… 4,755,9… 4.39e6
    ## 4   498 Over… Retail        2011      7125 TX    Fort… $11,13… 5,152,1… 5.98e6
    ## 5   499 Bela… IT Serv…      2010       140 MI    Troy  $17,38… 1,387,7… 1.60e7
    ## 6   500 Allp… IT Serv…      2011        24 CA    Los … $11,94… 689,161… 1.13e7
    ## # … with 1 more variable: Growth <chr>

``` r
str(fin)
```

    ## tibble [500 × 11] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ID       : num [1:500] 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Name     : chr [1:500] "Over-Hex" "Unimattax" "Greenfax" "Blacklane" ...
    ##  $ Industry : chr [1:500] "Software" "IT Services" "Retail" "IT Services" ...
    ##  $ Inception: num [1:500] 2006 2009 2012 2011 2013 ...
    ##  $ Employees: num [1:500] 25 36 NA 66 45 60 116 73 55 25 ...
    ##  $ State    : chr [1:500] "TN" "PA" "SC" "CA" ...
    ##  $ City     : chr [1:500] "Franklin" "Newtown Square" "Greenville" "Orange" ...
    ##  $ Revenue  : chr [1:500] "$9,684,527" "$14,016,543" "$9,746,272" "$15,359,369" ...
    ##  $ Expenses : chr [1:500] "1,130,700 Dollars" "804,035 Dollars" "1,044,375 Dollars" "4,631,808 Dollars" ...
    ##  $ Profit   : num [1:500] 8553827 13212508 8701897 10727561 4193069 ...
    ##  $ Growth   : chr [1:500] "19%" "20%" "16%" "19%" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ID = col_double(),
    ##   ..   Name = col_character(),
    ##   ..   Industry = col_character(),
    ##   ..   Inception = col_double(),
    ##   ..   Employees = col_double(),
    ##   ..   State = col_character(),
    ##   ..   City = col_character(),
    ##   ..   Revenue = col_character(),
    ##   ..   Expenses = col_character(),
    ##   ..   Profit = col_double(),
    ##   ..   Growth = col_character()
    ##   .. )

``` r
summary(fin)
```

    ##        ID            Name             Industry           Inception   
    ##  Min.   :  1.0   Length:500         Length:500         Min.   :1999  
    ##  1st Qu.:125.8   Class :character   Class :character   1st Qu.:2009  
    ##  Median :250.5   Mode  :character   Mode  :character   Median :2011  
    ##  Mean   :250.5                                         Mean   :2010  
    ##  3rd Qu.:375.2                                         3rd Qu.:2012  
    ##  Max.   :500.0                                         Max.   :2014  
    ##                                                        NA's   :1     
    ##    Employees          State               City             Revenue         
    ##  Min.   :   1.00   Length:500         Length:500         Length:500        
    ##  1st Qu.:  27.25   Class :character   Class :character   Class :character  
    ##  Median :  56.00   Mode  :character   Mode  :character   Mode  :character  
    ##  Mean   : 148.61                                                           
    ##  3rd Qu.: 126.00                                                           
    ##  Max.   :7125.00                                                           
    ##  NA's   :2                                                                 
    ##    Expenses             Profit            Growth         
    ##  Length:500         Min.   :   12434   Length:500        
    ##  Class :character   1st Qu.: 3272074   Class :character  
    ##  Mode  :character   Median : 6513366   Mode  :character  
    ##                     Mean   : 6539474                     
    ##                     3rd Qu.: 9303951                     
    ##                     Max.   :19624534                     
    ##                     NA's   :2

Changing from non-factor to factor:

``` r
fin$ID = factor(fin$ID)
#summary(fin)
fin$Inception = factor(fin$Inception)
#str(fin)
```

## Factor Variable Trap (FVT)

### *Converting into Numerics For Chararcters:*

``` r
a = c("12", "13", "14", "12", "12")
#typeof(a)
b = as.numeric(a)
#typeof(b)
```

### *Converting into Numerics For Factors:*

``` r
z = factor(c("12", "13", "14", "12", "12"))
typeof(z)
```

    ## [1] "integer"

``` r
y = as.numeric(z) #Wrong result
```

Correct way :

``` r
x = as.numeric(as.character(z))
typeof(x)
```

    ## [1] "double"

## `sub()` and `gsub()`

``` r
#?sub()
fin$Expenses = gsub(" Dollars", "", fin$Expenses)
fin$Expenses = gsub(",", "", fin$Expenses)
head(fin)
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr> <chr>   <chr>     <dbl>
    ## 1 1     Over… Software 2006             25 TN    Fran… $9,684… 1130700  8.55e6
    ## 2 2     Unim… IT Serv… 2009             36 PA    Newt… $14,01… 804035   1.32e7
    ## 3 3     Gree… Retail   2012             NA SC    Gree… $9,746… 1044375  8.70e6
    ## 4 4     Blac… IT Serv… 2011             66 CA    Oran… $15,35… 4631808  1.07e7
    ## 5 5     Year… Software 2013             45 WI    Madi… $8,567… 4374841  4.19e6
    ## 6 6     Indi… IT Serv… 2013             60 NJ    Mana… $12,80… 4626275  8.18e6
    ## # … with 1 more variable: Growth <chr>

``` r
str(fin) #expenses no longer a factor but character variable
```

    ## tibble [500 × 11] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ID       : Factor w/ 500 levels "1","2","3","4",..: 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Name     : chr [1:500] "Over-Hex" "Unimattax" "Greenfax" "Blacklane" ...
    ##  $ Industry : chr [1:500] "Software" "IT Services" "Retail" "IT Services" ...
    ##  $ Inception: Factor w/ 16 levels "1999","2000",..: 8 11 14 13 15 15 11 15 11 12 ...
    ##  $ Employees: num [1:500] 25 36 NA 66 45 60 116 73 55 25 ...
    ##  $ State    : chr [1:500] "TN" "PA" "SC" "CA" ...
    ##  $ City     : chr [1:500] "Franklin" "Newtown Square" "Greenville" "Orange" ...
    ##  $ Revenue  : chr [1:500] "$9,684,527" "$14,016,543" "$9,746,272" "$15,359,369" ...
    ##  $ Expenses : chr [1:500] "1130700" "804035" "1044375" "4631808" ...
    ##  $ Profit   : num [1:500] 8553827 13212508 8701897 10727561 4193069 ...
    ##  $ Growth   : chr [1:500] "19%" "20%" "16%" "19%" ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ID = col_double(),
    ##   ..   Name = col_character(),
    ##   ..   Industry = col_character(),
    ##   ..   Inception = col_double(),
    ##   ..   Employees = col_double(),
    ##   ..   State = col_character(),
    ##   ..   City = col_character(),
    ##   ..   Revenue = col_character(),
    ##   ..   Expenses = col_character(),
    ##   ..   Profit = col_double(),
    ##   ..   Growth = col_character()
    ##   .. )

When including a special symbol : “$”

``` r
fin$Revenue = gsub("\\$", "", fin$Revenue)
fin$Revenue = gsub(",", "", fin$Revenue)
head(fin)
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr> <chr>   <chr>     <dbl>
    ## 1 1     Over… Software 2006             25 TN    Fran… 9684527 1130700  8.55e6
    ## 2 2     Unim… IT Serv… 2009             36 PA    Newt… 140165… 804035   1.32e7
    ## 3 3     Gree… Retail   2012             NA SC    Gree… 9746272 1044375  8.70e6
    ## 4 4     Blac… IT Serv… 2011             66 CA    Oran… 153593… 4631808  1.07e7
    ## 5 5     Year… Software 2013             45 WI    Madi… 8567910 4374841  4.19e6
    ## 6 6     Indi… IT Serv… 2013             60 NJ    Mana… 128054… 4626275  8.18e6
    ## # … with 1 more variable: Growth <chr>

``` r
fin$Growth = gsub("%", "", fin$Growth)
```

Convert those three variables into numeric:

``` r
fin$Expenses = as.numeric(fin$Expenses)
fin$Revenue = as.numeric(fin$Revenue)
fin$Growth = as.numeric(fin$Growth)
str(fin)
```

    ## tibble [500 × 11] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
    ##  $ ID       : Factor w/ 500 levels "1","2","3","4",..: 1 2 3 4 5 6 7 8 9 10 ...
    ##  $ Name     : chr [1:500] "Over-Hex" "Unimattax" "Greenfax" "Blacklane" ...
    ##  $ Industry : chr [1:500] "Software" "IT Services" "Retail" "IT Services" ...
    ##  $ Inception: Factor w/ 16 levels "1999","2000",..: 8 11 14 13 15 15 11 15 11 12 ...
    ##  $ Employees: num [1:500] 25 36 NA 66 45 60 116 73 55 25 ...
    ##  $ State    : chr [1:500] "TN" "PA" "SC" "CA" ...
    ##  $ City     : chr [1:500] "Franklin" "Newtown Square" "Greenville" "Orange" ...
    ##  $ Revenue  : num [1:500] 9684527 14016543 9746272 15359369 8567910 ...
    ##  $ Expenses : num [1:500] 1130700 804035 1044375 4631808 4374841 ...
    ##  $ Profit   : num [1:500] 8553827 13212508 8701897 10727561 4193069 ...
    ##  $ Growth   : num [1:500] 19 20 16 19 19 22 17 NA 30 20 ...
    ##  - attr(*, "spec")=
    ##   .. cols(
    ##   ..   ID = col_double(),
    ##   ..   Name = col_character(),
    ##   ..   Industry = col_character(),
    ##   ..   Inception = col_double(),
    ##   ..   Employees = col_double(),
    ##   ..   State = col_character(),
    ##   ..   City = col_character(),
    ##   ..   Revenue = col_character(),
    ##   ..   Expenses = col_character(),
    ##   ..   Profit = col_double(),
    ##   ..   Growth = col_character()
    ##   .. )

``` r
summary(fin)
```

    ##        ID          Name             Industry           Inception  
    ##  1      :  1   Length:500         Length:500         2011   : 93  
    ##  2      :  1   Class :character   Class :character   2010   : 83  
    ##  3      :  1   Mode  :character   Mode  :character   2012   : 80  
    ##  4      :  1                                         2013   : 69  
    ##  5      :  1                                         2009   : 60  
    ##  6      :  1                                         (Other):114  
    ##  (Other):494                                         NA's   :  1  
    ##    Employees          State               City              Revenue        
    ##  Min.   :   1.00   Length:500         Length:500         Min.   : 1614585  
    ##  1st Qu.:  27.25   Class :character   Class :character   1st Qu.: 8695702  
    ##  Median :  56.00   Mode  :character   Mode  :character   Median :10647231  
    ##  Mean   : 148.61                                         Mean   :10845170  
    ##  3rd Qu.: 126.00                                         3rd Qu.:13106928  
    ##  Max.   :7125.00                                         Max.   :21810051  
    ##  NA's   :2                                               NA's   :2         
    ##     Expenses           Profit             Growth     
    ##  Min.   :  71219   Min.   :   12434   Min.   :-3.00  
    ##  1st Qu.:2758425   1st Qu.: 3272074   1st Qu.: 8.00  
    ##  Median :4365512   Median : 6513366   Median :15.00  
    ##  Mean   :4310134   Mean   : 6539474   Mean   :14.38  
    ##  3rd Qu.:5832473   3rd Qu.: 9303951   3rd Qu.:20.00  
    ##  Max.   :9860686   Max.   :19624534   Max.   :30.00  
    ##  NA's   :3         NA's   :2          NA's   :1

## Dealing with Missing Data:

1.  Predict with 100% accuracy
2.  Leave as it is
3.  Remove from record entirely
4.  Replace with mean or median(popular)
5.  Fill in by exploring correlations and similarities
6.  Introduce dummy variable for “Missingness”

### What is an NA? - “Not Available/Missing Value”

TRUE = 1 FALSE = 0 NA

``` r
head(fin, 24)
```

    ## # A tibble: 24 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 1     Over… Software 2006             25 TN    Fran…  9.68e6  1130700  8.55e6
    ##  2 2     Unim… IT Serv… 2009             36 PA    Newt…  1.40e7   804035  1.32e7
    ##  3 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ##  4 4     Blac… IT Serv… 2011             66 CA    Oran…  1.54e7  4631808  1.07e7
    ##  5 5     Year… Software 2013             45 WI    Madi…  8.57e6  4374841  4.19e6
    ##  6 6     Indi… IT Serv… 2013             60 NJ    Mana…  1.28e7  4626275  8.18e6
    ##  7 7     Tres… Financi… 2009            116 MO    Clay…  5.39e6  2127984  3.26e6
    ##  8 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ##  9 9     Lamt… IT Serv… 2009             55 CA    San …  1.18e7  6482465  5.27e6
    ## 10 10    Stri… Financi… 2010             25 FL    Boca…  1.23e7   916455  1.14e7
    ## # … with 14 more rows, and 1 more variable: Growth <dbl>

``` r
fin[!complete.cases(fin), ] 
```

    ## # A tibble: 12 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ##  2 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ##  3 11    Cane… Health   2012              6 <NA>  New …  1.06e7  7591189  3.01e6
    ##  4 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ##  5 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ##  6 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ##  7 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ##  8 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ##  9 84    Dril… Software 2010             30 <NA>  San …  7.80e6  2785799  5.01e6
    ## 10 267   Circ… Software 2010             14 <NA>  San …  9.07e6  5929828  3.14e6
    ## 11 332   West… Financi… 2010             NA MI    Troy   1.19e7  5245126  6.62e6
    ## 12 379   Stov… Retail   2013             73 <NA>  New …  1.38e7  5904502  7.91e6
    ## # … with 1 more variable: Growth <dbl>

Update Import:

``` r
fin1 = read.csv("./data/Future500.csv", na.strings = c(""))
head(fin1, 24)
```

    ##    ID            Name            Industry Inception Employees State
    ## 1   1        Over-Hex            Software      2006        25    TN
    ## 2   2       Unimattax         IT Services      2009        36    PA
    ## 3   3        Greenfax              Retail      2012        NA    SC
    ## 4   4       Blacklane         IT Services      2011        66    CA
    ## 5   5        Yearflex            Software      2013        45    WI
    ## 6   6    Indigoplanet         IT Services      2013        60    NJ
    ## 7   7         Treslam  Financial Services      2009       116    MO
    ## 8   8       Rednimdox        Construction      2013        73    NY
    ## 9   9         Lamtone         IT Services      2009        55    CA
    ## 10 10       Stripfind  Financial Services      2010        25    FL
    ## 11 11 Canecorporation              Health      2012         6  <NA>
    ## 12 12        Mattouch         IT Services      2013         6    WA
    ## 13 13       Techdrill              Health      2009         9    MS
    ## 14 14        Techline                <NA>      2006        65    CA
    ## 15 15         Cityace                <NA>      2010        25    CO
    ## 16 16  Kayelectronics              Health      2009       687    NC
    ## 17 17         Ganzlax         IT Services      2011        75    NJ
    ## 18 18     Trantraxlax Government Services      2011        35    VA
    ## 19 19           E-Zim              Retail      2008       320    OH
    ## 20 20        Daltfase            Software      2011        78    NC
    ## 21 21         Hotlane Government Services      2012        87    AL
    ## 22 22      Lathotline              Health        NA       103    VA
    ## 23 23          Lambam         IT Services      2012       210    SC
    ## 24 24          Quozap            Software      2004        21    NJ
    ##              City     Revenue          Expenses   Profit Growth
    ## 1        Franklin  $9,684,527 1,130,700 Dollars  8553827    19%
    ## 2  Newtown Square $14,016,543   804,035 Dollars 13212508    20%
    ## 3      Greenville  $9,746,272 1,044,375 Dollars  8701897    16%
    ## 4          Orange $15,359,369 4,631,808 Dollars 10727561    19%
    ## 5         Madison  $8,567,910 4,374,841 Dollars  4193069    19%
    ## 6       Manalapan $12,805,452 4,626,275 Dollars  8179177    22%
    ## 7         Clayton  $5,387,469 2,127,984 Dollars  3259485    17%
    ## 8        Woodside        <NA>              <NA>       NA   <NA>
    ## 9       San Ramon $11,757,018 6,482,465 Dollars  5274553    30%
    ## 10     Boca Raton $12,329,371   916,455 Dollars 11412916    20%
    ## 11       New York $10,597,009 7,591,189 Dollars  3005820     7%
    ## 12       Bellevue $14,026,934 7,429,377 Dollars  6597557    26%
    ## 13        Flowood $10,573,990 7,435,363 Dollars  3138627     8%
    ## 14      San Ramon $13,898,119 5,470,303 Dollars  8427816    23%
    ## 15     Louisville  $9,254,614 6,249,498 Dollars  3005116     6%
    ## 16        Clayton  $9,451,943 3,878,113 Dollars  5573830     4%
    ## 17         Iselin $14,001,180              <NA> 11901180    18%
    ## 18        Suffolk $11,088,336 5,635,276 Dollars  5453060     7%
    ## 19         Monroe $10,746,451 4,762,319 Dollars  5984132    13%
    ## 20         Durham $10,410,628 6,196,409 Dollars  4214219    17%
    ## 21     Huntsville  $7,978,332 5,686,574 Dollars  2291758     2%
    ## 22         McLean  $9,418,303 7,567,233 Dollars  1851070     2%
    ## 23       Columbia $11,950,148 4,365,512 Dollars  7584636    20%
    ## 24   Collingswood  $8,304,480 7,019,973 Dollars  1284507    20%

``` r
fin1[!complete.cases(fin1), ] 
```

    ##      ID            Name           Industry Inception Employees State
    ## 3     3        Greenfax             Retail      2012        NA    SC
    ## 8     8       Rednimdox       Construction      2013        73    NY
    ## 11   11 Canecorporation             Health      2012         6  <NA>
    ## 14   14        Techline               <NA>      2006        65    CA
    ## 15   15         Cityace               <NA>      2010        25    CO
    ## 17   17         Ganzlax        IT Services      2011        75    NJ
    ## 22   22      Lathotline             Health        NA       103    VA
    ## 44   44       Ganzgreen       Construction      2010       224    TN
    ## 84   84      Drilldrill           Software      2010        30  <NA>
    ## 267 267      Circlechop           Software      2010        14  <NA>
    ## 332 332     Westminster Financial Services      2010        NA    MI
    ## 379 379       Stovepuck             Retail      2013        73  <NA>
    ##              City     Revenue          Expenses   Profit Growth
    ## 3      Greenville  $9,746,272 1,044,375 Dollars  8701897    16%
    ## 8        Woodside        <NA>              <NA>       NA   <NA>
    ## 11       New York $10,597,009 7,591,189 Dollars  3005820     7%
    ## 14      San Ramon $13,898,119 5,470,303 Dollars  8427816    23%
    ## 15     Louisville  $9,254,614 6,249,498 Dollars  3005116     6%
    ## 17         Iselin $14,001,180              <NA> 11901180    18%
    ## 22         McLean  $9,418,303 7,567,233 Dollars  1851070     2%
    ## 44       Franklin        <NA>              <NA>       NA     9%
    ## 84  San Francisco  $7,800,620 2,785,799 Dollars  5014821    17%
    ## 267 San Francisco  $9,067,070 5,929,828 Dollars  3137242    20%
    ## 332          Troy $11,861,652 5,245,126 Dollars  6616526    15%
    ## 379      New York $13,814,975 5,904,502 Dollars  7910473    10%

### Filtering: Non-missing Data with `which()`

``` r
head(fin)
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 1     Over… Software 2006             25 TN    Fran…  9.68e6  1130700 8.55e6
    ## 2 2     Unim… IT Serv… 2009             36 PA    Newt…  1.40e7   804035 1.32e7
    ## 3 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375 8.70e6
    ## 4 4     Blac… IT Serv… 2011             66 CA    Oran…  1.54e7  4631808 1.07e7
    ## 5 5     Year… Software 2013             45 WI    Madi…  8.57e6  4374841 4.19e6
    ## 6 6     Indi… IT Serv… 2013             60 NJ    Mana…  1.28e7  4626275 8.18e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin[fin$Revenue == 9746272, ] 
```

    ## # A tibble: 3 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 3     Gree… Retail   2012             NA SC    Gree… 9746272  1044375 8701897
    ## 2 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA      NA
    ## 3 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA      NA
    ## # … with 1 more variable: Growth <dbl>

``` r
#will compare NA values with 9746272, so produced mysterious NAs.
which(fin$Revenue == 9746272)
```

    ## [1] 3

``` r
#?which()
fin[which(fin$Revenue == 9746272), ]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 3     Gree… Retail   2012             NA SC    Gree… 9746272  1044375 8.70e6
    ## # … with 1 more variable: Growth <dbl>

``` r
#^ select the exact row 
fin[fin$Employees == 45, ]
```

    ## # A tibble: 12 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>  NA            NA NA     
    ##  2 5     Year… Software 2013             45 WI    Madi…  8.57e6  4374841  4.19e6
    ##  3 137   Toug… Retail   2009             45 CA    Burb…  1.24e7  5796075  6.63e6
    ##  4 183   Itte… IT Serv… 2013             45 MN    Minn…  1.11e7  6544488  4.59e6
    ##  5 200   Lala… Retail   2003             45 MN    Gold…  1.25e7  4934351  7.53e6
    ##  6 208   Coun… Constru… 2010             45 FL    Spri…  8.38e6  8213905  1.66e5
    ##  7 245   Pesk… IT Serv… 2010             45 VA    Rich…  1.30e7  4284410  8.73e6
    ##  8 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>  NA            NA NA     
    ##  9 360   Reme… Constru… 2012             45 UT    Lind…  1.09e7  4515112  6.36e6
    ## 10 380   Pick… IT Serv… 2011             45 CO    Denv…  1.48e7  4458447  1.04e7
    ## 11 435   Lucr… IT Serv… 2004             45 VA    Glen…  1.29e7  3512395  9.38e6
    ## 12 487   Genu… Constru… 2007             45 NC    Gree…  8.50e6  5741773  2.76e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin[which(fin$Employees == 45), ]
```

    ## # A tibble: 10 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ##  1 5     Year… Software 2013             45 WI    Madi…  8.57e6  4374841 4.19e6
    ##  2 137   Toug… Retail   2009             45 CA    Burb…  1.24e7  5796075 6.63e6
    ##  3 183   Itte… IT Serv… 2013             45 MN    Minn…  1.11e7  6544488 4.59e6
    ##  4 200   Lala… Retail   2003             45 MN    Gold…  1.25e7  4934351 7.53e6
    ##  5 208   Coun… Constru… 2010             45 FL    Spri…  8.38e6  8213905 1.66e5
    ##  6 245   Pesk… IT Serv… 2010             45 VA    Rich…  1.30e7  4284410 8.73e6
    ##  7 360   Reme… Constru… 2012             45 UT    Lind…  1.09e7  4515112 6.36e6
    ##  8 380   Pick… IT Serv… 2011             45 CO    Denv…  1.48e7  4458447 1.04e7
    ##  9 435   Lucr… IT Serv… 2004             45 VA    Glen…  1.29e7  3512395 9.38e6
    ## 10 487   Genu… Constru… 2007             45 NC    Gree…  8.50e6  5741773 2.76e6
    ## # … with 1 more variable: Growth <dbl>

### Filtering: Using `is.na()` for missing data

Cannot compare things with NAs.

``` r
fin[fin$Expenses == NA, ]
```

    ## # A tibble: 500 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ##  1 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  2 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  3 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  4 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  5 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  6 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  7 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  8 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ##  9 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ## 10 <NA>  <NA>  <NA>     <NA>             NA <NA>  <NA>       NA       NA     NA
    ## # … with 490 more rows, and 1 more variable: Growth <dbl>

``` r
a = c(1, 24, 543, NA, 76, 45, NA)
is.na(a)
```

    ## [1] FALSE FALSE FALSE  TRUE FALSE FALSE  TRUE

``` r
is.na(fin$Expenses)
```

    ##   [1] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
    ##  [13] FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [25] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [37] FALSE FALSE FALSE FALSE FALSE FALSE FALSE  TRUE FALSE FALSE FALSE FALSE
    ##  [49] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [61] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [73] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [85] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ##  [97] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [109] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [121] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [133] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [145] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [157] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [169] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [181] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [193] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [205] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [217] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [229] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [241] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [253] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [265] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [277] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [289] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [301] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [313] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [325] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [337] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [349] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [361] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [373] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [385] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [397] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [409] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [421] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [433] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [445] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [457] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [469] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [481] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE
    ## [493] FALSE FALSE FALSE FALSE FALSE FALSE FALSE FALSE

``` r
fin[is.na(fin$Expenses), ]
```

    ## # A tibble: 3 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ## 2 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ## 3 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ## # … with 1 more variable: Growth <dbl>

``` r
fin[is.na(fin$State), ]
```

    ## # A tibble: 4 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 11    Cane… Health   2012              6 <NA>  New …  1.06e7  7591189 3.01e6
    ## 2 84    Dril… Software 2010             30 <NA>  San …  7.80e6  2785799 5.01e6
    ## 3 267   Circ… Software 2010             14 <NA>  San …  9.07e6  5929828 3.14e6
    ## 4 379   Stov… Retail   2013             73 <NA>  New …  1.38e7  5904502 7.91e6
    ## # … with 1 more variable: Growth <dbl>

### Remove records with missing data:

``` r
fin_backup = fin
fin[!complete.cases(fin), ]
```

    ## # A tibble: 12 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ##  2 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ##  3 11    Cane… Health   2012              6 <NA>  New …  1.06e7  7591189  3.01e6
    ##  4 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ##  5 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ##  6 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ##  7 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ##  8 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ##  9 84    Dril… Software 2010             30 <NA>  San …  7.80e6  2785799  5.01e6
    ## 10 267   Circ… Software 2010             14 <NA>  San …  9.07e6  5929828  3.14e6
    ## 11 332   West… Financi… 2010             NA MI    Troy   1.19e7  5245126  6.62e6
    ## 12 379   Stov… Retail   2013             73 <NA>  New …  1.38e7  5904502  7.91e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin[is.na(fin$Industry), ]
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303 8.43e6
    ## 2 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498 3.01e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin[!is.na(fin$Industry), ] #opposite
```

    ## # A tibble: 498 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 1     Over… Software 2006             25 TN    Fran…  9.68e6  1130700  8.55e6
    ##  2 2     Unim… IT Serv… 2009             36 PA    Newt…  1.40e7   804035  1.32e7
    ##  3 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ##  4 4     Blac… IT Serv… 2011             66 CA    Oran…  1.54e7  4631808  1.07e7
    ##  5 5     Year… Software 2013             45 WI    Madi…  8.57e6  4374841  4.19e6
    ##  6 6     Indi… IT Serv… 2013             60 NJ    Mana…  1.28e7  4626275  8.18e6
    ##  7 7     Tres… Financi… 2009            116 MO    Clay…  5.39e6  2127984  3.26e6
    ##  8 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ##  9 9     Lamt… IT Serv… 2009             55 CA    San …  1.18e7  6482465  5.27e6
    ## 10 10    Stri… Financi… 2010             25 FL    Boca…  1.23e7   916455  1.14e7
    ## # … with 488 more rows, and 1 more variable: Growth <dbl>

``` r
fin_backup = fin_backup[!is.na(fin_backup$Industry), ] 
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 10 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ##  2 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ##  3 11    Cane… Health   2012              6 <NA>  New …  1.06e7  7591189  3.01e6
    ##  4 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ##  5 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ##  6 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ##  7 84    Dril… Software 2010             30 <NA>  San …  7.80e6  2785799  5.01e6
    ##  8 267   Circ… Software 2010             14 <NA>  San …  9.07e6  5929828  3.14e6
    ##  9 332   West… Financi… 2010             NA MI    Troy   1.19e7  5245126  6.62e6
    ## 10 379   Stov… Retail   2013             73 <NA>  New …  1.38e7  5904502  7.91e6
    ## # … with 1 more variable: Growth <dbl>

## Reset Dataframe index

``` r
row.names(fin_backup)
```

    ##   [1] "1"   "2"   "3"   "4"   "5"   "6"   "7"   "8"   "9"   "10"  "11"  "12" 
    ##  [13] "13"  "14"  "15"  "16"  "17"  "18"  "19"  "20"  "21"  "22"  "23"  "24" 
    ##  [25] "25"  "26"  "27"  "28"  "29"  "30"  "31"  "32"  "33"  "34"  "35"  "36" 
    ##  [37] "37"  "38"  "39"  "40"  "41"  "42"  "43"  "44"  "45"  "46"  "47"  "48" 
    ##  [49] "49"  "50"  "51"  "52"  "53"  "54"  "55"  "56"  "57"  "58"  "59"  "60" 
    ##  [61] "61"  "62"  "63"  "64"  "65"  "66"  "67"  "68"  "69"  "70"  "71"  "72" 
    ##  [73] "73"  "74"  "75"  "76"  "77"  "78"  "79"  "80"  "81"  "82"  "83"  "84" 
    ##  [85] "85"  "86"  "87"  "88"  "89"  "90"  "91"  "92"  "93"  "94"  "95"  "96" 
    ##  [97] "97"  "98"  "99"  "100" "101" "102" "103" "104" "105" "106" "107" "108"
    ## [109] "109" "110" "111" "112" "113" "114" "115" "116" "117" "118" "119" "120"
    ## [121] "121" "122" "123" "124" "125" "126" "127" "128" "129" "130" "131" "132"
    ## [133] "133" "134" "135" "136" "137" "138" "139" "140" "141" "142" "143" "144"
    ## [145] "145" "146" "147" "148" "149" "150" "151" "152" "153" "154" "155" "156"
    ## [157] "157" "158" "159" "160" "161" "162" "163" "164" "165" "166" "167" "168"
    ## [169] "169" "170" "171" "172" "173" "174" "175" "176" "177" "178" "179" "180"
    ## [181] "181" "182" "183" "184" "185" "186" "187" "188" "189" "190" "191" "192"
    ## [193] "193" "194" "195" "196" "197" "198" "199" "200" "201" "202" "203" "204"
    ## [205] "205" "206" "207" "208" "209" "210" "211" "212" "213" "214" "215" "216"
    ## [217] "217" "218" "219" "220" "221" "222" "223" "224" "225" "226" "227" "228"
    ## [229] "229" "230" "231" "232" "233" "234" "235" "236" "237" "238" "239" "240"
    ## [241] "241" "242" "243" "244" "245" "246" "247" "248" "249" "250" "251" "252"
    ## [253] "253" "254" "255" "256" "257" "258" "259" "260" "261" "262" "263" "264"
    ## [265] "265" "266" "267" "268" "269" "270" "271" "272" "273" "274" "275" "276"
    ## [277] "277" "278" "279" "280" "281" "282" "283" "284" "285" "286" "287" "288"
    ## [289] "289" "290" "291" "292" "293" "294" "295" "296" "297" "298" "299" "300"
    ## [301] "301" "302" "303" "304" "305" "306" "307" "308" "309" "310" "311" "312"
    ## [313] "313" "314" "315" "316" "317" "318" "319" "320" "321" "322" "323" "324"
    ## [325] "325" "326" "327" "328" "329" "330" "331" "332" "333" "334" "335" "336"
    ## [337] "337" "338" "339" "340" "341" "342" "343" "344" "345" "346" "347" "348"
    ## [349] "349" "350" "351" "352" "353" "354" "355" "356" "357" "358" "359" "360"
    ## [361] "361" "362" "363" "364" "365" "366" "367" "368" "369" "370" "371" "372"
    ## [373] "373" "374" "375" "376" "377" "378" "379" "380" "381" "382" "383" "384"
    ## [385] "385" "386" "387" "388" "389" "390" "391" "392" "393" "394" "395" "396"
    ## [397] "397" "398" "399" "400" "401" "402" "403" "404" "405" "406" "407" "408"
    ## [409] "409" "410" "411" "412" "413" "414" "415" "416" "417" "418" "419" "420"
    ## [421] "421" "422" "423" "424" "425" "426" "427" "428" "429" "430" "431" "432"
    ## [433] "433" "434" "435" "436" "437" "438" "439" "440" "441" "442" "443" "444"
    ## [445] "445" "446" "447" "448" "449" "450" "451" "452" "453" "454" "455" "456"
    ## [457] "457" "458" "459" "460" "461" "462" "463" "464" "465" "466" "467" "468"
    ## [469] "469" "470" "471" "472" "473" "474" "475" "476" "477" "478" "479" "480"
    ## [481] "481" "482" "483" "484" "485" "486" "487" "488" "489" "490" "491" "492"
    ## [493] "493" "494" "495" "496" "497" "498"

``` r
rownames(fin_backup) = 1:nrow(fin_backup)
```

    ## Warning: Setting row names on a tibble is deprecated.

``` r
fin_backup = fin

rownames(fin_backup) = NULL
```

### Replacing Missing Data: Factual Analysis

``` r
fin_backup[is.na(fin_backup$State), ]
```

    ## # A tibble: 4 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 11    Cane… Health   2012              6 <NA>  New …  1.06e7  7591189 3.01e6
    ## 2 84    Dril… Software 2010             30 <NA>  San …  7.80e6  2785799 5.01e6
    ## 3 267   Circ… Software 2010             14 <NA>  San …  9.07e6  5929828 3.14e6
    ## 4 379   Stov… Retail   2013             73 <NA>  New …  1.38e7  5904502 7.91e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[is.na(fin_backup$State) & fin_backup$City == "New York", ]
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 11    Cane… Health   2012              6 <NA>  New …  1.06e7  7591189 3.01e6
    ## 2 379   Stov… Retail   2013             73 <NA>  New …  1.38e7  5904502 7.91e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[is.na(fin_backup$State) & fin_backup$City == "New York", "State" ] = "NY"
#check:
fin_backup[c(11, 379), ]
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 11    Cane… Health   2012              6 NY    New …  1.06e7  7591189 3.01e6
    ## 2 379   Stov… Retail   2013             73 NY    New …  1.38e7  5904502 7.91e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 10 x 11
    ##    ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##    <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ##  1 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ##  2 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ##  3 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ##  4 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ##  5 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ##  6 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ##  7 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ##  8 84    Dril… Software 2010             30 <NA>  San …  7.80e6  2785799  5.01e6
    ##  9 267   Circ… Software 2010             14 <NA>  San …  9.07e6  5929828  3.14e6
    ## 10 332   West… Financi… 2010             NA MI    Troy   1.19e7  5245126  6.62e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[is.na(fin_backup$State) & fin_backup$City == "San Francisco", ]
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 84    Dril… Software 2010             30 <NA>  San … 7800620  2785799 5.01e6
    ## 2 267   Circ… Software 2010             14 <NA>  San … 9067070  5929828 3.14e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[is.na(fin_backup$State) & fin_backup$City == "San Francisco", "State" ] = "CA"

# check:
fin_backup[c(84, 267), ]
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 84    Dril… Software 2010             30 CA    San … 7800620  2785799 5.01e6
    ## 2 267   Circ… Software 2010             14 CA    San … 9067070  5929828 3.14e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 8 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ## 2 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ## 3 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ## 4 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ## 5 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ## 6 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ## 7 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ## 8 332   West… Financi… 2010             NA MI    Troy   1.19e7  5245126  6.62e6
    ## # … with 1 more variable: Growth <dbl>

## Replacing Missing Data : Median Imputation Method

Part 1

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 8 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 3     Gree… Retail   2012             NA SC    Gree…  9.75e6  1044375  8.70e6
    ## 2 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ## 3 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ## 4 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ## 5 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ## 6 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ## 7 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ## 8 332   West… Financi… 2010             NA MI    Troy   1.19e7  5245126  6.62e6
    ## # … with 1 more variable: Growth <dbl>

``` r
#median(fin_backup[,"Employees"], na.rm = TRUE)

lapply(fin_backup[,"Employees"],median, na.rm = TRUE)
```

    ## $Employees
    ## [1] 56

``` r
med_empl_retail = lapply(fin_backup[fin_backup$Industry == "Retail","Employees"],median, na.rm = TRUE)

#typeof(fin_backup[,"Employees"])  #-->list

#mean(fin[,"Employees"],na.rm = TRUE)
lapply(fin_backup[,"Employees"],mean, na.rm = TRUE)
```

    ## $Employees
    ## [1] 148.6104

``` r
lapply(fin_backup[fin_backup$Industry == "Retail","Employees"],mean, na.rm = TRUE)
```

    ## $Employees
    ## [1] 209.2766

``` r
lapply(fin_backup[fin_backup$Industry == "Retail","Employees"],mean, na.rm = TRUE)
```

    ## $Employees
    ## [1] 209.2766

``` r
fin_backup[is.na(fin_backup$Employees) & fin_backup$Industry == "Retail", "Employees"] = med_empl_retail

# check:
fin_backup[3, ]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 3     Gree… Retail   2012             28 SC    Gree… 9746272  1044375 8.70e6
    ## # … with 1 more variable: Growth <dbl>

``` r
lapply(fin_backup[,"Employees"],median, na.rm = TRUE)
```

    ## $Employees
    ## [1] 56

``` r
lapply(fin_backup[,"Employees"],mean, na.rm = TRUE)
```

    ## $Employees
    ## [1] 148.3687

``` r
med_empl_finance = lapply(fin_backup[fin_backup$Industry == "Financial Services","Employees"],median, na.rm = TRUE)

mean_empl_finance = lapply(fin_backup[fin_backup$Industry == "Financial Services","Employees"],median, na.rm = TRUE)

fin_backup[is.na(fin_backup$Employees) & fin_backup$Industry == "Financial Services", "Employees"] = med_empl_finance

#check:

fin_backup[332,]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 332   West… Financi… 2010             80 MI    Troy   1.19e7  5245126 6.62e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ## 2 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ## 3 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ## 4 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ## 5 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ## 6 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ## # … with 1 more variable: Growth <dbl>

Part 2

``` r
lapply(fin_backup[,"Growth"],median, na.rm = TRUE)
```

    ## $Growth
    ## [1] 15

``` r
med_growth_constr = lapply(fin_backup[fin_backup$Industry == "Construction","Growth"],median, na.rm = TRUE)

fin_backup[is.na(fin_backup$Growth) & fin_backup$Industry == "Construction", "Growth"] = med_growth_constr

#check:
fin_backup[8, ]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…      NA       NA     NA
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood… NA            NA NA     
    ## 2 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ## 3 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ## 4 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ## 5 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ## 6 44    Ganz… Constru… 2010            224 TN    Fran… NA            NA NA     
    ## # … with 1 more variable: Growth <dbl>

Part 3 Mini-Exercise

``` r
#Revenue
med_revenue_constr = lapply(fin_backup[fin_backup$Industry == "Construction","Revenue"],median, na.rm = TRUE)

fin_backup[is.na(fin_backup$Revenue) & fin_backup$Industry == "Construction", "Revenue"] = med_revenue_constr

#check:
fin_backup[8, ]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…  9.06e6       NA     NA
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…  9.06e6       NA NA     
    ## 2 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303  8.43e6
    ## 3 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498  3.01e6
    ## 4 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA  1.19e7
    ## 5 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233  1.85e6
    ## 6 44    Ganz… Constru… 2010            224 TN    Fran…  9.06e6       NA NA     
    ## # … with 1 more variable: Growth <dbl>

``` r
#Expenses:
med_expense_constr = lapply(fin_backup[fin_backup$Industry == "Construction","Expenses"],median, na.rm = TRUE)

fin_backup[is.na(fin_backup$Expenses) & is.na(fin_backup$Profit), ] 
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…  9.06e6       NA     NA
    ## 2 44    Ganz… Constru… 2010            224 TN    Fran…  9.06e6       NA     NA
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[is.na(fin_backup$Expenses) & fin_backup$Industry == "Construction", "Expenses"] = med_expense_constr

# check:
fin_backup[8, ]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…  9.06e6 4506976.     NA
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 6 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses  Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>   <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…  9.06e6 4506976. NA     
    ## 2 14    Tech… <NA>     2006             65 CA    San …  1.39e7 5470303   8.43e6
    ## 3 15    City… <NA>     2010             25 CO    Loui…  9.25e6 6249498   3.01e6
    ## 4 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7      NA   1.19e7
    ## 5 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6 7567233   1.85e6
    ## 6 44    Ganz… Constru… 2010            224 TN    Fran…  9.06e6 4506976. NA     
    ## # … with 1 more variable: Growth <dbl>

### Replacing Missing Data : Deriving Values Method

Revenue - Expense = Profit Expense = Revenue - Profit

``` r
fin_backup[is.na(fin_backup$Profit), "Profit"] = fin_backup[is.na(fin_backup$Profit), "Revenue"] - fin_backup[is.na(fin_backup$Profit), "Expenses"]

# check:
fin_backup[c(8, 44), ]
```

    ## # A tibble: 2 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 8     Redn… Constru… 2013             73 NY    Wood…  9.06e6 4506976. 4.55e6
    ## 2 44    Ganz… Constru… 2010            224 TN    Fran…  9.06e6 4506976. 4.55e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 4 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303 8.43e6
    ## 2 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498 3.01e6
    ## 3 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7       NA 1.19e7
    ## 4 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233 1.85e6
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[is.na(fin_backup$Expenses), "Expenses"] = fin_backup[is.na(fin_backup$Expenses), "Revenue"] - fin_backup[is.na(fin_backup$Expenses), "Profit"]

#check:

fin_backup[17,]
```

    ## # A tibble: 1 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 17    Ganz… IT Serv… 2011             75 NJ    Isel…  1.40e7  2100000 1.19e7
    ## # … with 1 more variable: Growth <dbl>

``` r
fin_backup[!complete.cases(fin_backup), ]
```

    ## # A tibble: 3 x 11
    ##   ID    Name  Industry Inception Employees State City  Revenue Expenses Profit
    ##   <fct> <chr> <chr>    <fct>         <dbl> <chr> <chr>   <dbl>    <dbl>  <dbl>
    ## 1 14    Tech… <NA>     2006             65 CA    San …  1.39e7  5470303 8.43e6
    ## 2 15    City… <NA>     2010             25 CO    Loui…  9.25e6  6249498 3.01e6
    ## 3 22    Lath… Health   <NA>            103 VA    McLe…  9.42e6  7567233 1.85e6
    ## # … with 1 more variable: Growth <dbl>
