# Food System Emissons

![pexels-tom-fisk-1595104](https://user-images.githubusercontent.com/99369565/182712311-863f6afc-36a7-4bc8-ad13-d51008e855bf.jpg)

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

Questions we hope to answer with the data to predict classification of Industrial or Developing countries:

- Is there a clear distinction between industrial and developing countries based on GHG emissions per year?
- Is one group contributing distinctly more GHG emissions?
- Are developing countries at a disadvantage for GHG emissions production or is there no distinction between the types of countries?
- Can the RFC accurately select industrial or developing countries using the specific features we set it to train on?  

### Data Exploration

We wanted our data to meet the following criteria:
- credible
- medium - large size
- show history over time and use

After finding the right data set to use, we had discussions on what questions we wanted and could be answered. Next we found what data needed to be cleaned, dropped and what was missing.

One of the first things we noticed we needed to change was switch year from a row to a column.

![image](https://user-images.githubusercontent.com/99369565/181135147-ada52a89-f5da-4782-9f82-decfac928719.png)

We also dropped all rows that contained a 0 in a year, and the countries listed "Int. Aviation" and "Int. Shipping", which helped our accuracy score go up.

![image](https://user-images.githubusercontent.com/99369565/181382880-24b93013-d605-44d6-b4df-8c34101bc73a.png)


### Data Analysis
Once the data exploration phase was complete we setout to clean the data and narrow our questions down.

We cleaned the data using Jupyter Notebook and the following libaries:
- pandas as pd to process data in a tabular format
- numpy as np for linear algebra

Preliminary data analysis included identifying features that distinguish developing from industrial countries and types of GHGs produced along with food system stages within each country.

Preparing the data for the Machine Learning Model included: 
- Removing redundant columns from data such as country code.
- Removing International Aviation and International Shipping GHG emissions data.
- Removing country grouping, this initially seemed redundant to include country names and group.
- Encode each column using LabelEncoder to fit transform names to unique values for the Machine Learning Model.
- Adjust the dataset to contain only columns used by machine learning model

To prepare for the Machine Learning Model we split, scaled, and fit the data accordingly:
- Split the working data frame into features and target values.
- Split the working data frame into a training and testing dataset.
- Scale and fit the data for consistency along the distribution of data points for the RandomForestClassifier.

We used .replace to clean and update country names.

![image](https://user-images.githubusercontent.com/99369565/182044586-b35258a9-b95b-4127-89fa-88f24ca40949.png)

#### Cleaned Data with Region Grouping and All Years DF

![image](https://user-images.githubusercontent.com/99369565/181916972-32ff820d-7d46-4455-b879-93ac3b94f9dc.png)

#### Cleaned Data with Country and All Years

![image](https://user-images.githubusercontent.com/99369565/181917176-aa36ec20-0f4a-4ae6-a08a-31c26d83676c.png)

The initial step required connecting the Jupyter Notebook to the SQL server that was hosted on AWS. The SQL database housed a verity of tables created with data sorted uniquely between tables. The table selected for the RFC had null values removed, which represented a small portion of the dataset, mostly from early years within the data set. This clean table allowed for a solid data set to begin working with.

### Machine Learning Model 

Understading what questions we wanted to answer lead us to creating a machine learning model using Random Forest Classification to predict whether a country was industrial or developing based on equal features. Narrowing down on this classification would improve understanding of the production of GHG emissions. The target for the ML RFC is to distinguish countries from each other.

Initially we tried a linear regression model, it worked but had errors when showing accuracy with dividing by zero. We then moved to Random Forest 2018 model and had no errors predicting developing countries for the RF model and is more accurate than industrial countries.

We found that the advantages for using a RFC model are:
-	Well suited for classification tasks.
-	Many individual decision trees prevents overfitting.
-	Trees are trained on different pieces of the data that operate as an ensemble.
-	Effective for processing many input variables when working with large datasets.

The limitations we found for the RFC model are:
-	Can require a significant amount computational resources to process the data.
-	Can be time consuming for large data sets to train multiple trees.
-	RFC can’t extrapolate, it can only make a prediction that are based previous observations.

Our target for the ML model was set early on. Our first RFC model was specifically designed to look at one year of data (2018), the latest data available. Then the code was modified to look at any year in the data set 1990 – 2018. Our latest RFC model considers all the years available.

The target was defined as 0 for Developing and 1 for Industrial.  The data frame for training the RFC model included the 4 types of GHG tracked in our data set along with stage of food system that corresponds to that specific GHG.  To further help identify the target, the name of the country was also provided with the twentyeight years of tracked data.

The rest of the data was split using the standard 75% training 25% testing ratio, this benchmark is common and allows for training without overfitting, while leaving a robust data set for training. The next step applied the StandardScaler to the training data set and fit the data, then the RFC was created via RandomForestClassifier() using two parameters:
- The number of trees created by the algorithm (n_estimators=500).
  -	N_estimators = the number of trees to be built before taking the maximum voting or averages of predictions.  The higher generally better accuracy but more CPU resources required.
- A random_state=1.
  -	random_state= set to check and validate the data when running the code multiple times, a fixed value will assure that the same sequence of random numbers is generated each time the code is run.

**Splitting the preprocessed data:**

![image](https://user-images.githubusercontent.com/99369565/181919741-43b49d85-106b-4607-98b0-bbd2f4db4420.png)

With the RFC built, the model was fit with the trained and scaled data allowing for predictions. After making predictions on the scaled testing data analysis was made on the Accuracy, Precision, Recall, and F1-Scores.

When our initial model analyzed specifically 2018, we had an overall accuracy score within a tenth compared to looking at all years (79% vs 78%). This was a similar trend observed running the model for various individual years in the data set (1995 Below). We typically observe the model able to predict developing countries near 80% accuracy with industrial countries near 70%. A quick summary of these scores tells us that industrial countries don’t have many unique features within the group to help the model identify them with the data provided.

Further analysis could include additional futures such as population to help the model. A keynote to consider, when the model was tweaked to account for country grouping the RFC accuracy jumped to suspicious 98%. When the datasets country grouping was visualized, we see clear geographic boundaries and good reason why the accuracy jumps. Coupling the country grouping with the other features clearly boost the model’s accuracy. For example, if a country is within the Central Europe group it is 100% industrial. For our model without country grouping, country name was much more important than the model with country grouping. Finding those correlations was helpful to understand importance of different features and help model future work.

#### 1995 Classification Report:</u>

![image](https://user-images.githubusercontent.com/99369565/181919355-f0e4eb9d-052d-4eae-b9e7-b5beb42170c0.png)

#### 2018 Classification Report:

![image](https://user-images.githubusercontent.com/99369565/181919350-4ea403da-93ab-4674-ba8f-5cf357426cf7.png)

#### All Years with Country Grouping Classification Report:

![image](https://user-images.githubusercontent.com/99369565/181919361-934314d5-0225-4655-b9a0-a3f931379b06.png)

#### All Years without Country Grouping Classification Report:

![image](https://user-images.githubusercontent.com/99369565/181919363-fab74990-4b30-4970-ac65-404928b199fb.png)


### Database

We used Postgres SQL on Amazon AWS due to its useability and convenience.

<img width="668" alt="Updated_erd" src="https://user-images.githubusercontent.com/99369565/182042866-e3a6c60d-0e34-4988-8463-4367d0d2a27e.png">

We joined country from edgar_food_switched database with country_name from country_def database.

<img width="591" alt="Join" src="https://user-images.githubusercontent.com/99369565/182042933-5529ab0d-efb3-4455-992b-f5ae48621b1b.png">

<img width="837" alt="Table_join" src="https://user-images.githubusercontent.com/99369565/182042887-ab3efbf1-efe8-4bf6-bf6d-c4e799dc6dae.png">

### Dashboard

We built our dashboard on Tableau and included a heat map, graphs, and images to represent the data we analyzed. The heatmap is interactive by hovering over each country and updates on command by changing the filters. 

![Food System Greenhouse Gas Emissions (1)](https://user-images.githubusercontent.com/99369565/182269417-07b6f411-583f-4409-ab14-49ab2f1c77b7.png)


## Links
* [Presentation](https://docs.google.com/presentation/d/1UWW6PTv3gYfUZt2sINpBFY7_NyeHyOu3HGkMoWSyKko/edit#slide=id.gf48cb76871_0_33)
* [Dashboard](https://public.tableau.com/app/profile/katelyn.underbrink/viz/FoodSystemEmissions/FoodSystemGreenhouseGasEmissions?publish=yes)
* [Source Data](https://edgar.jrc.ec.europa.eu/edgar_food)


[Jump to top](https://github.com/AndyPicton/Food_System_Emissions/blob/main/README.md#Table-of-Contents)
