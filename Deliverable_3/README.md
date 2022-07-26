# Food System Emissons

![Background Image](/Katelyn/pexels-tom-fisk-1595104.jpg)

## Table of Contents

* [Overview](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Overview)
* [Data](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Data)
* [Machine Learning Model](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#MachineLearningModel)

## Overview
### Project Topic Description

The focus of our project is on food system greenhouse gas (GHGs) emissions throughout the world. We will be analyzing the data for trends utilizing various data analysis techniques and visualizations to portray our research results. 


### Background: Reason for Selecting Topic

Our team selected the topic of food system emissions due to our mutual interests in the environment and agriculture. The global food system  at every stage of food production throughout the world is energy intensive and contributes to GHG production. We would like to discover the impacts of food production on the production of GHG emissions by looking at our food system's emissions over time, across different countries and regions and other elements. We would also like to predict future emissions using a machine learning model. 

## Data
### Description of Source Data

The data for this project comes from EDGAR-FOOD. EDGAR is a multipurpose, independent, global database of anthropogenic emissions of greenhouse gases and air pollution on Earth. EDGAR provides independent emission estimates compared to what reported by European Member States or by Parties under the United Nations Framework Convention on Climate Change (UNFCCC), using international statistics and a consistent IPCC methodology.

Our data source contains information on Countries and Regions of the world in regards to their GHG emissions. It contains data on whether a country is developing or industrialized, the type of GHG emission, the year corresponding to the GHG emission amount, and the food stage that corresponds with the amount and type of GHG emitted per year. 

Link to Source Data: https://edgar.jrc.ec.europa.eu/edgar_food 

Description Information Source: https://edgar.jrc.ec.europa.eu/

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

## Machine Learning Model

Initially we tried a linear regression model, it worked but had errors when showing accuracy with dividing by zero.

We then moved to Random Forest 2018 model and has no errors predicting developing countries for the RF model and is more accurate than industrial countries. The code is updated to run on any specified year from the data set and a new notebook can run a RF model for all years of the data set.

## Communication Protocols

We created a Google Doc to track our resources and other project related links. This also contains our contact information and information on next steps. We will place all project related items that are not ready for GitHub on this doc if we need to keep track of it. We are communicating through Slack and have shared phone numbers for immediate concerns. We are using Discord to to video meetings outside of class time. A majority of our work together will take place during class time meetings. 

## Links
* [Presentation](https://docs.google.com/presentation/d/1UWW6PTv3gYfUZt2sINpBFY7_NyeHyOu3HGkMoWSyKko/edit#slide=id.gf48cb76871_0_33)
* [Dashboard Planning](https://docs.google.com/presentation/d/13E7F-yIHB91cka32D1X9BRDlvEzHa5vGhuE8NXBjyjw/edit#slide=id.p)
