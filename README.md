<h1 align="center">Exploring the Los Angeles Airbnb Market:</h1>
<h2 align="center">Unveiling Insights for Prospective Hosts</h2>

### Goal
- Primary goal was to understand the factors that significantly influenced rental prices in different neighborhoods with the use of Python / Pandas and data visualization. 

### Outcome
Based on the analysis of rental prices in different neighborhoods, the following were derived:

- **Neighborhood plays a significant role**: The location of the listing is a key factor influencing rental prices in Los Angeles. Different neighborhoods have distinct price dynamics, with some commanding higher prices than others. The more popular a neighborhood the likelier price will come down rather than neighborhoods in less competitive areas. Hosts should consider the desirability and amenities of a neighborhood when determining their rental pricing strategy.

- **Property attributes matter**: The number of bedrooms, bathrooms, and beds in a listing has a significant impact on rental prices. Listings with more bedrooms and bathrooms tend to command higher prices, indicating the importance of space and accommodation capacity for potential guests. Based on a Multiple Linear Regression model, a host might expect an increment of around $46 an additional bedroom or an entire home/apt.

- **Amenities can drive prices**: The presence of basic or essential amenities in a listing, such as a dishwasher, tv, or washer, can positively influence rental prices. Hosts should highlight these amenities in their listings to attract guests and potentially justify higher prices. As an example, using the same modeling, hosts are able to increase their prices by around $21 just by offering a dishwasher.

![](https://i.postimg.cc/qvg95Qxy/Summary-Trends1.png)
![](https://i.postimg.cc/RZ8j5fg8/Summary-Trends2.png)

### Objective
- The project aimed to showcase data analysis skills using Python/Pandas and statistical modeling to address influential markers for price in AirBnB rentals.
- Skills leverages: data cleaning & transforming, exploratory data analysis, modeling, evaluation

---

### Data Exploration and Cleaning
- One dataset was leveraged (listings.csv) which included roughly 42K unique listing id's and 75 features. 
- Among the functions and strategy used to review the dataset included:  
    - *.info(), .shape, .head, .tails, .duplicated(), .describe(), .nunique(), .isnull(), string functions, .astype() and masking to derive initial observations and transform, fill any necessary data.*

![](https://i.postimg.cc/8CMX2YJJ/data-exploration.png)
- *using .describe() to view frequency, mean, min, max, standard deviation*

### Exploratory Data Analysis
- To refine the number of variables and understand which have the strongest influence in price various functions and visualizations were used including:  
    - *correlation heatmaps, boxplots, bar graphs, regression plots, scatterplots, line graphs, and VIF values to check for high multicollinearity between variables.*
    
- From this analysis the following variables were considered among the strongest influencers agaisnt price, though are  considered weak compared to the first few in this list: 
    - *'bedrooms', 'beds', 'Entire Home/Apt', 'bathrooms','avg_price_per_neighborhood', 'amenity_count', 'dishwasher_flag','tv_flag', 'oven_flag', 'washer_flag'* 

- Correlation heatmaps helped focus key variables, but by including additional features derived from the dataset (i.e. avg_price_per_neighborhood, amenity_count, essential amenities, listings by room type), key representation of the data was not lost. As an example, within the dataset there were over 7,000 unique amenity offers. To consider some representation of that data without one hot encoding due to the risk of high dimensionality, the total number of amenities per listings was used instead. 

- Bar graphs helped affirm the relationship between price and varied neighborhoods. The more popular a neighborhood by number of listings (i.e. Sherman Oaks, Long Beach etc.) the more competitive the area and the lower the price will trend. That also words vice versa, neighborhoods like Malibu that only had 114 listings in the data set holds the second highest average price at \\$312 vs. a neighborhood like Sherman Oaks with over 2K listings and an average of \\$111.06.

- Using scatterplots, regression plots (regplot) and VIF values also solidified not just the relationship between price and their respective independent variable but whether these variables had any high multicollinearity among other variables. The risk of high multicollinearity would have lowered modeling performance if not evaluated during EDA. 

![](https://i.postimg.cc/JntKQ4VL/refined-corr-matrix.png)
- *Ability to visualize clusters of variables highly correlated to each other, indication there might be high multicollinearity with several variables.*

![](https://i.postimg.cc/hGD2f12h/corr-matrix-reviews.png)
- *Another view but zoomed into just the variables related to reviews*

![](https://i.postimg.cc/XvsQFBPL/corr-vector.png)
- *Narrowing scope of variables to see how price compares to each. Before considering essential amenities.*

![](https://i.postimg.cc/50GgKdbF/neighborhoods-and-price.png)
- *Viewing average price by different neighborhood associations. The first shows top neighborhoods by average price while the second lists the most popular neighborhoods (listing total) but shows their respective average price for comparison.*

![](https://i.postimg.cc/YCwnwHg6/price-boxplot.png)
- *Viewing the distribution of listings by price and capturing if any outliers exist.*

![](https://i.postimg.cc/DwdCvMdt/price-bargraph.png)
- *Showing a better representation of outliers for price and what percentage of the data each represent.*

![](https://i.postimg.cc/0jnQ2xjz/amenity-flag-line.png)
- *To consider additional variables, select amenities (considered essential by the following [Redfin article](https://www.redfin.com/blog/apartment-amenities/), were evaluated.*

---

### Modeling and Evaluation
- Given that the question being addressed is what key factors influence price, the outcome variable was straightforward. It is a continous dependent variable with all independent variables in consideration of numerical value as well. That made running a multiple linear regression model the most approach. 
    - Multiple Linear Regression modeling is not too complex, and is considered an explainable model scheme that best fits this type of analysis. Though there is a consideration to be made in using machine learning models like Random Forests to help improve performance with the risk of incrementing complexity. 
    
- The final dataset being used for modeling contained around 37K listings after data cleaning and processing. Outliers for several variables were kept into the data to maintain the size of the set, but were evaluated individually to make sure they were valid outliers. 

- The strategy involved splitting the data for training and testing against all 37K listings. The model was evaluated against all 4 linear regression assumptions and once a score was obtained, that modeling would be applied onto some of the most popular neighborhoods as subsets. Within those subsets all data for a given neighborhood was used to train and test the model due to the drastic drop of data available (ex: Sherman Oaks has 2K listings, while the total set contains 37K). 
    - By evaluating the performance of this modeling at the neighborhood level, a better understanding of these key factors against price could be derived. 
    - A neighborhood like Sherman Oaks showed that modeling of the key variables like bedrooms, beds, and bathrooms explained around 72\% of the variance on price while a neighborhood like Santa Monica was not as significant at an R-squared of 22\%.
    
![](https://i.postimg.cc/qMBqDtDy/MLR-building.png)
- *Building the Multiple Linear Regressio Model without the essential amenities (first model)*.

![](https://i.postimg.cc/65H3k9FS/MLR-assumptions.png)
- *Visualization of the assumptions being met with this modeling*.

![](https://i.postimg.cc/9XYzBPbc/validation-MLR.png)
- *A view of the actual price values vs. the predicted values. With price outliers removed (listings with price > \\$481.5) it would make sense to see the predictions of listings at higher values drop as the graph shows*.

---

### Next Steps
- Some options to consider for further investigation:
1. **Neighborhood research**: Investigate the specific neighborhoods that command higher rental prices in Los Angeles. This research can help listing owners understand the market dynamics and make informed decisions about targeting specific neighborhoods for their listings. An option to review the data on reviews.csv might form more insights on customer sentiment based on neighborhood and amenities offered.

2. **Price fluctuations based on Time of Year**: Consider the busiest months or season per listing as a factor for price variance. Monitoring prices based on time of year or times in the year which are busiest overall (be it season, local events etc.) may have more a significant influence on price. It's far more difficult to move a property from one neighborhood to another, than it is adjusting price based on the demand in a given time of year.

3. **Highlight amenities**: Target amenities that go beyond essential necessities. Having a pool, children's dishware, or even shampoo may be influential amenities not considered necessities that have more impact in price variance. 

4. **Try different modeling**: Although Multiple Linear Regression offered a more simplied and explainable regression, using machine learning options such as Random Forest might offer better performance and a more tuned set of important features. 

#### Credit
- Data comes from [Inside AirBnB](http://insideairbnb.com/get-the-data/). Public data sourced from AirBnB.
