\#\#Exercise 1: Use R to figure out how many elements in the vector
below are greater than 2 . (You need to filter out the NAs first) rooms
\<- c(1, 2, 1, 3, 1, NA, 3, 1, 3, 2, 1, NA, 1, 8, 3, 1, 4, NA, 1, 3, 1,
2, 1, 7, 1, NA)

``` r
#create object
rooms <- c(1, 2, 1, 3, 1, NA, 3, 1, 3, 2, 1, NA, 1, 8, 3, 1, 4, NA, 1, 3, 1, 2, 1, 7, 1, NA)

#remove na's
rooms_clean <- na.omit(rooms)
rooms_clean
```

    ##  [1] 1 2 1 3 1 3 1 3 2 1 1 8 3 1 4 1 3 1 2 1 7 1
    ## attr(,"na.action")
    ## [1]  6 12 18 26
    ## attr(,"class")
    ## [1] "omit"

``` r
#count how many elements are greater than 2
sum(rooms_clean > 2)
```

    ## [1] 8

\#\#Exercise 2: What is the result of running median() function on the
above ‘rooms’ vector? (again, best remove the NAs)

``` r
#apply median function 
median(rooms_clean)
```

    ## [1] 1.5

The median() function on the “rooms” vector (or in my case rooms\_clean,
which has no NA’s) gives 1.5.

\#\#Exercise 3: Inside your R Project (.Rproj), install the ‘tidyverse’
package and use the download.file() and read\_csv() function to read the
SAFI\_clean.csv dataset into your R project as ‘interviews’ digital
object (see instructions in
<a href="https://datacarpentry.org/r-socialsci/setup.html" class="uri">https://datacarpentry.org/r-socialsci/setup.html</a>
and ‘Starting with Data’ section). Take a screenshot of your RStudio
interface showing a) the script you used to create the object, b) the
‘interviews’ object in the Environment and the c) structure of your R
project in the bottom right Files pane. Save the screenshot as an image
and put it in your AUID\_lastname\_firstname repository inside our
Github organisation (github.com/Digital-Methods-HASS). Place here the
URL leading to the screenshot in your repository.

``` r
library(tidyverse)
```

    ## ── Attaching packages ────────────────────────────────────────────────────────────────────────────────────────────── tidyverse 1.3.0 ──

    ## ✓ ggplot2 3.3.2     ✓ purrr   0.3.4
    ## ✓ tibble  3.0.3     ✓ dplyr   1.0.2
    ## ✓ tidyr   1.1.2     ✓ stringr 1.4.0
    ## ✓ readr   1.3.1     ✓ forcats 0.5.0

    ## ── Conflicts ───────────────────────────────────────────────────────────────────────────────────────────────── tidyverse_conflicts() ──
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
setwd("~/Documents/University/5SEMESTER/CULTDATA/RStudio/au601190_dwenger_nicole")

download.file("https://ndownloader.figshare.com/files/11492171",
              "data/SAFI_clean.csv", mode = "wb")

interviews <- read_csv("data/SAFI_clean.csv", na = "NULL")
```

    ## Parsed with column specification:
    ## cols(
    ##   key_ID = col_double(),
    ##   village = col_character(),
    ##   interview_date = col_datetime(format = ""),
    ##   no_membrs = col_double(),
    ##   years_liv = col_double(),
    ##   respondent_wall_type = col_character(),
    ##   rooms = col_double(),
    ##   memb_assoc = col_character(),
    ##   affect_conflicts = col_character(),
    ##   liv_count = col_double(),
    ##   items_owned = col_character(),
    ##   no_meals = col_double(),
    ##   months_lack_food = col_character(),
    ##   instanceID = col_character()
    ## )

![Environment](/Users/nicoledwenger/Documents/University/5SEMESTER/CULTDATA/RStudio/au601190_dwenger_nicole/pictures/environment.png)
![Environment](/Users/nicoledwenger/Documents/University/5SEMESTER/CULTDATA/RStudio/au601190_dwenger_nicole/pictures/files.png)
![Environment](/Users/nicoledwenger/Documents/University/5SEMESTER/CULTDATA/RStudio/au601190_dwenger_nicole/pictures/script.png)
