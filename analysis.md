Twindemic Analaysis
================

# Data Cleaning

Loading the COVID data from NYC Health.

``` r
caserate_by_zip = read_csv("./data/caserate-by-modzcta.csv")
```

    ## Rows: 70 Columns: 184

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (1): week_ending
    ## dbl (183): CASERATE_CITY, CASERATE_BX, CASERATE_BK, CASERATE_MN, CASERATE_QN...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
vax_by_boro_age = read_csv("./data/coverage-by-boro-age.csv")
```

    ## Rows: 66 Columns: 10

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (2): BOROUGH, AGE_GROUP
    ## dbl  (7): POP_DENOMINATOR, COUNT_PARTIALLY_CUMULATIVE, COUNT_FULLY_CUMULATIV...
    ## date (1): DATE

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
vax_by_boro_demo = read_csv("./data/coverage-by-boro-demo.csv")
```

    ## Rows: 144 Columns: 11

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (3): BOROUGH, AGE_GROUP, RACE_ETHNICITY
    ## dbl  (7): POP_DENOMINATOR, COUNT_PARTIALLY_CUMULATIVE, COUNT_FULLY_CUMULATIV...
    ## date (1): DATE

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
data_by_day = read_csv("./data/data-by-day.csv")
```

    ## Rows: 645 Columns: 67

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr  (1): date_of_interest
    ## dbl (66): CASE_COUNT, PROBABLE_CASE_COUNT, HOSPITALIZED_COUNT, DEATH_COUNT, ...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
doses_by_day = read_csv("./data/doses-by-day.csv")
```

    ## Rows: 358 Columns: 11

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## dbl  (10): ADMIN_DOSE1_DAILY, ADMIN_DOSE1_CUMULATIVE, ADMIN_DOSE2_DAILY, ADM...
    ## date  (1): DATE

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
hosprate_by_zip = read_csv("./data/hosprate-by-modzcta.csv")
```

    ## Rows: 20 Columns: 184

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (1): date
    ## dbl (183): HOSPRATE_Bronx, HOSPRATE_Brooklyn, HOSPRATE_Manhattan, HOSPRATE_Q...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
testrate_by_zip = read_csv("./data/testrate-by-modzcta.csv")
```

    ## Rows: 70 Columns: 184

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (1): week_ending
    ## dbl (183): TESTRATE_CITY, TESTRATE_BX, TESTRATE_BK, TESTRATE_MN, TESTRATE_QN...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
