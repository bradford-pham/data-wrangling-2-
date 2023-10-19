p8105_hw1_bp2678
================
Brady Pham
2023-09-22

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