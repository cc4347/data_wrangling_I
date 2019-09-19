Data Import
================
CC
9/17/2019

\#never use absolute paths; use relative paths instead

\#\#load litters data

``` r
litters_data = read_csv(file = "./data_import_examples/FAS_litters.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
litters_data = janitor::clean_names(litters_data)
names(litters_data)
```

    ## [1] "group"           "litter_number"   "gd0_weight"      "gd18_weight"    
    ## [5] "gd_of_birth"     "pups_born_alive" "pups_dead_birth" "pups_survive"

\#\#load pups data

``` r
pups_data = read_csv(file = "./data_import_examples/FAS_pups.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   `Litter Number` = col_character(),
    ##   Sex = col_double(),
    ##   `PD ears` = col_double(),
    ##   `PD eyes` = col_double(),
    ##   `PD pivot` = col_double(),
    ##   `PD walk` = col_double()
    ## )

``` r
pups_data = janitor::clean_names(pups_data)
pups_data
```

    ## # A tibble: 313 x 6
    ##    litter_number   sex pd_ears pd_eyes pd_pivot pd_walk
    ##    <chr>         <dbl>   <dbl>   <dbl>    <dbl>   <dbl>
    ##  1 #85               1       4      13        7      11
    ##  2 #85               1       4      13        7      12
    ##  3 #1/2/95/2         1       5      13        7       9
    ##  4 #1/2/95/2         1       5      13        8      10
    ##  5 #5/5/3/83/3-3     1       5      13        8      10
    ##  6 #5/5/3/83/3-3     1       5      14        6       9
    ##  7 #5/4/2/95/2       1      NA      14        5       9
    ##  8 #4/2/95/3-3       1       4      13        6       8
    ##  9 #4/2/95/3-3       1       4      13        7       9
    ## 10 #2/2/95/3-2       1       4      NA        8      10
    ## # … with 303 more rows

``` r
tail(pups_data)
```

    ## # A tibble: 6 x 6
    ##   litter_number   sex pd_ears pd_eyes pd_pivot pd_walk
    ##   <chr>         <dbl>   <dbl>   <dbl>    <dbl>   <dbl>
    ## 1 #2/95/2           2       4      12        7       9
    ## 2 #2/95/2           2       3      13        6       8
    ## 3 #2/95/2           2       3      13        7       9
    ## 4 #82/4             2       4      13        7       9
    ## 5 #82/4             2       3      13        7       9
    ## 6 #82/4             2       3      13        7       9

``` r
skimr::skim(pups_data)
```

    ## Skim summary statistics
    ##  n obs: 313 
    ##  n variables: 6 
    ## 
    ## ── Variable type:character ───────────────────────────────────────────────────────────────────────────
    ##       variable missing complete   n min max empty n_unique
    ##  litter_number       0      313 313   3  15     0       49
    ## 
    ## ── Variable type:numeric ─────────────────────────────────────────────────────────────────────────────
    ##  variable missing complete   n  mean   sd p0 p25 p50 p75 p100     hist
    ##   pd_ears      18      295 313  3.68 0.59  2   3   4   4    5 ▁▁▅▁▁▇▁▁
    ##   pd_eyes      13      300 313 12.99 0.62 12  13  13  13   15 ▂▁▇▁▁▂▁▁
    ##  pd_pivot      13      300 313  7.09 1.51  4   6   7   8   12 ▃▆▇▃▂▁▁▁
    ##   pd_walk       0      313 313  9.5  1.34  7   9   9  10   14 ▁▅▇▅▃▂▁▁
    ##       sex       0      313 313  1.5  0.5   1   1   2   2    2 ▇▁▁▁▁▁▁▇

\#\#play with column parsing

``` r
litters_data = read_csv(
  file = "./data_import_examples/FAS_litters.csv")
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
  col_types = cols(
    Group = col_character(),
    `Litter Number` = col_character(),
    `GD0 weight` = col_double(),
    `GD18 weight` = col_double(),
    `GD of Birth` = col_integer(),
    `Pups born alive` = col_integer(),
    `Pups dead @ birth` = col_integer(),
    `Pups survive` = col_integer()
  )
view(litters_data)
```

\#\#Read in an excel file…

``` r
mlb11_data = read_excel(path = "./data_import_examples/mlb11.xlsx")
view(mlb11_data)
```

\#\#Read in
SAS

``` r
pulse_data = haven::read_sas("./data_import_examples/public_pulse_data.sas7bdat")
view(pulse_data)
```

\#\#Import datasets

``` r
library(tidyverse)
litters_data = read_csv("./data_import_examples/FAS_litters.csv",
  col_types = "ccddiiii")
  litters_data = janitor::clean_names(litters_data)
pups_data = read_csv("./data_import_examples/FAS_pups.csv",
  col_types = "ciiiii")
  pups_data = janitor::clean_names(pups_data)
```

\#\#Selecting

``` r
select(litters_data, group, litter_number, gd0_weight, pups_born_alive)
```

    ## # A tibble: 49 x 4
    ##    group litter_number   gd0_weight pups_born_alive
    ##    <chr> <chr>                <dbl>           <int>
    ##  1 Con7  #85                   19.7               3
    ##  2 Con7  #1/2/95/2             27                 8
    ##  3 Con7  #5/5/3/83/3-3         26                 6
    ##  4 Con7  #5/4/2/95/2           28.5               5
    ##  5 Con7  #4/2/95/3-3           NA                 6
    ##  6 Con7  #2/2/95/3-2           NA                 6
    ##  7 Con7  #1/5/3/83/3-3/2       NA                 9
    ##  8 Con8  #3/83/3-3             NA                 9
    ##  9 Con8  #2/95/3               NA                 8
    ## 10 Con8  #3/5/2/2/95           28.5               8
    ## # … with 39 more rows

``` r
select(litters_data, litter_number, gd0_weight, starts_with("pups"))
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight pups_born_alive pups_dead_birth pups_survive
    ##    <chr>                <dbl>           <int>           <int>        <int>
    ##  1 #85                   19.7               3               4            3
    ##  2 #1/2/95/2             27                 8               0            7
    ##  3 #5/5/3/83/3-3         26                 6               0            5
    ##  4 #5/4/2/95/2           28.5               5               1            4
    ##  5 #4/2/95/3-3           NA                 6               0            6
    ##  6 #2/2/95/3-2           NA                 6               0            4
    ##  7 #1/5/3/83/3-3/2       NA                 9               0            9
    ##  8 #3/83/3-3             NA                 9               1            8
    ##  9 #2/95/3               NA                 8               0            8
    ## 10 #3/5/2/2/95           28.5               8               0            8
    ## # … with 39 more rows

``` r
select(litters_data, litter_number, group, gd0_weight)
```

    ## # A tibble: 49 x 3
    ##    litter_number   group gd0_weight
    ##    <chr>           <chr>      <dbl>
    ##  1 #85             Con7        19.7
    ##  2 #1/2/95/2       Con7        27  
    ##  3 #5/5/3/83/3-3   Con7        26  
    ##  4 #5/4/2/95/2     Con7        28.5
    ##  5 #4/2/95/3-3     Con7        NA  
    ##  6 #2/2/95/3-2     Con7        NA  
    ##  7 #1/5/3/83/3-3/2 Con7        NA  
    ##  8 #3/83/3-3       Con8        NA  
    ##  9 #2/95/3         Con8        NA  
    ## 10 #3/5/2/2/95     Con8        28.5
    ## # … with 39 more rows

``` r
select(litters_data, litter_number, group, everything())
```

    ## # A tibble: 49 x 8
    ##    litter_number group gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>         <chr>      <dbl>       <dbl>       <int>           <int>
    ##  1 #85           Con7        19.7        34.7          20               3
    ##  2 #1/2/95/2     Con7        27          42            19               8
    ##  3 #5/5/3/83/3-3 Con7        26          41.4          19               6
    ##  4 #5/4/2/95/2   Con7        28.5        44.1          19               5
    ##  5 #4/2/95/3-3   Con7        NA          NA            20               6
    ##  6 #2/2/95/3-2   Con7        NA          NA            20               6
    ##  7 #1/5/3/83/3-… Con7        NA          NA            20               9
    ##  8 #3/83/3-3     Con8        NA          NA            20               9
    ##  9 #2/95/3       Con8        NA          NA            20               8
    ## 10 #3/5/2/2/95   Con8        28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#those two variables shifted to be the first 2 columns, then all other variables follow

select(litters_data, -group)
```

    ## # A tibble: 49 x 7
    ##    litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 #85                 19.7        34.7          20               3
    ##  2 #1/2/95/2           27          42            19               8
    ##  3 #5/5/3/83/3-3       26          41.4          19               6
    ##  4 #5/4/2/95/2         28.5        44.1          19               5
    ##  5 #4/2/95/3-3         NA          NA            20               6
    ##  6 #2/2/95/3-2         NA          NA            20               6
    ##  7 #1/5/3/83/3-…       NA          NA            20               9
    ##  8 #3/83/3-3           NA          NA            20               9
    ##  9 #2/95/3             NA          NA            20               8
    ## 10 #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#removing a column

select(litters_data, litter_number, gd0_weight:pups_born_alive)
```

    ## # A tibble: 49 x 5
    ##    litter_number   gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr>                <dbl>       <dbl>       <int>           <int>
    ##  1 #85                   19.7        34.7          20               3
    ##  2 #1/2/95/2             27          42            19               8
    ##  3 #5/5/3/83/3-3         26          41.4          19               6
    ##  4 #5/4/2/95/2           28.5        44.1          19               5
    ##  5 #4/2/95/3-3           NA          NA            20               6
    ##  6 #2/2/95/3-2           NA          NA            20               6
    ##  7 #1/5/3/83/3-3/2       NA          NA            20               9
    ##  8 #3/83/3-3             NA          NA            20               9
    ##  9 #2/95/3               NA          NA            20               8
    ## 10 #3/5/2/2/95           28.5        NA            20               8
    ## # … with 39 more rows

``` r
select(litters_data, GROUP = group, litter_number)
```

    ## # A tibble: 49 x 2
    ##    GROUP litter_number  
    ##    <chr> <chr>          
    ##  1 Con7  #85            
    ##  2 Con7  #1/2/95/2      
    ##  3 Con7  #5/5/3/83/3-3  
    ##  4 Con7  #5/4/2/95/2    
    ##  5 Con7  #4/2/95/3-3    
    ##  6 Con7  #2/2/95/3-2    
    ##  7 Con7  #1/5/3/83/3-3/2
    ##  8 Con8  #3/83/3-3      
    ##  9 Con8  #2/95/3        
    ## 10 Con8  #3/5/2/2/95    
    ## # … with 39 more rows

``` r
#changing variable names

rename(litters_data, GROUP = group)
```

    ## # A tibble: 49 x 8
    ##    GROUP litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Con8  #3/83/3-3           NA          NA            20               9
    ##  9 Con8  #2/95/3             NA          NA            20               8
    ## 10 Con8  #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

\#\#Filtering \!\!\!\!\!

``` r
filter(litters_data, group == "Con7")
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #1/2/95/2           27          42            19               8
    ## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 5 Con7  #4/2/95/3-3         NA          NA            20               6
    ## 6 Con7  #2/2/95/3-2         NA          NA            20               6
    ## 7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
# == lgoical operator that asks a question and returns either a true or false type of answer. So group should only be Con7 in this scenario. Are these two things equal to each other? i.e. are there times when group variable is equal to Con7. Group wasn't actually assigned to be equal to Con7.

filter(litters_data, group == "Mod8")
```

    ## # A tibble: 7 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Mod8  #97                 24.5        42.8          20               8
    ## 2 Mod8  #5/93               NA          41.1          20              11
    ## 3 Mod8  #5/93/2             NA          NA            19               8
    ## 4 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 5 Mod8  #7/110/3-2          27.5        46            19               8
    ## 6 Mod8  #2/95/2             28.5        44.5          20               9
    ## 7 Mod8  #82/4               33.4        52.7          20               8
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, gd_of_birth == 20)
```

    ## # A tibble: 32 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  3 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  4 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  5 Con8  #3/83/3-3           NA          NA            20               9
    ##  6 Con8  #2/95/3             NA          NA            20               8
    ##  7 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  8 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ##  9 Con8  #3/5/3/83/3-…       NA          NA            20               8
    ## 10 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # … with 22 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
filter(litters_data, gd_of_birth < 20)
```

    ## # A tibble: 17 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #1/2/95/2           27          42            19               8
    ##  2 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  3 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  4 Con8  #5/4/3/83/3         28          NA            19               9
    ##  5 Con8  #2/2/95/2           NA          NA            19               5
    ##  6 Mod7  #59                 17          33.4          19               8
    ##  7 Mod7  #103                21.4        42.1          19               9
    ##  8 Mod7  #1/82/3-2           NA          NA            19               6
    ##  9 Mod7  #3/83/3-2           NA          NA            19               8
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## 11 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## 12 Mod7  #94/2               24.4        42.9          19               7
    ## 13 Mod7  #62                 19.5        35.9          19               7
    ## 14 Low7  #112                23.9        40.5          19               6
    ## 15 Mod8  #5/93/2             NA          NA            19               8
    ## 16 Mod8  #7/110/3-2          27.5        46            19               8
    ## 17 Low8  #79                 25.4        43.8          19               8
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, gd_of_birth >= 20)
```

    ## # A tibble: 32 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  3 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  4 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  5 Con8  #3/83/3-3           NA          NA            20               9
    ##  6 Con8  #2/95/3             NA          NA            20               8
    ##  7 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  8 Con8  #1/6/2/2/95-2       NA          NA            20               7
    ##  9 Con8  #3/5/3/83/3-…       NA          NA            20               8
    ## 10 Con8  #3/6/2/2/95-3       NA          NA            20               7
    ## # … with 22 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
filter(litters_data, pups_born_alive < 6)
```

    ## # A tibble: 8 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## 3 Con8  #2/2/95/2           NA          NA            19               5
    ## 4 Mod7  #3/82/3-2           28          45.9          20               5
    ## 5 Mod7  #5/3/83/5-2         22.6        37            19               5
    ## 6 Mod7  #106                21.7        37.8          20               5
    ## 7 Low7  #111                25.5        44.6          20               3
    ## 8 Low8  #4/84               21.8        35.2          20               4
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, pups_born_alive < 6, group == "Con7")
```

    ## # A tibble: 2 x 8
    ##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##   <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ## 1 Con7  #85                 19.7        34.7          20               3
    ## 2 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
#filter(litters_data, group == "Con7" | group == "Mod8") This is another way to perform the "or" function, but below is the best option.
filter(litters_data, group %in% c("Con7", "Mod8"))
```

    ## # A tibble: 14 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 Con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 Mod8  #97                 24.5        42.8          20               8
    ##  9 Mod8  #5/93               NA          41.1          20              11
    ## 10 Mod8  #5/93/2             NA          NA            19               8
    ## 11 Mod8  #7/82-3-2           26.9        43.2          20               7
    ## 12 Mod8  #7/110/3-2          27.5        46            19               8
    ## 13 Mod8  #2/95/2             28.5        44.5          20               9
    ## 14 Mod8  #82/4               33.4        52.7          20               8
    ## # … with 2 more variables: pups_dead_birth <int>, pups_survive <int>

``` r
filter(litters_data, gd0_weight + gd18_weight < 70)
```

    ## # A tibble: 23 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Mod7  #59                 17          33.4          19               8
    ##  5 Mod7  #103                21.4        42.1          19               9
    ##  6 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  7 Mod7  #106                21.7        37.8          20               5
    ##  8 Mod7  #94/2               24.4        42.9          19               7
    ##  9 Mod7  #62                 19.5        35.9          19               7
    ## 10 Low7  #84/2               24.3        40.8          20               8
    ## # … with 13 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#addition of variables, less than, greater than certain values

drop_na(litters_data)
```

    ## # A tibble: 31 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Mod7  #59                 17          33.4          19               8
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #3/82/3-2           28          45.9          20               5
    ##  8 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  9 Mod7  #106                21.7        37.8          20               5
    ## 10 Mod7  #94/2               24.4        42.9          19               7
    ## # … with 21 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#drop na in any line of any variable
drop_na(litters_data, gd0_weight)
```

    ## # A tibble: 34 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Con7  #1/2/95/2           27          42            19               8
    ##  3 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #3/5/2/2/95         28.5        NA            20               8
    ##  6 Con8  #5/4/3/83/3         28          NA            19               9
    ##  7 Mod7  #59                 17          33.4          19               8
    ##  8 Mod7  #103                21.4        42.1          19               9
    ##  9 Mod7  #3/82/3-2           28          45.9          20               5
    ## 10 Mod7  #4/2/95/2           23.5        NA            19               9
    ## # … with 24 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#drop na in specific variable
```

\#\#Mutate

``` r
mutate(
  litters_data,
  we_gain = gd18_weight - gd0_weight,
  #make new variable base on existing
  group = str_to_lower(group))
```

    ## # A tibble: 49 x 9
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 con7  #85                 19.7        34.7          20               3
    ##  2 con7  #1/2/95/2           27          42            19               8
    ##  3 con7  #5/5/3/83/3-3       26          41.4          19               6
    ##  4 con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 con7  #4/2/95/3-3         NA          NA            20               6
    ##  6 con7  #2/2/95/3-2         NA          NA            20               6
    ##  7 con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  8 con8  #3/83/3-3           NA          NA            20               9
    ##  9 con8  #2/95/3             NA          NA            20               8
    ## 10 con8  #3/5/2/2/95         28.5        NA            20               8
    ## # … with 39 more rows, and 3 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>, we_gain <dbl>

``` r
  #overwrite existing variables in dataset
```

\#\#Arrange

``` r
arrange(litters_data, pups_born_alive)
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Low7  #111                25.5        44.6          20               3
    ##  3 Low8  #4/84               21.8        35.2          20               4
    ##  4 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  5 Con8  #2/2/95/2           NA          NA            19               5
    ##  6 Mod7  #3/82/3-2           28          45.9          20               5
    ##  7 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  8 Mod7  #106                21.7        37.8          20               5
    ##  9 Con7  #5/5/3/83/3-3       26          41.4          19               6
    ## 10 Con7  #4/2/95/3-3         NA          NA            20               6
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#ordered the dataset according to the number of pups born alive

arrange(litters_data, desc(pups_born_alive))
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Low7  #102                22.6        43.3          20              11
    ##  2 Mod8  #5/93               NA          41.1          20              11
    ##  3 Con7  #1/5/3/83/3-…       NA          NA            20               9
    ##  4 Con8  #3/83/3-3           NA          NA            20               9
    ##  5 Con8  #5/4/3/83/3         28          NA            19               9
    ##  6 Mod7  #103                21.4        42.1          19               9
    ##  7 Mod7  #4/2/95/2           23.5        NA            19               9
    ##  8 Mod7  #8/110/3-2          NA          NA            20               9
    ##  9 Low7  #107                22.6        42.4          20               9
    ## 10 Low7  #98                 23.8        43.8          20               9
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#arrange descending

arrange(litters_data, pups_born_alive, gd0_weight)
```

    ## # A tibble: 49 x 8
    ##    group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive
    ##    <chr> <chr>              <dbl>       <dbl>       <int>           <int>
    ##  1 Con7  #85                 19.7        34.7          20               3
    ##  2 Low7  #111                25.5        44.6          20               3
    ##  3 Low8  #4/84               21.8        35.2          20               4
    ##  4 Mod7  #106                21.7        37.8          20               5
    ##  5 Mod7  #5/3/83/5-2         22.6        37            19               5
    ##  6 Mod7  #3/82/3-2           28          45.9          20               5
    ##  7 Con7  #5/4/2/95/2         28.5        44.1          19               5
    ##  8 Con8  #2/2/95/2           NA          NA            19               5
    ##  9 Low8  #99                 23.5        39            20               6
    ## 10 Low7  #112                23.9        40.5          19               6
    ## # … with 39 more rows, and 2 more variables: pups_dead_birth <int>,
    ## #   pups_survive <int>

``` r
#first arranges by pups born alive variable, then if you have multiple pups with the same number in that variable, it will then arrange by gd0_weight
```

## pipe …

Create a collection of commands

``` r
litters_data =
  read_csv("./data_import_examples/FAS_litters.csv") %>% 
  #hot key for %>% is command shift M
  janitor::clean_names() %>% 
  select(-pups_survive) %>% 
  mutate(
    wt_gain = gd18_weight - gd0_weight,
    group = str_to_lower(group)) %>% 
  drop_na(gd0_weight)
```

    ## Parsed with column specification:
    ## cols(
    ##   Group = col_character(),
    ##   `Litter Number` = col_character(),
    ##   `GD0 weight` = col_double(),
    ##   `GD18 weight` = col_double(),
    ##   `GD of Birth` = col_double(),
    ##   `Pups born alive` = col_double(),
    ##   `Pups dead @ birth` = col_double(),
    ##   `Pups survive` = col_double()
    ## )

``` r
litters_data %>% view()

litters_data %>% pull(gd0_weight) %>% mean
```
