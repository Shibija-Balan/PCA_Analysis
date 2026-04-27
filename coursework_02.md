# Coursework 2


<!--- DO NOT DELETE THIS LINE --->

<!--- METADATA ANCHOR: MA22019-CW2-2026 --->

# Data Preparation Notes

<!--- DO NOT DELETE THIS LINE - DATA PREPARATION NOTES ANCHOR --->

Briefly document the main data-handling decisions that matter for your
analysis. This section may be short prose or one small table.

``` r
library(tidyverse)
library(sf)
library(knitr)

wards <- read_sf("data/city_wards.shp")
profiles <- read_csv("data/ward_profiles.csv" , show_col_types = FALSE)
incidents <- read_csv("data/incident_reports.csv" , show_col_types = FALSE)

#NAs in datasets
na_summary <- tibble(dataset = c("incidents", "ward profiles", "ward polygons"),
  missing_values = c(sum(is.na(incidents)),sum(is.na(profiles)),sum(is.na(wards))))

#conversion and check in spatial
incidents_sf <- incidents %>% 
  st_as_sf( coords = c("x","y"), crs = st_crs(wards) )

#creating recorded and spatial wards left join
incidents_joined <- incidents_sf %>%
  st_join( wards %>% select(ward_id , ward_name) , left = TRUE ) %>% 
  rename( ward_name_recorded = ward_name.x , ward_name_spatial = ward_name.y)

#number of rows where recorded and spatial dont match
discrepancies <- incidents_joined %>% 
  st_drop_geometry() %>% 
  filter(ward_name_recorded != ward_name_spatial) %>% 
  nrow()

#number of incidents in each spatial ward
incident_counts <-  incidents_joined %>% 
  st_drop_geometry() %>%
  count(ward_id, ward_name_spatial, name = "n_incidents")
  
#profiles cleaning 
profiles_clean <- profiles %>%
  mutate(rental_share = parse_number(rental_share),
         ward_name = str_replace_all(ward_name, "-" , " "))

#final data set contain - count and profiles all by spatial crs

wards_data <- wards %>% 
  left_join(
    incident_counts %>% select(ward_id, n_incidents),
    by = "ward_id"
  ) %>%
  mutate(n_incidents = replace_na(n_incidents, 0)) %>%
  left_join(
    profiles_clean %>% select(-ward_name),
    by = "ward_id"
  ) %>% 
  mutate( area_km2 = as.numeric(st_area(geometry))/1000000,
          incident_density =  n_incidents / area_km2)


na_summary
```

    # A tibble: 3 × 2
      dataset       missing_values
      <chr>                  <int>
    1 incidents                  0
    2 ward profiles              6
    3 ward polygons              0

``` r
discrepancies
```

    [1] 39

The incident records are point pattern data, with each row giving an
event location. I converted the incident coordinates to an sf point
object using the ward boundary CRS and spatially joined the points to
ward polygons. This allowed the recorded ward names to be checked
against the coordinate-based ward assignment. Ward-level incident counts
were then calculated using the spatially assigned wards. I converted
rental_share from percentage text to numeric and joined ward-profile
variables by ward_id, avoiding reliance on ward names because some
profile names used hyphens. The ward profile file had 6 missing values:
3 in transport_access and 3 in listed_building_share which were
retained. I also calculated ward area and incident density to compare
wards of different sizes.

# Task 1

<!--- DO NOT DELETE THIS LINE - TASK 1 ANCHOR --->

Identify and investigate the most important spatial patterns in the
incident data.

``` r
# Write your Task 1 code here.
```

Write your Task 1 answer here.

# Task 2

<!--- DO NOT DELETE THIS LINE - TASK 2 ANCHOR --->

Use the available neighbourhood data to develop and justify possible
explanations for the patterns you identified.

``` r
# Write your Task 2 code here.
```

Write your Task 2 answer here.

# Task 3

<!--- DO NOT DELETE THIS LINE - TASK 3 ANCHOR --->

Make a small number of evidence-based recommendations for priority areas
or actions.

``` r
# Write your Task 3 code here.
```

Write your Task 3 answer here.

# References

<!--- DO NOT DELETE THIS LINE - REFERENCES ANCHOR --->

Add references only if needed.

    **Prose Word Count:** 203 words (797 words under the 1000-word limit)
