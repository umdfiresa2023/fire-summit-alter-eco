# Team Name’s FIRE Summit Presentation
Team Members

## Research Question

Write research question here.

(Optional) Insert an image if it helps motivate the research question.

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
1+1
```

    [1] 2

