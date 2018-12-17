---
title: "Polygon Map"
author: "Ben Gonzalez"
date: "3/9/2017"

---

# How to create a polygon map with popups in R Studio. 


### Step 1: Let's get our data.

The shape files we need are available on the Tiger Files part of the census website. Here they have shape files for any state, county, and even road files. We are going to download the files directly, then load them into a temp directory. 

Census Tiger Files: ftp://ftp2.census.gov/geo/tiger/TIGER2016/

####File 1

````
    {r,warning=FALSE,message=FALSE}
    tmp <- tempdir()

    url <- "ftp://ftp2.census.gov/geo/tiger/TIGER2016/SLDL/tl_2016_17_sldl.zip"

    file <- basename(url)

    download.file(url, file)

    unzip(file, exdir = tmp)
````

#### File 2

````
    {r,warning=FALSE,message=FALSE}

    tmptwo <- tempdir()

    url <- "ftp://ftp2.census.gov/geo/tiger/TIGER2016/SLDU/tl_2016_17_sldu.zip"

    file <- basename(url)

    download.file(url, file)

    unzip(file, exdir = tmptwo)
````

#### File 3

````
    {r,warning=FALSE,message=FALSE}

    tmpthree <- tempdir()

    url <- "ftp://ftp2.census.gov/geo/tiger/TIGER2016/COUNTY/tl_2016_us_county.zip"

    file <- basename(url)

    download.file(url, file)

    unzip(file, exdir = tmpthree)

````



### Step 2: Install the needed packages into R.

Utilize the code below to download the necessary packages to create, merge, and build new datasets. 

````
{r,warning=FALSE,message=FALSE}
install.packages(c("rgdal","leaflet","reshape","reshape2","dplyr","RcolorBrewer"),dependencies = TRUE)


````

### Step 3: Load the libraries into R.

````
    {r,warning=FALSE,message=FALSE}
    library(rgdal)
    library(leaflet)
    library(reshape)
    library(reshape2)
    library(dplyr)
    library(RColorBrewer)
````

### Step 4: Create a color palette

We are going to create a generic color palette we can use for our map. 

````

    pal3 <- colorNumeric(c("red", "green", "blue"), 1:10)
    
````


### Step 5: Read in our data

We are now going to read our shapefiles into R. We wil be using the 'rgdal' package to do so. Our 'dsn' is where the files are stored, and the 'layer' is the name of the file we need to retrieve.

````
{r,warning=FALSE,message=FALSE}
### Illinois Congressional Districts 

    houseillower <- readOGR(dsn = tmp,layer = "tl_2016_17_sldl", verbose = FALSE, encoding = "UTF-8")

    houseilupper <- readOGR(dsn = tmptwo,layer = "tl_2016_17_sldu", verbose = FALSE, encoding = "UTF-8")

    countyil <- readOGR(dsn = tmpthree,layer = "tl_2016_us_county", verbose = FALSE, encoding = "UTF-8")

````


### Step 6: Subset our data into dataframes.

We are going to subset our shape files into a data frame. This will allow us to merge our files together with other data. In our case we are going to merge our data with congressional data and census population data as well.

````
{r,warning=FALSE,message=FALSE}
## Creates dataframe of SpatialPolygonData
    houseillowerframe <- as.data.frame(houseillower)
    houseilupperframe <- as.data.frame(houseilupper)
    countyilframe<-as.data.frame(countyil)
```

###Step 7: Read in our csv files

Now lets read in our csv files that have the data on our state congressional members. I retrieved this data from the Illinois statehouse website. I then cleaned up the data a bit before pulling it into R. I retieved this data from: http://www.ilga.gov/

````
{r,warning=FALSE,message=FALSE}
##Reads in CSV
    illinois_senate <- read.csv("C:/Users/Ben/Desktop/Illinois/illinoisstatesenators.csv",
                            stringsAsFactors = FALSE)


    illinois_house <- read.csv("C:/Users/Ben/Desktop/Illinois/illinoisstatehouse.csv",
                           stringsAsFactors = FALSE)

    illinoispop<-read.csv("C:/Users/Ben/Desktop/Illinois/CC-EST2015-ALLDATA-17.csv")

````


### Step 8: Clean up our data and convert some variable names

In this step we are going to clean up our data and rename some of the variables. We need to rename the variable names to the same names as those in our dataframe. Once we do this our datasets will have a common variable name we can now merge our data together with. If there is no 'common' variable name our datasets will not merge properly.

````{r,warning=FALSE,message=FALSE}
    illinoispoptotal<-illinoispop[illinoispop$YEAR==1&illinoispop$AGEGRP==0,]

##Rename variables to match data frame for coercion
    illinois_senate <- rename(illinois_senate, SLDUST = District)

##Rename variables to match data frame for coercion
    illinois_house <- rename(illinois_house,SLDLST = District)

    names(countyil)

    illinoispoptotal<-rename(illinoispoptotal, NAMELSAD = CTYNAME )

    countyil@data<-left_join(countyil@data,illinoispoptotal)

    nrow(countyil)
    ncol(countyil)
    nrow(illinoispoptotal)
````

### Step 9: Combine our data into a new dataframe 

Now we will combine our data into a new dataframe using the cbind() function in R. 


````
{r,warning=FALSE,message=FALSE}
    library(dplyr)


### Can use cbind or left_join to bind the new data to the SpatialPolygonDataFrames
    houseilupper@data <- cbind(houseilupper@data, illinois_senate)

    houseillower@data <- cbind(houseillower@data, illinois_house)
````

### Step 10: Subset by political party

In this step we are going to subset our data by political party affiliation. We will do this using the subset() function. We then create a new object to store the new data in. We will use this new object for creating our popups for our map. 

````

{r,warning=FALSE,message=FALSE}
## Subsets the data to be used in a map and create grouping variables for overlays ####
    housedemocrats<- subset(houseillower, houseillower$Party %in% c("D"))

    houserepublicans <- subset(houseillower, houseillower$Party %in% c("R"))

    senatedemocrats<- subset(houseilupper, houseilupper$Party %in% c("D"))

    senaterepublicans <- subset(houseilupper, houseilupper$Party %in% c("R"))
````


### Step 11: Create popups for our map

Here we are going to create some popups for our map. The 'strong' and 'br' statements are html code and help us create a cleaner looking popup. You can utilize a variety of html code in your maps. The '$' sign is used to designate the variable we want to use from each particular dataframe.

````
{r,warning=FALSE,message=FALSE}
##Creates the popups for the datasets 

    senatedemo_popup <- paste0("<strong>Senator: </strong>", 
                           senatedemocrats$Senator, 
                           "<br><strong>Party: </strong>", 
                           senatedemocrats$Party,
                           "<br><strong>District: </strong>",
                           senatedemocrats$SLDUST)

    senaterepub_popup <- paste0("<strong>Senator: </strong>", 
                            senaterepublicans$Senator, 
                            "<br><strong>Party: </strong>", 
                            senaterepublicans$Party,
                            "<br><strong>District: </strong>",
                            senaterepublicans$SLDUST)



    housedemo_popup <- paste0("<strong>State Representative: </strong>", 
                          housedemocrats$Representative, 
                          "<br><strong>Party: </strong>", 
                          housedemocrats$Party,
                          "<br><strong>District: </strong>",
                          housedemocrats$SLDLST)

houserepub_popup <- paste0("<strong>State Representative: </strong>", 
                           houserepublicans$Representative, 
                           "<br><strong>Party: </strong>", 
                           houserepublicans$Party,
                           "<br><strong>District: </strong>",
                           houserepublicans$SLDLST)


````



### Step 12: Create our map

We will now create our map using the leaflet package in R. We will add different provider tiles to our map, these are available from Open Street Maps amongst others. The provider tiles we use will allow our users to change the map background between a variety of tiles available for leaflet. We will also create our polygons and designate a color for them as well. We will use each political party's respective color in this tutorial to shade our polygons. Lastly, we are going to add a 'layers control'. The layers control will allow us to click our  'provider tiles' on and off and the 'overlay groups' or 'polygons' that we created as well. 

````{r,warning=FALSE,message=FALSE}
##Creates the Interactive Map for publishing on Rpubs 

    leaflet() %>%
      addTiles(group = "OSM (default)") %>%
      addProviderTiles("Stamen.Toner", group = "Toner") %>%
      addProviderTiles("Stamen.TonerLite", group = "Toner Lite") %>%
      addPolygons(data = senatedemocrats,color = "blue",popup = senatedemo_popup,group = "Senate Democrat") %>%
      addPolygons(data = senaterepublicans,color = "red",popup = senaterepub_popup,group = "Senate Republican") %>%
      addPolygons(data = housedemocrats,color = "blue",popup = housedemo_popup,group = "House Democrat") %>%
      addPolygons(data = houserepublicans,color = "red",popup = houserepub_popup,group = "House Republican") %>%
      addLayersControl(
        baseGroups = c("OSM (default)", "Toner", "Toner Lite"),
        overlayGroups = c("Senate Democrat","Senate Republican","House Democrat","House Republican"),
        options = layersControlOptions(collapsed = TRUE)
      ) %>% 
      addLegend("bottomleft",title = "Illinois Congress",colors = c("blue","red"),labels = c("D = Democrat","R = Republican"))
  

````

## Congratulations!!!!!! 

### You have successfully created an interactive map in R Studio you can share with other people. 

