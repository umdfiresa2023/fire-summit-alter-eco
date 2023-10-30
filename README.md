# Team Name’s FIRE Summit Presentation
Kat, Defne, Padmini, and William 

## Research Question

How do the marginal damages associated with electric vehicles compare to those of gasoline vehicles in the United States?


## Background Project

### Objective: 
<img align="right" width="300" height="200" src="https://github.com/umdfiresa2023/fire-summit-alter-eco/assets/28952036/b4bdd171-9f79-4bba-b042-695910184a6c">


Replicate the 2016 paper
_“Are There Environmental Benefits from Driving Electric Vehicles? The Importance of Local Factors”_ by _Holland et al. (2016)_ 
on the environmental benefits of electric vehicles (EVs) versus gas vehicles using updated data from 2019-2021

### Findings from the original study:

+ The marginal damages of EVs depend on which fuel source is being used to generate electricity
+ In metropolitan areas, gas vehicles have higher marginal damages
    
We limit the marginal damages calculations based only on **NOx** and **SO2** emissions only

## Key Terms
<img align="right" width="397" alt="Map of electricity interconnections" src="https://github.com/umdfiresa2023/fire-summit-alter-eco/assets/28952036/8eb8b12d-14c1-41fd-bf79-f1a3b2de54ad">

### Marginal Damages

The incremental negative effects on the environment are caused by an additional unit of pollution. In our case, it would be the damage in _$/mile_ of using an EV or a gas vehicle

### Interconnections 

+ The United States electrical grid consists of **3** main interconnections; **Eastern, Western, and Texas**
+ Each interconnection pulls its electricity from the grid and distributes it to each area within the interconnection

## The APX Model

The APX Model is the _Air Pollution Emission Experiments & Policy Analysis_ model. It was developed by Nicolas Muller, who is a professor at Carnegie Mellon University. The model takes emissions from every source of pollution, such as agriculture, roads, and power plants as input. Through several algorithms and modeling, it produces the marginal damages for each source of pollution in dollars per ton. 

## What are we doing now?

Before we are able to replicate the 2016 paper, we must ensure that our code processes raw data from the _National Emissions Inventory_ before it’s used in the AP3 model. The current code to process the data is outdated and difficult to follow, so we are rewriting and updating it. Our updated code should process the raw data in the same way, so we must replicate the results from past years _(2008-2014)_ before we can ensure its accuracy for current use. 


``` r
library("tidyverse")
library("data.table")
install.packages("arrow")
library(arrow)

emissions <- list()
emissionsTemp <- list()

filenames <- c( "G:/Shared drives/2023 FIRE-SA/FALL OUTPUT/Team Alter Eco/Emissions Data/Nonroad/2008/2008neiv3_nonroad_byregions/2008NEIv3_nonroad123.csv", 
                "G:/Shared drives/2023 FIRE-SA/FALL OUTPUT/Team Alter Eco/Emissions Data/Nonroad/2008/2008neiv3_nonroad_byregions/2008NEIv3_nonroad4.csv", 
                "G:/Shared drives/2023 FIRE-SA/FALL OUTPUT/Team Alter Eco/Emissions Data/Nonroad/2008/2008neiv3_nonroad_byregions/2008NEIv3_nonroad5.csv", 
                "G:/Shared drives/2023 FIRE-SA/FALL OUTPUT/Team Alter Eco/Emissions Data/Nonroad/2008/2008neiv3_nonroad_byregions/2008NEIv3_nonroad67.csv", 
                "G:/Shared drives/2023 FIRE-SA/FALL OUTPUT/Team Alter Eco/Emissions Data/Nonroad/2008/2008neiv3_nonroad_byregions/2008NEIv3_nonroad8910.csv")
#filenames <- c("2008NEIv3_nonroad123", "2008NEIv3_nonroad4", "2008NEIv3_nonroad5", "2008NEIv3_nonroad67", "2008NEIv3_nonroad8910")
pollutants<-c("Sulfur Dioxide", "Nitrogen Oxides", "PM2.5 Primary (Filt + Cond)", "Volatile Organic Compounds", "Ammonia")

# counter to determine if current file is the first file 
counter <- 0
# looping through each file in 2008 nonroad 
for(i in filenames){
  # reads file at index i and stores in nonroad 
  nonroad <- arrow::read_csv_arrow(i) 
  
  print(colnames(nonroad))
  # stores nonroad in emissionsTemp list 
  emissionsTemp <- nonroad
  # cleans emissionsTemp and stores into emissions df 
  emissions.df<-emissionsTemp %>%
    # filter description column
    filter(description %in% pollutants) %>%
  mutate(total_emissions=as.numeric(total_emissions)) %>%
  mutate(state_and_county_fips_code=as.numeric(state_and_county_fips_code)) 
  
  if (counter == 0){ # if first file
    emissions[[1]] <- emissions.df
  } else { # for all other files
    emissions[[1]] <- rbind(emissions[[1]], emissions.df)
  }
  # increments so all other files handled by else 
  counter <- counter + 1
}

```


