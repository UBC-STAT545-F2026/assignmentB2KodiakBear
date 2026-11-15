
<!-- README.md is generated from README.Rmd. Please edit that file -->

# assignmentB2KodiakBear

<!-- badges: start -->

<!-- badges: end -->

## Overview

The goal of assignmentB2KodiakBear is to provide a function that assists
users in counting missing values for all columns by group. Given a data
frame `data` and a column `group`, `count_all_missing_by_group()`
creates a new data frame with one row per level of `group`. The first
column of the output data frame contains the levels of `group`, and the
rest of the columns contain the number of missing values for all columns
in `data` except `group`.

## Installation

You can install this package directly by calling
`devtools::install_github("UBC-STAT545-F2026/assignmentB2KodiakBear")`

``` r
devtools::install_github("UBC-STAT545-F2026/assignmentB2KodiakBear")
#> Using GitHub PAT from the git credential store.
#> Downloading GitHub repo UBC-STAT545-F2026/assignmentB2KodiakBear@HEAD
#> ── R CMD build ─────────────────────────────────────────────────────────────────
#>          checking for file 'C:\Users\zhent\AppData\Local\Temp\Rtmpu2ADpU\remotesd618401f29ff\UBC-STAT545-F2026-assignmentB2KodiakBear-14d9b8b/DESCRIPTION' ...     checking for file 'C:\Users\zhent\AppData\Local\Temp\Rtmpu2ADpU\remotesd618401f29ff\UBC-STAT545-F2026-assignmentB2KodiakBear-14d9b8b/DESCRIPTION' ...   ✔  checking for file 'C:\Users\zhent\AppData\Local\Temp\Rtmpu2ADpU\remotesd618401f29ff\UBC-STAT545-F2026-assignmentB2KodiakBear-14d9b8b/DESCRIPTION'
#>       ─  preparing 'assignmentB2KodiakBear':
#>    checking DESCRIPTION meta-information ...     checking DESCRIPTION meta-information ...   ✔  checking DESCRIPTION meta-information
#>   Warning in as.POSIXlt.POSIXct(x, tz) :     Warning in as.POSIXlt.POSIXct(x, tz) :
#>      unknown timezone 'British Columbia Standard Time'
#>       ─  checking for LF line-endings in source and make files and shell scripts
#>   ─  checking for empty or unneeded directories
#>      NB: this package now depends on R (>=        NB: this package now depends on R (>= 4.1.0)
#>      WARNING: Added dependency on R >= 4.1.0 because package code uses the
#>      pipe |> or function shorthand \(...) syntax added in R 4.1.0.
#>      File(s) using such syntax:
#>        'count_all_missing_by_group.R'
#>   ─  building 'assignmentB2KodiakBear_0.0.0.9000.tar.gz'
#>      
#> 
#> Installing package into 'C:/Users/zhent/AppData/Local/Temp/RtmpwFIuDT/temp_libpathcc7072c71ae'
#> (as 'lib' is unspecified)
```

## Package Description

- `R`: A folder that contains the function
  `count_all_missing_by_group()`, which is held in a R script file
- `man`: A folder that contains any figures used in knit files and
  `count_all_missing_by_group.Rd`
- `.Rbuildignore`: A file that tells R CMD Build which files to ignore
- `.gitignore`: A file that tells git which files to ignore
- `DESCRIPTION`: A file containing package metadata and dependencies
- `LICENSE`: A file containing basic license information
- `LICENSE.md`: A knit file containing license details
- `NAMESPACE`: A file that defines the functions within this package
- `README.Rmd`: An unknit version of this README file
- `README.md`: A knit version of this README file
- `assignmentB2KodiakBear.Rproj`: The R project file for this package,
  containing the R setting used when working on this package

## Examples

This example computes the number of missing values in the `airquality`
dataset grouped by the `cyl` column.

``` r
library(assignmentB2KodiakBear)
library(dplyr)
#> 
#> Attaching package: 'dplyr'
#> The following objects are masked from 'package:stats':
#> 
#>     filter, lag
#> The following objects are masked from 'package:base':
#> 
#>     intersect, setdiff, setequal, union
count_all_missing_by_group(airquality, Month)
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

This example has the same output as the last example, but shows off an
alternative way of invoking the `count_all_missing_by_group()`: piping
the dataset into the function.

``` r
library(assignmentB2KodiakBear)
library(dplyr)
airquality |> count_all_missing_by_group(Month) 
#> # A tibble: 5 × 6
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```

The optional `.groups` argument allows us to keep the output grouped by
the grouping column. See example below; notice how the output is a
grouped tibble, rather than the ungrouped tibble output of the earlier
examples.

``` r
library(assignmentB2KodiakBear)
library(dplyr)
count_all_missing_by_group(airquality, Month, .groups = "keep")
#> # A tibble: 5 × 6
#> # Groups:   Month [5]
#>   Month Ozone Solar.R  Wind  Temp   Day
#>   <int> <int>   <int> <int> <int> <int>
#> 1     5     5       4     0     0     0
#> 2     6    21       0     0     0     0
#> 3     7     5       0     0     0     0
#> 4     8     5       3     0     0     0
#> 5     9     1       0     0     0     0
```
