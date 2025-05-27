# ACCIDENT TREND FORECASTING


# 1. **Business Understanding**

Aviation safety is paramount in the airline industry, where each accident can result in catastrophic consequences, not only in terms of human life but also reputational and financial losses. The National Transportation Safety Board (NTSB) has collected extensive accident data from 1962 to 2022, offering a unique opportunity to investigate patterns, root causes, and contributing factors of aviation accidents in the U.S.

By leveraging machine learning and data science, we aim to uncover insights and build predictive models to improve situational awareness, inform safety protocols, and ultimately reduce the frequency and severity of aviation incidents.

**Problem Statement**

Despite advances in aviation technology and regulation, accidents continue to occur due to a variety of factors such as weather, pilot error, aircraft condition, and flight phase. The challenge lies in understanding which conditions most often lead to severe outcomes and forecasting future risks based on historical trends.

**Project Objectives**

1. Descriptive Analysis:

- Explore trends in aviation accidents over the decades (frequency, location, severity).

- Identify the most common causes and contributing factors.

2. Predictive Modeling:

- Develop a time series model to forecast future accident trends.

3. Interpretability:

- Use feature importance to explain what drives severe accidents.

4. Recommendations:

- Suggest actionable insights for aviation safety regulators and flight operators.

**Key Business Questions**

1. What flight phases and weather conditions are most associated with fatal accidents?

2. Can we predict the severity of an accident based on pre-incident conditions?

3. Are accident rates increasing or decreasing over time?

4. Which types of aircraft or operations  are most at risk?

5. How can predictive models assist in safety planning and incident prevention?


**Metrics of Success**

1. For Time Series:

- MAE / RMSE – Forecast error

- MAPE – Percentage error for trend forecasting

- Visual Fit – Actual vs. Predicted graph quality

2. Business Metrics:

- Actionable insights that can inform safety recommendations

- Ability to highlight the top 5 features contributing to high-severity accidents

- A model that can generalize across different types of flights and conditions

# 2.0 **Data Understanding**

1. Dataset Overview

- Records: 88,889

- Columns: 31

- Time Range: 1962–2022

- Source: NTSB Aviation Accident Database

2. Key Columns by Category

-  Identifiers & Meta:
Event.Id, Investigation.Type, Accident.Number

3. Time & Location:

- Event.Date: Primary time series axis

- Location; Country, Latitude, Longitude

4. Aircraft & Operator Info:

- Make, Model, Aircraft.Category, Engine.Type

- Air.carrier, Operator

5. Incident Context

- Broad.phase.of.flight – Phase during which the accident occurred

- Weather.Condition – Visual/Instrument meteorological conditions

- Purpose.of.flight – Personal, Commercial, Instructional, etc.

6. Accident Impact

- Injury.Severity–Total.Fatal.Injuries, Total.Serious.Injuries, etc.

- Aircraft.damage – Minor, Substantial, Destroyed

# **Exploratory Data Analysis (EDA)**

## **Univariate Analysis**

![image](https://github.com/user-attachments/assets/5d5b5305-956b-49f2-a242-b82235dc6cd0)

**Observations**:

Most investigations are labeled as "Accident" which is 96%.

![image](https://github.com/user-attachments/assets/0763c413-33cd-4c29-8a26-40e1a56e12e1)

**Observations**:

- The most frequent outcome in terms of injury severity is "Non- Fatal" and "Fatal" with over a thousand cases.

- The other severities occur less frequently, with "Serious" being the least common among the displayed top 5.

  ## **Bi-variate Analysis**

  ![image](https://github.com/user-attachments/assets/133da8cc-dab6-46dc-9452-ed385c95a1ca)

  **Observations:**

- There is a strong positive correlation between total fatal injuries and total injuries. As the number of fatal injuries increases, the total number of injuries also tends to increase.

- Many points are clustered along the x-axis and close to the y-axis, indicating many accidents with few or no injuries.

- There's a clear line where total injuries equal fatal injuries, representing accidents where all injuries were fatal.

  ![image](https://github.com/user-attachments/assets/c20a186b-3b99-4620-8e2a-f15b3fa0322a)

  **Observations:**

- Similar to the accident count, there is a general downward trend in the total number of injuries from aviation accidents between 2000 and 2022.

- This suggests that not only are accidents becoming less frequent, but the total human impact in terms of injuries is also decreasing



## **Multi-variate Analysis**

![image](https://github.com/user-attachments/assets/61465f86-bd7b-4041-a313-3151504e2393)

**Observations:**

- Points colored "Fatal" are generally concentrated in the upper right portion of the scatter plot, where both total injuries and fatal injuries are high.

- Points colored "Non-Fatal" are clustered along the x-axis, indicating accidents with total injuries but zero fatal injuries.

- Points colored "Serious" and "Minor" are found in between, with lower total injuries and a range of fatal injury counts (mostly low). This visual reinforces the relationship between the different injury metrics and the categorized injury severity.

  ![image](https://github.com/user-attachments/assets/b3083034-e08a-457f-ab3c-cac07f68cd5f)

  **Observations:**

- Among the top 5 makes, "Boeing" aircraft with "Jet" engines show the highest average number of fatal injuries.

- "Airbus" with "Jet" engines also shows a high average number of fatal injuries.
Makes like "Cessna" and "Piper" with

- "Reciprocating" engines have much lower average fatal injuries per accident, even though they have high accident counts.

# MODELING

=== ARIMA In-Sample Evaluation ===
Mean Absolute Error (MAE): 89.21
Root Mean Squared Error (RMSE): 112.48

![image](https://github.com/user-attachments/assets/bfff4bf2-88b3-420b-8154-e705b24ba9dd)

![image](https://github.com/user-attachments/assets/19607b52-a97c-44ea-97b2-76ceb5d957d3)

**Insights and Observations**

1. **Overall Trend Capture:** The red line representing the ARIMA predictions generally follows the downward trend observed in the actual test data (orange line). This suggests the model is capturing the underlying trend of decreasing accident counts.

2. **Fluctuation Handling:** The ARIMA model seems to smooth out the year-to-year fluctuations present in the actual data. The predicted line is less volatile than the actual data points in the test set. This is typical of many time series models that aim to capture the underlying pattern rather than the specific noise or irregularities in individual periods.

3. **Accuracy in the Test Period:** To make more precise observations about accuracy, you would need to compare the predicted values (red line) to the actual values (orange line) for each year in the test period. Visually, you can see how close the red dots are to the orange dots. The RMSE and MAE values printed below the plot provide quantitative measures of this accuracy. Lower values indicate better performance.

4. **Potential for Improvement:** While the model captures the trend, there might be noticeable differences between the predicted and actual values in certain years of the test set. This suggests there's room for improvement in the model's ability to capture the nuances or specific deviations in the time series. This could involve:

5. **Tuning the ARIMA parameters (p, d, q).**
Exploring other time series models (e.g., Prophet, seasonal ARIMA).
Considering external factors that might influence accident rates (though this would require more complex modeling).
Forecasting Beyond the Test Period: The plot shows predictions only up to the end of the test period (2022). If you were to forecast further into the future, the model would continue the trend it has learned. The reliability of those future forecasts would depend on how well the historical trend continues and whether any significant external events occur.

- In summary, the visualization indicates that the basic ARIMA model successfully identifies and projects the downward trend in aviation accidents. However, its ability to precisely predict the specific accident count for each year in the test set may be limited, as evidenced by the smoothing effect on fluctuations. The evaluation metrics (RMSE, MAE) provide a more objective measure of this performance.

=== Prophet In-Sample Evaluation (2000–2022) ===
Mean Absolute Error (MAE): 79.96
Root Mean Squared Error (RMSE): 100.41

![image](https://github.com/user-attachments/assets/1b160480-a792-4b83-b531-88653697a323)
Prophet Forecast - Aviation Accidents (2000-2027)" 

**Observations:**

1. Declining Trend: The historical data (black dots and blue line) from 2000 to around 2023 shows a general downward trend in aviation accidents.
Seasonality/Fluctuations: While there's a downward trend, there are clear year-to-year fluctuations. For example, there's a noticeable dip around 2008 and a more significant dip around 2020.

2. Confidence Interval (Shaded Area): The blue shaded area represents the confidence interval (likely 95% confidence). It indicates the range within which the actual accident count is expected to fall. The interval widens as the forecast horizon extends, reflecting increased uncertainty.
Forecast (2024-2027): The blue line continues the downward trend into the forecast period. The forecast predicts a continued decrease in aviation accidents, though with more uncertainty as indicated by the widening confidence band.
2020 Dip: There's a very sharp and significant drop in accident count around 2020, likely attributable to the global impact of the COVID-19 pandemic on air travel.
Post-2020 Rebound/Adjustment: After the 2020 dip, there's a slight rebound/increase in 2021 before the trend appears to continue downwards.
Insights:

3. Effectiveness of Safety Measures: The overall downward trend suggests that aviation safety measures, technological advancements, and operational improvements over the years have been effective in reducing the number of accidents.
Impact of External Factors: The sharp dip in 2020 highlights how significant external events (like a global pandemic affecting travel) can drastically alter trends and present challenges for forecasting.

4. Uncertainty in Long-Term Forecasts: The widening confidence interval emphasizes that predictions further into the future (e.g., 2026-2027) are inherently less certain than short-term predictions.

5. Prophet Model Suitability: The use of a "Prophet Forecast" suggests the model is designed to handle trends and seasonality, which appear to be present in this data.
Base Rate Fallacy Consideration: While accidents are declining, it's important to consider if this is also reflective of a decline in total flight hours or if the accident rate per flight hour is decreasing. This chart only shows raw accident count.


# **Conclusion**

This project provided a comprehensive analysis of aviation accidents using historical data from 1962 to 2022. Through exploratory data analysis (EDA), we identified key patterns and trends in accident occurrences, such as seasonal fluctuations, high-risk aircraft categories, and common phases of flight associated with severe injuries. The dataset was then enriched through feature engineering to improve model performance.


The forecasting component aimed to predict future accident trends. Time series models provided valuable insights into long-term patterns and potential future risks, which can help stakeholders in resource planning and preventive measures.

Overall, the integration of data preprocessing,  and forecasting created a well-rounded pipeline that can support safety improvements in the aviation industry.

# **Recommendations**

1. Enhance Data Collection:

- Improve data completeness for missing or underreported fields (e.g., exact weather conditions).

- Include human factors data (e.g., pilot experience, fatigue) if available, as these are critical for understanding accident causes.

2. Model Improvement:

- Use advanced time series models such as LSTM, or SARIMA for more accurate forecasting with seasonal components.

3. Feature Expansion:

- Incorporate additional geospatial data (e.g., flight routes, airport proximity) to analyze location-based risks.

- Add external factors such as aviation regulation changes or major events (e.g., pandemics, economic downturns).

4. Deployment & Monitoring:

- Develop a dashboard (e.g., in Tableau or Power BI) to visualize key trends and model predictions in real time.

- Set up periodic model retraining and evaluation as new data becomes available to maintain accuracy.

5. Industry Collaboration:

- Share insights with aviation authorities, maintenance crews, and training programs to tailor 

