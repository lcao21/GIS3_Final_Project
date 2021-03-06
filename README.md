# GIS 3 Final Project: Predicting Manhattan Home Sales 🏠
by Lily Cao 

For my GIS 3 final project, I trained a model to predict housing prices in Manhattan, New York. The process included 4 main steps: 1) Cleaning the data; 2) Feature selection; 3) Training the models; and 4) Mapping the predictions. In the first step, beyond just cleaning the data, I created additional independent variables and merged those with the slaes data. In the second step, I used the Boruta method and package to select which of these variables were most important in predicting slae prices. Then, I was able to train 4 different models on the data and figure out which model worked best based on its mean absolute error. Lastly, I mapped the results and created additional figures to help visualize them. 

# **Goals & Objectives** 📌
Though my ultimate goal was to train a model to best predict Manhattan home sales, I also had smaller goals integral to the process. I wanted to include new independent variables not provided by the sales dataset and did so by calculating how many high schools, food vendors, parks, and subway stations were located within a buffer of each home. I also created a fifth independent variable that ranked neighborhood locations based on median incomes. By the end of the project, I will have a) a trained model; b) maps to visualize the predictions; c) prediction results for data on Manhattan home sales. 

The main reason I chose this topic was to better understand how real estate companies like Zillow estimate homes that are not even on the market. These companies and real estate agents likely use a wide array of models to determine their respective predictions, especially since every type of property and locations has its own specifics. Though the final model will be most useful for people who are thinking of putting their houses on the markets, it will also be useful for those who are considering moving to Manhattan and want to find the best valued home. Furthermore, housing prices are an important indicator of the economy. The data I am using is on rolling sales from the last 12 months (April 2019 – March 2020). The coronavirus outbreak will change or is already changing the real estate market and so building a model of data from this timeline will hopefully give insight into housing prices in the midst of this outbreak.

# **Data** 📑
1) NYC Property Rolling Sales: https://www1.nyc.gov/site/finance/taxes/property-rolling-sales-data.page 
    * Titled "manhattan.csv" in the data folder
    * Vars used: NEIGHBORHOOD, BUILDING CLASS CATEGORY, ADDRESS, RESIDENTIAL UNITS, COMMERCIAL UNITS, TOTAL UNITS, LAND       SQUARE FEET, GROSS SQUARE FEET, SALE PRICE
2) NYC School Locations: https://data.cityofnewyork.us/Education/2019-2020-School-Locations/wg9x-4ke6
    * Titled "schools.csv" in the data folder
    * Vars used: Location Category Description, Grades Final Text, Longitude, Latitude
3) NYC Healthy Stores: https://data.cityofnewyork.us/Health/Recognized-Shop-Healthy-Stores/ud4g-9x9z
    * Titled "healthystores.csv" in the data folder
    * Vars used: Borough, Latitude, Longitude
4) NYC Farmers' Markets: https://data.cityofnewyork.us/dataset/DOHMH-Farmers-Markets/8vwk-6iz2
    * Titled "farmersmarkets.csv" in the data folder
    * Vars used: Borough, Latitude, Longitude
5) NYC Parks: https://data.cityofnewyork.us/Recreation/Open-Space-Parks-/g84h-jbjm
    * Read in as geojson file
    * Vars used: Shape Leng, Shape Area, Geometry
6) NYC Subway Stations: https://data.cityofnewyork.us/Transportation/Subway-Stations/arq3-7z49
    * Read in as geojson file
    * Vars used: Geometry
7) NYC Neighborhood Affordability: https://ny.curbed.com/2017/8/4/16099252/new-york-neighborhood-affordability
8) Neighborhood Tabulation Areas (NTA): https://data.cityofnewyork.us/City-Government/Neighborhood-Tabulation-Areas-NTA-/cpf4-rkhq
    * Read in as shapefile
    
I used datasets 2-7 to create new independent variables, in addition to the ones I included from the original rolling sales data. For datasets 2-5, each variable represented the number of schools, food vendors, parks, or subway stations within a 1 mile buffer of each home. I used an article from curbed.com to create a variable that ranks the neighborhood of each home by affordability. So, before feature selection, the independent variables I considered were num_schools,num_parks, num_food, num_subway, neighborhood_ord, RESIDENTIAL.UNITS, COMMERCIAL.UNITS, LAND.SQUARE.FEET, GROSS.SQUARE.FEET.
 
# **Code** 💻
*Append each URL to http://htmlpreview.github.io/? to view without downloading i.e. http://htmlpreview.github.io/?https://github.com/lcao21/GIS3_Final_Project/blob/master/Progress/Part1.html*

1) Data Cleaning and Wrangling: https://github.com/lcao21/GIS3_Final_Project/blob/master/Progress/Part1.html
   * Cleaned the dataset on property rolling sales including filtering for homes located in Manhattan and geocoding addresses
   * Used datasets 2-7 to create 5 new independent variables to merge with the home sales dataframe: num_schools, num_food, num_parks, num_subway, neighborhood_ord
2) Feature Selection: https://github.com/lcao21/GIS3_Final_Project/blob/master/Progress/Part2.html
   * Used Boruta to find the most important features in predicting sale price
   * Of the 12 independent variables I chose, 7 were deemed important: num_food, num_subway, num_parks, num_schools, neighborhood_ord, RESIDENTIAL.UNITS, LAND.SQUARE.FEET
3) Model Training: https://github.com/lcao21/GIS3_Final_Project/blob/master/Progress/Part3.html
   * Normalized data and split it into training (70%) and testing (30%) sets
   * Trained 4 different models: OLS, Poisson, Random Forest, GBM (Generalized Boosted Machine)
   * Ultimately picked GBM since it had the smallest MAE (mean absolute error)
4) Results: https://github.com/lcao21/GIS3_Final_Project/blob/master/Progress/Part4.html
   * Created maps to visualize predictions vs actual sale prices 
   
# **Figures** 🗺
These are just a few of the visualizations I created:

*Left to right: Map of Manhattan homes by sale price; map of intersections between homes and high schools; map of intersections between homes and food vendors*    
<p float="left">
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/home_sales.png" width="270" />
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/homes_schools_int.png" width="245" /> 
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/homes_food_int.png" width="240" />
</p>

*Boruta rankings of features by importance*  
<img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/Boruta.png" width="400">

*Correlation plot of 7 features deemed important*   
<img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/corr_plot.png" width="400">

*Trained models by MAE value*    
<img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/model_maes.png" width="400">

*Left to right: Map of homes by num_schools; map of homes by num_parks; map of homes by num_food*    
<p float="left">
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/num_schools.png" width="250" />
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/num_parks.png" width="250" /> 
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/num_food.png" width="250" />
</p>

*Left to right: Map of homes by num_subway; map of homes by RESIDENTIAL.UNITS; map of homes by LAND.SQUARE.FEET*    
<p float="left">
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/num_sub.png" width="250" />
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/res_units.png" width="250" /> 
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/land_sq.png" width="250" />
</p>

*Interactive map of homes by predicted vs actual sale prices*  
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/pred_v_actual.png" width="400" />

*Map of homes by difference in predicted and actual sale prices*  
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/abs_diff.png" width="400" /> 

*Interactive map of neighborhoods by average MAE*  
  <img src="https://github.com/lcao21/GIS3_Final_Project/blob/master/Figures/neigh_mae.png" width="400" /> 

# **Future Work**❓
In the future, I want to test this model on other boroughs and in turn, train new models more appropriate for each borough. Furthermore, I trained this model only on Manhattan home sales data from the past year and so another future goal would be to expand the time period of the data. For instance, incorporating data from the 2007-2008 recession would likely have a big impact on the final model. Lastly, I want to include more independent variables, as there are many more factors that go into determining sale price, namely the economy. There are also qualitative factors like aesthetics that would be interesting to quantify and incorporate.
