
<!-- README.md is generated from README.Rmd. Please edit that file -->

# casewhen

[![Travis build
status](https://travis-ci.org/RLesur/casewhen.svg?branch=master)](https://travis-ci.org/RLesur/casewhen)
[![Coverage
status](https://codecov.io/gh/RLesur/casewhen/branch/master/graph/badge.svg)](https://codecov.io/github/RLesur/casewhen?branch=master)

The goal of casewhen is to create reusable `dplyr::case_when()`
functions.  
`SAS` users may recognise a behavior close to the `SAS FORMATS`

## Installation

You can install the development version from
[GitHub](https://github.com/) with:

``` r
# install.packages("devtools")
devtools::install_github("RLesur/casewhen")
```

## Example

With `casewhen`, you can easily create reusable `dplyr::case_when()`
functions.

``` r
library(dplyr)
library(casewhen)

people <-
  tribble(
    ~name, ~sex, ~seek,
    "Mary", "F", "M",
    "Henry", "M", "F"
  )

cw_sex <- create_case_when(x == "F" ~ "Woman",
                           x == "M" ~ "Man",
                           TRUE ~ as.character(x),
                           vars = "x")

print(cw_sex)
#> <CASE WHEN>
#> 3 conditions:
#> -> x == "F" ~ "Woman"
#> -> x == "M" ~ "Man"
#> -> TRUE ~ as.character(x)

people %>% 
  mutate(sex_label = cw_sex(sex), 
         seek_label = cw_sex(seek))
#> # A tibble: 2 x 5
#>   name  sex   seek  sex_label seek_label
#>   <chr> <chr> <chr> <chr>     <chr>     
#> 1 Mary  F     M     Woman     Man       
#> 2 Henry M     F     Man       Woman
```
