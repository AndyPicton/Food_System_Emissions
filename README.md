# Food System Emissons

![Background Image](/Katelyn/pexels-tom-fisk-1595104.jpg)

## Table of Contents

* [Overview](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Overview)
* [Data](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Data)
* [Machine Learning Model](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Machine-Learning-Model)
* [Database](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Database)
* [Dashboard](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Dashboard)
* [Links](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Links)

## Overview
### Project Topic Description

The focus of our project is on food system greenhouse gas (GHGs) emissions throughout the world. We will be analyzing the data for trends utilizing various data analysis techniques and visualizations to portray our research results. 


### Background

Our team selected the topic of food system emissions due to our mutual interests in the environment and agriculture. The global food system  at every stage of food production throughout the world is energy intensive and contributes to GHG production. We would like to discover the impacts of food production on the production of GHG emissions by looking at our food system's emissions over time, across different countries and regions and other elements. We would also like to predict future emissions using a machine learning model. 

## Data
### Description of Source Data

The data for this project comes from EDGAR-FOOD. EDGAR is a multipurpose, independent, global database of anthropogenic emissions of greenhouse gases and air pollution on Earth. EDGAR provides independent emission estimates compared to what reported by European Member States or by Parties under the United Nations Framework Convention on Climate Change (UNFCCC), using international statistics and a consistent IPCC methodology.

Our data source contains information on Countries and Regions of the world in regards to their GHG emissions. It contains data on whether a country is developing or industrialized, the type of GHG emission, the year corresponding to the GHG emission amount, and the food stage that corresponds with the amount and type of GHG emitted per year. 

![image](https://user-images.githubusercontent.com/99369565/181123155-23d0b4c3-c8f3-443f-a9b3-fe04e81a2b5f.png)

### Research Questions

Questions we hope to answer with the data include the following:

- “How is the world’s food system contributing to Greenhouse Gas emissions?”
- "Over time, how has the world’s food system greenhouse gas emissions changed?”
- “Is our food system becoming more GHG emission intensive?”

#### Question for Random Forest:

Predicting classification of Industrial or Developing countries based on:
- Substance ( types of GHG - 4 types )
- Food system stage ( production, packaging, … )
- Country name ( found it helped accuracy )

### Data Exploration

We wanted our data to meet the following criteria:
- credible
- medium - large size
- show history over time and use

After finding the right data set to use, we had discussions on what questions we wanted and could be answered. Next we found what data needed to be cleaned and dropped and what data was missing.

One of the first things we noticed we needed to change was switch year from a row to a column.

![image](https://user-images.githubusercontent.com/99369565/181135147-ada52a89-f5da-4782-9f82-decfac928719.png)

We also dropped all rows that contained a 0 in a year, and the countries listed "Int. Aviation" and "Int. Shipping", which helped our accuracy score go up.

![image](https://user-images.githubusercontent.com/99369565/181382880-24b93013-d605-44d6-b4df-8c34101bc73a.png)


### Data Analysis
Once the data exploration phase was complete we setout to clean the data and narrow our questions down.

We cleaned the data using Jupyter Notebook and the following libaries:
- pandas as pd to process data in a tabular format
- numpy as np for linear algebra

We converted all data to be an integer so each country, substance, and food system stage has its own number as well as updating dev_country to be 1 for developing and 0 for industrialized.  We tested the models with different variables (substance, food system stage, year, country, country class, and region) and found that region had a huge impact on raising our accuracy score. With Tableau, we were able to visualize why region had such a big impact and found that if a group of countries close to eachother were all developed then they would be grouped together and the same goes with industrialized countries. Our model learned that when we tested to predict if a coutry is D or I, the accuracy score was 98% as seen in picture below.

#### Cleaned Data with Region Grouping and All Years DF

![image](https://user-images.githubusercontent.com/99369565/181916972-32ff820d-7d46-4455-b879-93ac3b94f9dc.png)

#### Random Forest Classification Report with Region for All Years

![image](https://user-images.githubusercontent.com/99369565/181916832-b0468894-98dd-4f1c-9159-0e5aadba656e.png)

#### Cleaned Data

![image](https://user-images.githubusercontent.com/99369565/181137223-9ce728ff-0e4b-4de8-b73c-67912c20017e.png)

### Machine Learning Model

Initially we tried a linear regression model, it worked but had errors when showing accuracy with dividing by zero.

We then moved to Random Forest 2018 model and had no errors predicting developing countries for the RF model and is more accurate than industrial countries. The code is updated to run on any specified year from the data set and a new notebook can run a RF model for all years of the data set.

We first setup two different machine learning models to test on one year at a time and also all years with and then without grouping. We decided to move forward with the model that does not include region.

Accuracy score and classification report for data on one year (1995): 

![image](https://user-images.githubusercontent.com/99369565/181862511-bf51cf62-f2f8-435c-9412-8a5a974e9215.png)

Accuracy score and classification report for data on all years without grouping: 

![image](https://user-images.githubusercontent.com/99369565/181862520-3ec63cee-3358-435a-973e-1785333af2a6.png)

### Database

We used Postgres SQL on Amazon AWS due to its useability and convenience.

![image](https://user-images.githubusercontent.com/99369565/181124075-2684d956-9351-42f5-8a72-37e5288ac120.png)

We joined country from edgar_food_switched database with country_name from country_def database.

![image](https://user-images.githubusercontent.com/99369565/181133898-da7dc05c-a0e9-4598-916b-5346ab89d9c5.png)



### Dashboard

We built our dashboard on Tableau and included a heat map, graphs, and images to represent the data we analyzed. The heatmap is interactive by hovering over each country and updates on command by changing the filters. 

## Communication Protocols

We created a Google Doc to track our resources and other project related links. This also contains our contact information and information on next steps. We will place all project related items that are not ready for GitHub on this doc if we need to keep track of it. We are communicating through Slack and have shared phone numbers for immediate concerns. We are using Discord to to video meetings outside of class time. A majority of our work together will take place during class time meetings. 

## Links
* [Presentation](https://docs.google.com/presentation/d/1UWW6PTv3gYfUZt2sINpBFY7_NyeHyOu3HGkMoWSyKko/edit#slide=id.gf48cb76871_0_33)
* [Dashboard](https://public.tableau.com/app/profile/katelyn.underbrink/viz/FoodSystemEmissions/FoodSystemGreenhouseGasEmissions?publish=yes)
* [Source Data](https://edgar.jrc.ec.europa.eu/edgar_food)


[Jump to top](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Table-of-Contents)
