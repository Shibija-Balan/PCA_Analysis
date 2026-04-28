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
  
#profiles cleaning 
profiles_clean <- profiles %>%
  mutate(rental_share = parse_number(rental_share),
         ward_name = str_replace_all(ward_name, "-" , " "))

na_summary
```

    # A tibble: 3 × 2
      dataset       missing_values
      <chr>                  <int>
    1 incidents                  0
    2 ward profiles              6
    3 ward polygons              0

I loaded the ward boundary polygons, ward profile data and incident
reports. The incident and ward polygon files had no missing values,
while the ward profile file had 6 missing values; these were retained
and handled using available cases where relevant. I converted
rental_share from percentage text to a numeric variable. I also
standardized ward names in the profile file by replacing hyphens with
spaces, although later joins use ward_id rather than ward_name to avoid
relying on name formatting.

# Task 1

<!--- DO NOT DELETE THIS LINE - TASK 1 ANCHOR --->

Identify and investigate the most important spatial patterns in the
incident data.

``` r
library(spatstat)

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

wards_incident <- wards %>% 
  left_join(incident_counts %>% select(ward_id, n_incidents),by = "ward_id") %>%
  mutate(n_incidents = replace_na(n_incidents, 0),
         area_km2 = as.numeric(st_area(geometry))/1000000,
         incident_density =  n_incidents / area_km2)

#kernel-smoothed intensity for ppp and quadrat with 4cm
wards_window <- as.owin(st_union(wards))
incident_coords = st_coordinates(incidents_sf)

incident_ppp = ppp( x = incident_coords[,1] , y =incident_coords[,2] , window = wards_window)

incident_quadrat6 <- quadratcount( incident_ppp, nx=6 , ny=6 )
plot(incident_ppp,pch = 16,cex = 0.25,main = "Quadrat counts of reported incidents")
plot(incident_quadrat6, add = TRUE)
plot(st_geometry(wards),add = TRUE,lwd = 0.5)
```

![](coursework_02_files/figure-commonmark/task-1-code-1.png)

``` r
incident_intensity = density.ppp( x = incident_ppp , edge= TRUE)
plot(incident_intensity,main = "Kernel-smoothed intensity of reported incidents")
plot(st_geometry(wards),add = TRUE,lwd = 0.5)
plot(incident_ppp, add = TRUE, pch = 16,cex = 0.25)
```

![](coursework_02_files/figure-commonmark/task-1-code-2.png)

``` r
top_wards <- wards_incident %>% 
  st_drop_geometry() %>% 
  arrange(desc(n_incidents)) %>% 
  select(ward_id,ward_name, n_incidents, incident_density) %>% 
  slice_head(n=10)
top_wards
```

    # A tibble: 10 × 4
       ward_id ward_name    n_incidents incident_density
       <chr>   <chr>              <int>            <dbl>
     1 W17     Maple Cross          337           223.  
     2 W25     Saffron Lea          110           112.  
     3 W08     Market End            96            17.8 
     4 W11     Hazel Row             95            55.6 
     5 W16     Foxley                57            59.0 
     6 W26     Mill Court            38            17.1 
     7 W13     East Hollow           34            34.3 
     8 W02     Riverstead            33             9.12
     9 W28     Falcon Heath          27             8.80
    10 W22     Willow Bank           26             7.06

``` r
total_incidents = sum(wards_incident$n_incidents)

top_10_share <- wards_incident %>%
  st_drop_geometry() %>% 
  arrange(desc(n_incidents)) %>% 
  slice_head(n =10) %>% 
  summarise( share = (sum(n_incidents)/total_incidents) *100)
top_10_share
```

    # A tibble: 1 × 1
      share
      <dbl>
    1  86.4

``` r
top_5_share <-  wards_incident %>% 
  st_drop_geometry() %>% 
  arrange(desc(n_incidents)) %>% 
  slice_head(n=5) %>% 
  summarise ( share = (sum(n_incidents)/total_incidents)*100)
top_5_share 
```

    # A tibble: 1 × 1
      share
      <dbl>
    1  70.4

The incident records were treated as point pattern data. A 6 × 6 quadrat
count showed strong variation across the city, with the largest counts
in the north-east/eastern cells and several southern or western cells
containing very few or no incidents. This suggests a non-homogeneous
point pattern rather than an even spatial distribution.

The kernel-smoothed intensity map confirms this, with the highest
intensity in the north-east/eastern part of the city and much lower
intensity elsewhere. I then aggregated incidents to wards using the
coordinate-based ward assignment to identify the administrative areas
contributing most to the hotspot. Maple Cross had the highest count,
with 337 incidents, followed by Saffron Lea, Market End, Hazel Row and
Foxley. The top five wards accounted for 70.4% of incidents and the top
ten for 86.4%, confirming that incidents are highly concentrated in a
small number of wards.

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

    **Prose Word Count:** 300 words (700 words under the 1000-word limit)
