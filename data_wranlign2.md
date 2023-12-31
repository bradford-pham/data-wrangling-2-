p8105_hw1_bp2678
================
Brady Pham
2333

``` r
library(tidyverse)
```

    ## ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
    ## ✔ dplyr     1.1.3     ✔ readr     2.1.4
    ## ✔ forcats   1.0.0     ✔ stringr   1.5.0
    ## ✔ ggplot2   3.4.3     ✔ tibble    3.2.1
    ## ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
    ## ✔ purrr     1.0.2     
    ## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    ## ✖ dplyr::filter() masks stats::filter()
    ## ✖ dplyr::lag()    masks stats::lag()
    ## ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors

``` r
library(rvest)
```

    ## 
    ## Attaching package: 'rvest'
    ## 
    ## The following object is masked from 'package:readr':
    ## 
    ##     guess_encoding

``` r
library(httr)
library(rvest)
```

imort NSDUH

``` r
nsduh_url = "https://www.samhsa.gov/data/sites/default/files/NSDUHsaeShortTermCHG2015/NSDUHsaeShortTermCHG2015.htm"
```

``` r
nsduh_html = 
  read_html(nsduh_url)
```

``` r
marj_use_df =
nsduh_html |>
  html_table() |>
  first() |>
slice(-1)
```

import star wars

``` r
swm_url = 
  "https://www.imdb.com/list/ls070150896/"

swm_html =
  read_html(swm_url)
```

``` r
swm_title_vec = 
  swm_html |>
  html_elements(".lister-item-header a") |>
  html_text()

swm_gross_rev_vec = 
  swm_html |>
  html_elements(".text-muted .ghost~ .text-muted+ span") |>
  html_text()

swm_df = 
  tibble(
    title = swm_title_vec, gross_rev = swm_gross_rev_vec
  )
```

\##APIs get water data from nyc

``` r
nyc_water_df = 
  GET("https://data.cityofnewyork.us/resource/ia2d-e54m.csv") |>
  content("parsed")
```

    ## Rows: 44 Columns: 4
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl (4): year, new_york_city_population, nyc_consumption_million_gallons_per...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

BRFSS data

``` r
brfss_df = 
  GET("https://data.cdc.gov/resource/acme-vg9e.csv",
      query = list("$limit" = 5000)) |>
  content("parsed")
```

    ## Rows: 5000 Columns: 23
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (16): locationabbr, locationdesc, class, topic, question, response, data...
    ## dbl  (6): year, sample_size, data_value, confidence_limit_low, confidence_li...
    ## lgl  (1): locationid
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

Try it now

``` r
poke_df = 
  GET("https://pokeapi.co/api/v2/pokemon/ditto") |>
  content()
```

2ND PART

``` r
string_vec = c("my", "name", "is", "Brady")

str_detect(string_vec, "Brady")
```

    ## [1] FALSE FALSE FALSE  TRUE

``` r
str_replace(string_vec, "Brady", "brady")
```

    ## [1] "my"    "name"  "is"    "brady"

``` r
string_vec = c(
  "i think we all rule for participating",
  "i think i have been caught",
  "i think this will be quite fun actually",
  "it will be fun, i think"
  )

str_detect(string_vec, "^i think")
```

    ## [1]  TRUE  TRUE  TRUE FALSE
