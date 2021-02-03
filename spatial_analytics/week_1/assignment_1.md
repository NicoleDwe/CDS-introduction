Assignment 1: Interactive Maps with Leaflet
================
Nicole Dwenger
2/2/2021

**1. Answer:** Describe a problem or question in your field for which
spatial analysis could be applicable.

Spatial Analysis could be used to analyse the location of e.g. social
media posts. For instance one could look at whether there are more posts
in urban areas compared to rural areas (besides the inequality due to
population). One could also look at relations of certain contents of
posts and their location, e.g. sentiment analysis of posts in different
cities (where are they more positive/negative), or also what are they
about.

**2. Answer:** List 5 data layers that you think are necessary to answer
your question/solve your problem. Find on the internet github.and then
describe examples of two or three of your listed layers.

To analyse e.g. density of tweets in Denmark you need:

  - point layer of tweets and their location (long, lat) in a given
    period of time
  - polygon layer of the borders of Denmark
  - polygon layer of the the regions and/or municipalities/cities in
    Denmark
  - if you wish to take into account the population in the areas, a
    layer of population density in each municipality/city (polygon)
    would also be necessary

**3. Code:** Your colleague has found some ruins during a hike in the
Blue Mountains and recorded the coordinates of structures on her
phone(RCFeature.csv). She would like to map her points but has no
computer or mapping skills. Can you make a map that she can work with
using only a browser? She needs an interactive map that she can download
to her computer and use straightaway.

**4.** Create a standalone .html map in Leaflet showing at least basic
topography and relief, and load in the table of points. Make sure she
can see the FeatureID, FeatureType and Description attributes when she
hovers over the point markers.

``` r
# packages
library(pacman)
p_load(leaflet, htmltools, htmlwidgets, tidyverse, here)

# load data
rcf <- read_csv(here("spatial_analytics/week_1/RCFeature.csv"))
rcf <- rcf %>% filter(!is.na(Longitude))
```

``` r
# define popup-content of markers
popup_content <- paste(
  "<b>Feature ID:</b>", rcf$FeatureID, "<br/>",
  "<b>Feature Type:</b>", rcf$FeatureType, "<br/>",
  "<b>Description:</b>", rcf$Description
)

#simple map
map <- leaflet(width = "100%") %>% 
  addTiles() %>% 
  addMarkers(lng = rcf$Longitude, 
             lat = rcf$Latitude,
             popup = popup_content)
map
```

**5.** Consider adding elements such as minimap() and measure() for
easier map interaction

``` r
additional_map <- leaflet(width = "100%") %>% 
  addTiles() %>% 
  addMarkers(lng = rcf$Longitude, 
             lat = rcf$Latitude,
             popup = popup_content) %>%
  addMiniMap(tiles = "Esri", toggleDisplay = TRUE,
             position = "bottomright") %>%
  addMeasure(
    position = "bottomleft",
    primaryLengthUnit = "meters",
    primaryAreaUnit = "sqmeters",
    activeColor = "#3D535D",
    completedColor = "#7D4479") 

additional_map
```

**6.** Explore differentiating the markers (e.g. by size using Accuracy
field)

``` r
size_map <- leaflet(width = "100%") %>% 
  addTiles() %>% 
  # change to circle markers to adjust the radius
  addCircleMarkers(lng = rcf$Longitude, 
                   lat = rcf$Latitude,
                   popup = popup_content,
                   # added radius to adjust the size based on Accuracy
                   radius = rcf$Accuracy*3) %>%
  addMiniMap(tiles = "Esri", toggleDisplay = TRUE,
             position = "bottomright") %>%
  addMeasure(
    position = "bottomleft",
    primaryLengthUnit = "meters",
    primaryAreaUnit = "sqmeters",
    activeColor = "#3D535D",
    completedColor = "#7D4479") 

size_map
```

**7.** Explore the option of clustering markers with
addMarkers(clusterOptions = markerClusterOptions()). Do you recommend
marker clustering here? I would not cluster in this case, as all sites
are quite close together, thus there is only one main cluster.

``` r
cluster_map <- leaflet(width = "100%") %>% 
  addTiles() %>% 
  addCircleMarkers(lng = rcf$Longitude, 
                   lat = rcf$Latitude,
                   popup = popup_content,
                   radius = rcf$Accuracy*3,
                   clusterOptions = markerClusterOptions()) %>%
  addMiniMap(tiles = "Esri", toggleDisplay = TRUE,
             position = "bottomright") %>%
  addMeasure(
    position = "bottomleft",
    primaryLengthUnit = "meters",
    primaryAreaUnit = "sqmeters",
    activeColor = "#3D535D",
    completedColor = "#7D4479") 

cluster_map
```

**Save final map:**

``` r
library(htmlwidgets)
saveWidget(size_map, "map.html", selfcontained = TRUE)
```
