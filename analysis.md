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

From the datasets above, we will likely compare the following pairs:
caserate/hosprate/testrate\_by\_zip; data/doses\_by\_day;
vax\_by\_boro\_age/demo

Cleaning caserate\_by\_zip:

``` r
caserate_by_zipcode = 
  caserate_by_zip %>% 
  janitor::clean_names() %>% 
  select(week_ending, caserate_10001:caserate_10280) %>% 
  pivot_longer(
    caserate_10001:caserate_10280,
    names_to = "zipcode", 
    names_prefix = "caserate_",
    values_to = "case_rate"
  )

caserate_by_boro = 
  caserate_by_zip %>% 
  janitor::clean_names() %>% 
  select(week_ending, caserate_city:caserate_si) %>% 
  pivot_longer(
    caserate_city:caserate_si,
    names_to = "boro", 
    names_prefix = "caserate_",
    values_to = "case_rate"
  )
```

Cleaning testrate\_by\_zip:

``` r
testrate_by_zipcode = 
  testrate_by_zip %>% 
  janitor::clean_names() %>% 
  select(week_ending, testrate_10001:testrate_10280) %>% 
  pivot_longer(
    testrate_10001:testrate_10280,
    names_to = "zipcode", 
    names_prefix = "testrate_",
    values_to = "test_rate"
  )

testrate_by_boro = 
  testrate_by_zip %>% 
  janitor::clean_names() %>% 
  select(week_ending, testrate_city:testrate_si) %>% 
  pivot_longer(
    testrate_city:testrate_si,
    names_to = "boro", 
    names_prefix = "testrate_",
    values_to = "test_rate"
  )
```

Cleaning hosprate\_by\_zip:

``` r
hosprate_by_zipcode = 
  hosprate_by_zip %>% 
  janitor::clean_names() %>% 
  select(date, hosprate_10001:hosprate_10280) %>% 
  pivot_longer(
    hosprate_10001:hosprate_10280,
    names_to = "zipcode", 
    names_prefix = "hosprate_",
    values_to = "hosp_rate"
  )

hosprate_by_boro = 
  hosprate_by_zip %>% 
  janitor::clean_names() %>% 
  select(date, hosprate_bronx:hosprate_citywide) %>% 
  pivot_longer(
    hosprate_bronx:hosprate_citywide,
    names_to = "boro", 
    names_prefix = "hosprate_",
    values_to = "hosp_rate"
  )
```

Cleaning vax\_by\_boro\_age/demo: \* need help deleting apostrophe in
age\_group

``` r
vax_by_boro_age_df = 
  vax_by_boro_age %>% 
  janitor::clean_names() %>% 
  filter(age_group %in% c("'18-24", "'25-34", "'35-44", "'45-54", "'55-64", "'65-74", "'75-84", "'85+") )

vax_by_boro_demo_df = 
  vax_by_boro_demo %>% 
  janitor::clean_names() %>% 
  filter(age_group %in% c("'18-44", "'45-64", "'65+", "All ages") )
```

Cleaning data/doses\_by\_day:

``` r
doses_by_day_df = 
  doses_by_day %>% 
  janitor::clean_names()

data_by_day_df = 
  data_by_day %>% 
  janitor::clean_names()
```

Loading NYC Locations Providing Seasonal Flu Vaccinations/ Emergency
Department Visits and Admissions for Influenza-like Illness/ Census
Selected Social Characterisics

``` r
flu_vaxx_loc = read_csv("./data/New_York_City_Locations_Providing_Seasonal_Flu_Vaccinations.csv")
```

    ## Warning: One or more parsing issues, see `problems()` for details

    ## Rows: 885 Columns: 26

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (14): Service Category, Service Type, Walk-in, Insurance, Children, Faci...
    ## dbl  (5): OBJECTID, A, Latitude, Longitude, ZIP Code
    ## lgl  (7): Monday, Tuesday, Wednesday, Thursday, Friday, Saturday, Sunday

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
census_social = read_csv("./data/censuszip_selected_social_characterisitcs.csv")
```

    ## New names:
    ## * NAME -> NAME...1
    ## * NAME -> NAME...615

    ## Rows: 1796 Columns: 615

    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr (615): NAME...1, DP02_0001E, DP02_0001M, DP02_0001PE, DP02_0001PM, DP02_...

    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
