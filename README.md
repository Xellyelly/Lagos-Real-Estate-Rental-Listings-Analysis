# Web-Scraping-Real-Estate-Listings-for-Rent-Analysis-in-Lagos-ANOVA-Regression-Insights
![download](https://github.com/user-attachments/assets/eb716673-457a-4589-ade7-bf4290bdcf16)

## Project Description
Finding the perfect rental home in Lagos can be overwhelming. With so many neighborhoods to choose from and varying prices that seem hard to explain, many renters struggle to understand what really drives rental costs.
This project tackles that problem by collecting rental listings directly from popular real estate websites[ONG ](https://ong.ng/c_real-estate?query=lagos) through web scraping. Gathered data on key factors like location, number of bedrooms, and house type.
**Our goal is to analyze this data to answer important questions:**
- How much does location affect rent prices?
- How much does adding an extra bedroom increase rent?
- Are duplexes generally more expensive than apartments, or is it more about size and rooms?
- By transforming scattered online listings into a clear, data-driven story, this project helps renters, landlords, and investors make better decisions in Lagos’s complex housing market.
In a city where hunting for a good rental can feel like searching for a needle in a haystack, having solid insights can save time, money, and stress.

##  Web Scraping
Data was scrapped from
[ONG ](https://ong.ng/c_real-estate?query=lagos)
![Screenshot 2025-07-05 175010](https://github.com/user-attachments/assets/d7342cbf-120d-4587-b26c-4cdd50112a48)

**Identified Features for**
- Price : This is the listed rental price of a property(in Naira)
- Period : Indicates whether the rent is charged annually, monthly or quarterly
- Description : text field containing extra details about the property
- Location : Specifies where the property is located
  
**Few more feature were extracted from Description columns for the pupose of this analysis
  used keyword search and pattern matching**
- Bedrooms : Number of bedrooms in each property
- purpose : Refers to why the property is listed (For Rent or For Sale)
- type : Describes the kind of property, such as Apartment, Duplex, or Others.

**Data manipulation & Cleaning**
  - Converted all prices to  yearly rent using the Period feature
  - Handled missing values by removing rows with missing or invalid prices,locations
    and filling missisng period
  - Filtered for precise location from location feature
  ## Exploratory Data Analysis (EDA)
  Plot price distributions
  ![image](https://github.com/user-attachments/assets/8048481d-862f-467a-85f7-a376963d553e)
The distribution of rental prices is positively skewed,
meaning most houses are moderately priced,
but a few luxury properties with very high prices are pulling the mean to the right.
This skewness suggests that the average price may not reflect typical rent,
so using the median or applying a log transformation gives a better picture for analysis.
![image](https://github.com/user-attachments/assets/57dd35a0-9724-4c57-878d-34528bedeea5)
Most values sit between 14 and 18 on the log scale. That converts to roughly ₦1.2 M – ₦6.6 M per year and 
slim tail extends beyond log ≈ 19–21 (₦65M+)These luxury outliers widen your confidence interval
- **Boxplot Insight: Log of Yearly Rent by Location** 
![image](https://github.com/user-attachments/assets/241f914c-03a5-4a7a-9ddf-63de89d2eaf4)

- Ikoyi and Victoria Island have the highest rent ranges, ideal for premium budgets, median is higher indicating more luxury properties.
- Ajah, Ikeja, and Magodo have moderate median rents with less spread, indicating more consistent pricing.
- Areas like Ojodu, Ibeju, Surulere, and Isolo are better suited  moderate budgets, with tighter boxes, suggesting fewer premium properties.
- Outliers in many locations confirm the earlier observation of positive skewness, caused by luxury listings.
**This chart can helps in identifying  where to rent in Lagos based on budget**

## Statistical Testing
**Hypotheses: Does Location Affect Yearly Rent Price?**
```
-- Null hypothesis ( H_0 ):
Mean yearly rent is the same across all locations.
$H_0: 
  \mu_1 = \mu_2 = \mu_3 = \dots = \mu_20
  $
-- Alternative hypothesis ( H_1 ):
At least one location has a different mean yearly price.
```
Kruskal-Wallis model

![image](https://github.com/user-attachments/assets/27dfaec9-456b-46cf-bfe5-b3835d8cc2ee)

To ensure fairness, We'll use the smallest listing count among the three as the subset size
Sampling equally from each location ,Combine and shuffle the data
This balanced dataset will be used to train the model and avoid bias from uneven group sizes.
![image](https://github.com/user-attachments/assets/2008133d-02cb-4503-97bb-8b37c21b6b7f)
## Observation
significance level is 0.05 for this tests 
Since your p-value = 0.0000 is less than 0.05, the result is statistically significant,
This means  null hypothesis is rejected that all locations have the same median yearly price,implying that there
is different in mean yearly price 
## Visualization 

![image](https://github.com/user-attachments/assets/e32c2a58-f08e-4259-96a6-7fba091d923f)
- The median is different accross each box plot
-  Victoria island distibution is clearly different from lekki and ikoyi,
  it has highly priced houdes , showing as outlier indicating luxuries compare to other top locations

**Does bedroom number Affect Yearly Rent Price, if yes by what % rent increase per bedroom**
### Build OLS model:
- Dependent: log_price
- Predictors: Location, Bedroom
- 
![image](https://github.com/user-attachments/assets/72d2d72a-33d5-4b2e-9f4f-d14c39c0d2c4)
## Observation
- The analysis shows that both location and number of bedrooms significantly affect the yearly rent prices.
- Each additional bedroom increases the yearly rent price by by ~52% (exp(0.417) ≈ 1.52) approximately (1.3m)
- The model (location + bedrooms) explains 53.4% of the total variation in log-prices and Residual variation (46.6% ) are unexplained
  - **Heatmap of Yearlyrent across differeent location and number of bedroom**
  ![image](https://github.com/user-attachments/assets/9b279089-9f59-4f80-a315-59a416708988)
  
**Hypotheses: check if Duplex Price is Greater Than Apartment for listed house for rent**
~~~
-- Null hypothesis ( H_0 ):
$H_0: \mu_duplex \leq \mu_apartment$
-- Alternative hypothesis ( H_1 ):
Duplex mean yearly price is greater than apartment mean yearly price.
 $H_1: $\mu_duplex > \mu_apartment$.
 ~~~


**Two-sample t-test comparing just two groups Duplex vs. Apartment**

![image](https://github.com/user-attachments/assets/fbdca685-1f58-4846-8a62-bc09189a3984)
 ### Observation
- Since P value 0.029026773881587146 is less than alpha 0.05 
- Reject Null Hypothesis that Duplex mean yearly price is less than or equal to apartment mean yearly price i.e
 Duplex mean yearly price is greater than apartment mean yearly price.
![image](https://github.com/user-attachments/assets/a2c4ab98-401d-4f9b-9727-41f4051d01c1)

# Conclusion 
- This analysis shows that location and number of bedrooms significantly influence rental prices in Lagos. Properties in areas like Ikoyi and Victoria Island tend to command higher rents compared to other locations.
- Each additional bedroom leads to a substantial increase in rent—on average by about 50%.
- Among house types, duplexes are generally more expensive than apartments, likely due to having more rooms and larger spaces. However, the number of bedrooms often explains more of the price difference than the house type itself.
- Statistical tests (ANOVA, regression, and Kruskal-Wallis) confirm that:
- Rent prices vary significantly by location and edroom count has a strong, positive effect on rent
The final regression model explains over 50% of the variation in rental prices
This data-driven insight can help renters, landlords, and investors make smarter decisions in the Lagos housing market.





























  

    
    




