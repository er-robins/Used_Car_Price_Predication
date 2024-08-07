# Data-Driven Insights into Used Car Pricing

**Jupyter Notebook with code, experimentation, further insights, and deployment strategies: [here](https://github.com/er-robins/Used_Car_Price_Predication/blob/main/Used_Car_Price_Modelling.ipynb).**



## Business Goal

The used car market is a dynamic and mutifaceted industry that presents various opportunities and challenges for buisnesses and consumers. The Global used car market is substatial and continues to grow. In 2021, it was valued at approximately $1.5 trillion and is expected to grow at the CAGR of around 6% from 2022 to 2028. The U.S is one of the largest markets of used cars, with millions of vehicles sold annually. Recently during pandemic, used car market saw huge demand, bumping used car prices significantly. The Goal of this analysis is to develop a predictive model that can help guide consumers and delears in deciding appropriate pricing for the used cars. 

## Data

In this application, we explore a dataset from kaggle. The original dataset contained information on 3 million used cars. The provided dataset contains information on 426K cars to ensure speed of processing.  Our goal is to understand what factors make a car more or less expensive.  As a result of our analysis, we should provide clear recommendations to our client -- a used car dealership -- as to what consumers value in a used car.

![Distribution of Target Variable](images/Distribution_Target_Variable_Price.png)

## Modeling and performance

In this project, I employed various regression modeling techniques to predict used car prices. The models evaluated include `Linear Regression` and `Ridge Regression` with `polynomial features of Degree 2`. I also tried `Lasso Regression` and `Sequential Feature Selection`, though due to high computation cost they werent explored in detail, they can be good areas to expore in the future. Each model was trained and evaluated using a train/test split, followed by cross-validation and hyperparameter tuning using GridSearchCV to optimize performance. 

Among these, the Ridge Regression model demonstrated the best performance with a `Root Mean Squared Error (RMSE) of 5447.9089` and an` R-squared (R²) value of 0.8170`. 

To see the interactive plot of actual vs. predicted values, please click the link below:
[Actual vs. Predicted Values](https://github.com/er-robins/Used_Car_Price_Predication/blob/main/images/Actual_vs_Prediction.png)

To see full coefficient list :
[Full Coefficient list](https://github.com/er-robins/Used_Car_Price_Predication/blob/main/data/ridge_coefficients.csv)


### Evaluation Matric Choice :

I have used following two Matrics for evaluation.
1. **Root Mean Square Error (RMSE)**
   - **What is RMSE?**
     RMSE is a standard way to measure the error of a model in predicting quantitative data. Essentially, it tells you how concentrated the data is around the line of best fit.

   - **Why use RMSE?**
     - **Understandable Units:** RMSE values are in the same units as the predicted values. For example, if you are predicting the price of cars, an RMSE of 5000 means the average prediction error is about $5000.
     - **Error Sensitivity:** RMSE is especially good at identifying large errors because it squares the differences before averaging them. This means bigger errors have a disproportionately large impact on RMSE, highlighting problems in the model that might need attention.
     - **Clear Performance Indicator:** A lower RMSE value means the model has fewer and smaller errors, which is what you aim for. If you tweak your model and the RMSE goes down, it’s a sign you’re improving the model.

2. **Coefficient of Determination (R^2)**
   - **What is R^2?**
     R^2 measures how well your model’s predictions approximate the real data points. An R^2 of 1 indicates that the model perfectly predicts the data, while an R^2 of 0 means the model is no better than just predicting the mean of the data.

   - **Why use R^2?**
     - **Effectiveness of the Model:** R^2 gives you a quick insight into how much of the variance in the dependent variable your model can predict based on the independent variables.
     - **Comparison Tool:** It’s useful for comparing the strength of different predictive models. For instance, if one model has an R^2 of 0.80 and another has 0.90, you can say the second model has a better fit.
     - **Normalization:** Since R^2 is always between 0 and 1, it’s easy to interpret across different contexts and datasets, regardless of scale.

#### Matric choice summary :

- **RMSE** gives you a practical sense of how far off your model’s predictions might be in terms of dollars, which is directly applicable and easy to understand.
- **R^2** provides a percentage that tells you how much of the total variation in car prices your model captures, offering a way to gauge the model’s accuracy and usefulness.

Both metrics together provide a comprehensive view of the model’s effectiveness and areas for potential improvement, helping guide further refinements to enhance accuracy.

### Important observations about Coefficients and Findings
- All coefficents sorted in descending order are located at [Download ridge_coefficients.csv](data/ridge_coefficients.csv)
1. **Prominent Positive Influencers:**
   - **High-Value Models:** Top models like `simplified_model_5500`, `simplified_model_911`, and `simplified_model_c10` show the highest positive coefficients, significantly boosting the model’s predicted value, likely indicating premium or highly sought-after vehicle models.

2. **Negative and Positive Dynamics in Age and Odometer:**
   - **Negative Coefficients for car_age and odometer:** Both `car_age` (-17180.42) and `odometer` (-3992.08) have negative coefficients, suggesting that as vehicles age or accumulate mileage, their value or some other positive attribute (like desirability or reliability) typically decreases.
   - **Positive Coefficients for Polynomial Terms (`car_age^2` and `odometer^3`):** The positive coefficients for `car_age^2` (12729) and `odometer^3` (1430) indicate a non-linear relationship. This could suggest diminishing negative impacts or plateauing depreciation rates as age or mileage increases beyond certain thresholds, possibly reflecting collector value stabilization or decreased rate of additional depreciation.

3. **Utility and Specialized Vehicles:**
   - Vehicles designed for specific functions or heavy-duty use such as `simplified_model_f650`, `simplified_model_f750` show substantial positive coefficients, highlighting their valued attributes in utility or niche markets.

4. **Luxury and High-Performance Vehicles:**
   - Models like `simplified_model_tesla`, `simplified_model_porsche`, and `simplified_model_corvette` feature prominently with positive coefficients, indicating their strong market value and desirability.

5. **Impact of Vehicle Condition:**
   - The condition categories like `condition_new` (+624.09) positively influence the model, while `condition_salvage` (-1332.87) and `condition_fair` (-2172.72) have negative impacts, reflecting their effect on vehicle valuation.

6. **Transmission and Drive Type:**
   - **Transmission:** `transmission_manual` has a  positive effect (+987.31), whereas `transmission_Not_Specified` and `transmission_automatic` show negative coefficients, possibly reflecting market preferences or availability.
   - **Drive Type:** `drive_4wd` has a positive effect (+1724.30), supporting the value added by four-wheel drive capabilities, especially in certain geographical or usage contexts.

7. **Geographical Influences:**
   - States like `state_wa`, `state_hi`, and `state_mt` show positive coefficients, possibly reflecting regional preferences, economic conditions, or the suitability of certain vehicle types in these regions.

8. **Effect of Car Types:**
   - Specific car types like `type_convertible`, `type_coupe`, and `type_offroad` have positive coefficients, indicating higher value or preferences for these styles, whereas `type_sedan` and `type_hatchback` show negative impacts, potentially due to oversaturation or declining popularity.

9. **Overall Model Considerations:**
   - The wide range of coefficients across different car models, conditions, and other features highlights the complexity of vehicle valuation and the multifaceted nature of what drives vehicle market dynamics.

## Conclusion and Further Recommendations

Our analysis utilizing Ridge regression has yielded robust results, underlined by an RMSE of 5447.9089 and an R^2 value of 0.8170. These metrics confirm that our model achieves a substantial degree of predictive accuracy while capturing a significant portion of the variance within the dataset.

### Key Insights from the Analysis:

1. **Model Efficacy:**
   - The **R^2 value of 0.8170** indicates that approximately 81.70% of the variability in the target variable (car prices) is explainable by the features included in the model. This strong performance highlights the model's effectiveness in understanding and predicting car prices based on various vehicle characteristics.
   - An **RMSE of 5447.9089**, while substantial, is reasonable given the variability and range of car prices in the dataset. This measure provides a benchmark for expected prediction error and can be used to gauge individual predictions' accuracy.

2. **Influence of Vehicle Attributes:**
   - **Model Coefficients** have provided valuable insights into how different car models, conditions, and other features like mileage and age impact price evaluations. High-value models, such as luxury and performance vehicles, have shown a positive correlation with price, enhancing their valuation significantly.
   - The model also elucidates the depreciation effect through negative coefficients associated with higher `car_age` and `odometer` readings, though the positive coefficients for their squared terms suggest a tapering depreciation rate at higher values.

3. **Strategic Implications for Stakeholders:**
   - These insights are crucial for stakeholders in the automotive industry, including dealerships and manufacturers, to strategize inventory management, pricing policies, and marketing approaches. For instance, inventory strategies could be optimized to favor models that consistently show strong positive price influences.
   - Geographical and demographic data layers could further refine this model, potentially unveiling regional preferences that could impact pricing strategies.

### Recommendations for Model Enhancement:

To further enhance the predictive accuracy and utility of our model, the following steps are recommended:
- **Integrate Additional Data:** Including more granular data such as features specific to car luxury amenities, safety ratings, and consumer reviews could enrich the model's predictive context.
- **Explore Advanced Modeling Techniques:** Employing more complex algorithms or ensemble methods might capture additional nuances in the data.
- **Continuous Model Training:** Regular updates and training with new data will help the model adapt to market trends and changes, ensuring its relevance and accuracy over time.

### Final Thoughts:

The insights derived from this model provide a robust framework for understanding and predicting car values, offering actionable intelligence for business strategies. Continued refinement and adaptation to emerging data trends will enhance this model's precision and relevance in dynamic market conditions.


