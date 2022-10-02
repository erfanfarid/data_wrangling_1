data_manipulation with ‘dyplr’
================
2022-09-22

``` r
library(tidyverse)
```

    ## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
    ## ✔ ggplot2 3.3.6      ✔ purrr   0.3.4 
    ## ✔ tibble  3.1.7      ✔ dplyr   1.0.10
    ## ✔ tidyr   1.2.1      ✔ stringr 1.4.0 
    ## ✔ readr   2.1.2      ✔ forcats 0.5.2 
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()

``` r
library(readxl)
library(haven)
```

``` r
select(litters_data, group, litter_number, gd0_weight, pups_born_alive)
## # A tibble: 49 × 4
##   group litter_number gd0_weight pups_born_alive
##   <chr> <chr>              <dbl>           <dbl>
## 1 Con7  #85                 19.7               3
## 2 Con7  #1/2/95/2           27                 8
## 3 Con7  #5/5/3/83/3-3       26                 6
## # … with 46 more rows
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
select(litters_data, group:gd_of_birth)
## # A tibble: 49 × 5
##   group litter_number gd0_weight gd18_weight gd_of_birth
##   <chr> <chr>              <dbl>       <dbl>       <dbl>
## 1 Con7  #85                 19.7        34.7          20
## 2 Con7  #1/2/95/2           27          42            19
## 3 Con7  #5/5/3/83/3-3       26          41.4          19
## # … with 46 more rows
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
select(litters_data, -pups_survive)
## # A tibble: 49 × 7
##   group litter_number gd0_weight gd18_weight gd_of_birth pups_born_alive pups_…¹
##   <chr> <chr>              <dbl>       <dbl>       <dbl>           <dbl>   <dbl>
## 1 Con7  #85                 19.7        34.7          20               3       4
## 2 Con7  #1/2/95/2           27          42            19               8       0
## 3 Con7  #5/5/3/83/3-3       26          41.4          19               6       0
## # … with 46 more rows, and abbreviated variable name ¹​pups_dead_birth
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
select(litters_data, GROUP = group, LiTtEr_NuMbEr = litter_number)
## # A tibble: 49 × 2
##   GROUP LiTtEr_NuMbEr
##   <chr> <chr>        
## 1 Con7  #85          
## 2 Con7  #1/2/95/2    
## 3 Con7  #5/5/3/83/3-3
## # … with 46 more rows
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
rename(litters_data, GROUP = group, LiTtEr_NuMbEr = litter_number)
## # A tibble: 49 × 8
##   GROUP LiTtEr_NuMbEr gd0_weight gd18_weight gd_of_birth pups_…¹ pups_…² pups_…³
##   <chr> <chr>              <dbl>       <dbl>       <dbl>   <dbl>   <dbl>   <dbl>
## 1 Con7  #85                 19.7        34.7          20       3       4       3
## 2 Con7  #1/2/95/2           27          42            19       8       0       7
## 3 Con7  #5/5/3/83/3-3       26          41.4          19       6       0       5
## # … with 46 more rows, and abbreviated variable names ¹​pups_born_alive,
## #   ²​pups_dead_birth, ³​pups_survive
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
select(litters_data, starts_with("gd"))
## # A tibble: 49 × 3
##   gd0_weight gd18_weight gd_of_birth
##        <dbl>       <dbl>       <dbl>
## 1       19.7        34.7          20
## 2       27          42            19
## 3       26          41.4          19
## # … with 46 more rows
## # ℹ Use `print(n = ...)` to see more rows
select(litters_data, ends_with("weight"))
## # A tibble: 49 × 2
##   gd0_weight gd18_weight
##        <dbl>       <dbl>
## 1       19.7        34.7
## 2       27          42  
## 3       26          41.4
## # … with 46 more rows
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
select(litters_data, litter_number, pups_survive, everything())
## # A tibble: 49 × 8
##   litter_number pups_survive group gd0_weight gd18_wei…¹ gd_of…² pups_…³ pups_…⁴
##   <chr>                <dbl> <chr>      <dbl>      <dbl>   <dbl>   <dbl>   <dbl>
## 1 #85                      3 Con7        19.7       34.7      20       3       4
## 2 #1/2/95/2                7 Con7        27         42        19       8       0
## 3 #5/5/3/83/3-3            5 Con7        26         41.4      19       6       0
## # … with 46 more rows, and abbreviated variable names ¹​gd18_weight,
## #   ²​gd_of_birth, ³​pups_born_alive, ⁴​pups_dead_birth
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
filter(litters_data, gd_of_birth == 20)
## # A tibble: 32 × 8
##   group litter_number gd0_weight gd18_weight gd_of_birth pups_…¹ pups_…² pups_…³
##   <chr> <chr>              <dbl>       <dbl>       <dbl>   <dbl>   <dbl>   <dbl>
## 1 Con7  #85                 19.7        34.7          20       3       4       3
## 2 Con7  #4/2/95/3-3         NA          NA            20       6       0       6
## 3 Con7  #2/2/95/3-2         NA          NA            20       6       0       4
## # … with 29 more rows, and abbreviated variable names ¹​pups_born_alive,
## #   ²​pups_dead_birth, ³​pups_survive
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
#litter_data2
mutate(litters_data,
        wt_gain = gd18_weight - gd0_weight,
        group = str_to_lower(group),
       # wt_gain_kg = wt_gain * 2.2
)
## # A tibble: 49 × 9
##   group litter_number gd0_weight gd18_…¹ gd_of…² pups_…³ pups_…⁴ pups_…⁵ wt_gain
##   <chr> <chr>              <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
## 1 con7  #85                 19.7    34.7      20       3       4       3    15  
## 2 con7  #1/2/95/2           27      42        19       8       0       7    15  
## 3 con7  #5/5/3/83/3-3       26      41.4      19       6       0       5    15.4
## # … with 46 more rows, and abbreviated variable names ¹​gd18_weight,
## #   ²​gd_of_birth, ³​pups_born_alive, ⁴​pups_dead_birth, ⁵​pups_survive
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
litters_data = 
    read_csv("./data/FAS_litters.csv", col_types = "ccddiiii") %>%
    janitor::clean_names() %>%
    select(-pups_survive) %>%
    mutate(
        wt_gain = gd18_weight - gd0_weight,
        group = str_to_lower(group)) %>%
    drop_na(wt_gain)

litters_data
## # A tibble: 31 × 8
##   group litter_number gd0_weight gd18_weight gd_of_birth pups_…¹ pups_…² wt_gain
##   <chr> <chr>              <dbl>       <dbl>       <int>   <int>   <int>   <dbl>
## 1 con7  #85                 19.7        34.7          20       3       4    15  
## 2 con7  #1/2/95/2           27          42            19       8       0    15  
## 3 con7  #5/5/3/83/3-3       26          41.4          19       6       0    15.4
## # … with 28 more rows, and abbreviated variable names ¹​pups_born_alive,
## #   ²​pups_dead_birth
## # ℹ Use `print(n = ...)` to see more rows
```

``` r
litters_data %>%
  lm(wt_gain ~ pups_born_alive, data = .)
## 
## Call:
## lm(formula = wt_gain ~ pups_born_alive, data = .)
## 
## Coefficients:
##     (Intercept)  pups_born_alive  
##         13.0833           0.6051
```

``` r
skimr::skim(litters_data)
```

|                                                  |              |
|:-------------------------------------------------|:-------------|
| Name                                             | litters_data |
| Number of rows                                   | 31           |
| Number of columns                                | 8            |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |              |
| Column type frequency:                           |              |
| character                                        | 2            |
| numeric                                          | 6            |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |              |
| Group variables                                  | None         |

Data summary

**Variable type: character**

| skim_variable | n_missing | complete_rate | min | max | empty | n_unique | whitespace |
|:--------------|----------:|--------------:|----:|----:|------:|---------:|-----------:|
| group         |         0 |             1 |   4 |   4 |     0 |        5 |          0 |
| litter_number |         0 |             1 |   3 |  13 |     0 |       31 |          0 |

**Variable type: numeric**

| skim_variable   | n_missing | complete_rate |  mean |   sd |   p0 |   p25 |  p50 |  p75 | p100 | hist  |
|:----------------|----------:|--------------:|------:|-----:|-----:|------:|-----:|-----:|-----:|:------|
| gd0_weight      |         0 |             1 | 24.16 | 3.28 | 17.0 | 22.00 | 23.9 | 25.8 | 33.4 | ▃▆▇▅▁ |
| gd18_weight     |         0 |             1 | 41.54 | 4.12 | 33.4 | 38.75 | 42.4 | 43.8 | 52.7 | ▃▃▇▂▁ |
| gd_of_birth     |         0 |             1 | 19.65 | 0.49 | 19.0 | 19.00 | 20.0 | 20.0 | 20.0 | ▅▁▁▁▇ |
| pups_born_alive |         0 |             1 |  7.10 | 1.89 |  3.0 |  6.00 |  8.0 |  8.0 | 11.0 | ▂▃▂▇▁ |
| pups_dead_birth |         0 |             1 |  0.48 | 0.89 |  0.0 |  0.00 |  0.0 |  1.0 |  4.0 | ▇▂▁▁▁ |
| wt_gain         |         0 |             1 | 17.38 | 2.10 | 13.4 | 15.80 | 16.6 | 19.0 | 21.9 | ▂▇▃▃▂ |

## Other data file formats

Read in an excel file

``` r
mlb_df = read_excel("./data/mlb11.xlsx")
```

Read in a SAS file

``` r
pulse_df = read_sas("./data/public_pulse_data.sas7bdat")
```
