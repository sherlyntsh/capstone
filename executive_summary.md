# Forecasting of Air Passenger Traffic at Singapore Changi Airport

## 1. Overview
Changi Airport was first built with just one terminal and one runway and officially began operations on July 1981. The second runway was then built in 1983 and commissioned in the following year. As passenger traffic increased, Terminal 2 and Terminal 3 were built and opened in November 1990 and January 2007 respectively to cope with traffic. Amidst the rise in popularity of low-cost travel, the budget terminal began operations in 2006 but subsequently closed in 2012 and was replaced with Terminal 4 which opened in 2017 [[1]](https://biblioasia.nlb.gov.sg/vol-17/issue-3/oct-dec-2021/changi-airport/).

Over the past 4 decades, passenger traffic continued to increase as air travel becomes increasingly prevalent and affordable due to the intense competition in the travel industry. To better meet the growing traffic and infrastructure needs, the plan for Terminal 5 was conceived and the construction is expected to begin in 2025 and eventually be completed in 2030. The addition of Terminal 5 is a monumental one as it marks the biggest expansion of the airport thus far, and it would be able to handle up to 50 million passengers annually in the initial phase of operations. Across all 5 terminals, the airport's total annual passenger handling capacity is expected to reach 135 million [[2]](https://www.airport-technology.com/projects/terminal-5-changi-international-airport/). This expansion of the airport is also part of the Changi East development which includes development of other areas such as landside and aviation support facilities and the Changi East Industrial Zone, to further strengthen Singapore's air hub status and its competitive edge.


## 2. Problem Statement
Changi Airport has been awarded with more than 660 “Best Airport” awards since it first opened and it was named the “world’s best airport” for a record 12th time earlier in March this year [[3]](https://www.cnbc.com/2023/03/16/best-airport-in-the-world-singapores-changi-airport-says-skytrax.html). The strategic addition of Terminal 5 would allow the airport to better serve passengers in all areas of arrival, departure and transit.

This project seeks to utilise regression and time series forecasting models to forecast passenger traffic to assess sufficiency of the passenger handling capacity of Changi Airport with the addition of Terminal 5.


## 3. Data Source
The passenger arrival and departure numbers through Changi Airport would be used to forecast the passenger traffic and the data are published by the Department of Statistics Singapore:
- Air Passenger Departures By Region/Country Of Disembarkation
- Air Passenger Arrivals By Region/Country Of Embarkation

The passengers served by the airport goes beyond just the passengers who arrive or depart from Singapore, but also the passengers who chose Singapore to transit at for their onward flight to their final destination. However, the above datasets do not include the number of transit passengers. Thus, data on transit passengers are sourced for separately from the following dataset:
- Civil Aircraft Arrivals And Departures, Passengers, Air Cargo Tonnage, Direct And Transhipment Tonnage And Mail


## 4. Model Evaluation Criteria
The objective would be for the final selected model to:
1. Outperform the baseline model; and / or
2. Achieve a MAPE of 10% or lesser.


## 5. Conclusion
Based on the data, it is observed that there is a general increasing trend in air passenger traffic across the past decades but with impact of external factors such as the SARS and COVID-19 outbreak clearly visible. When averaging on a monthly basis across the years, a general increasing trend is also observed with the peak in December. This indicates that air travel demand is mostly concentrated at the end of the year which coincides with the holiday period and the period in which most people would be taking time off from work before the next calendar year.

A total of 6 models consisting of linear regression and XGBoost (with lagged and differenced values), as well as Prophet were explored in 2 parts:
1. Built using original dataset
2. Built using truncated dataset (to only retain data prior to the impact of COVID-19)

As time series data is in a chronological order, models tend to perform well on the train set but badly on test set due to the presence of the sudden and drastic drop in air passenger traffic caused by the COVID-19 pandemic in the test set. Thus, the 3 models were built again but using the truncated dataset as a mean to objectively assess the model's performance. By using the truncated dataset, there are significant improvements in the performance of all models on the test set but the performance of the XGBoost model remains lacklustre as compared to linear regression and Prophet. The Prophet model was eventually selected as the final model to be used for the forecasting of air passenger traffic in view of its test MAPE score (of about 6.68%) being the lowest. Based on the objective stated in the Project Overview, the selected model has achieved the targets set out in the beginning.


## 6. Recommendation
As air travel demand returns in the midst of the pandemic's aftermath, air passenger traffic is expected to return to pre-pandemic level by 2024 [[4]](https://www.straitstimes.com/singapore/politics/passenger-traffic-at-changi-airport-expected-to-recover-fully-by-2024-or-possibly-earlier-iswaran#:~:text=Giving%20this%20update%20on%20Friday,recovered%20fully%20since%20January%202023.). To forecast the air passenger traffic in mid-2030 (i.e., June 2030), the pre-pandemic period (early 2020) is assigned as January 2024 before forecasting into the future to arrive at the period of (pseudo) June 2030 assuming that the increase in air passenger traffic follows the pre-pandemic trend.

Using the Prophet model, the forecasted air passenger traffic in (pseudo) June 2030 would reach about 6.8 million and this leads to an estimated annual number of 82 million passengers passing through Changi Airport. With the completion of Terminal 5 in mid-2030, Changi Airport's total annual passenger handling capacity would be increased up to 135 million [[5]](https://www.airport-technology.com/projects/terminal-5-changi-international-airport/). Thus, it can be concluded that Changi Airport would be well-equipped to handle the forecasted growth in air travel with the completion of Terminal 5 and with ample headroom for further growth.

By further stretching out the forecasting timeline of the Prophet model to determine the estimated time frame in which the air passenger traffic would approach the handling capacity limit, it is observed that the annual forecasted traffic would reach about 133 million by (pseudo) August 2049. Thus, the airport operations team could look into potential expansion plans for the terminals starting from year 2039.


## 7. Future Steps
Firstly, additional models could be explored to forecast the air passenger traffic by regions since the collected data on arrival and departure traffic contains the breakdown by region. With these forecasts, it could potentially further assist the airport operations team in planning the flight distribution across the five terminals.

Another aspect to consider would be to source for alternative sources of data which records the air passenger traffic observations on a daily basis to increase the number of observations and investigate its impact on the models' performances. This is in view of the fact that the current datasets records the observations on a monthly basis which gives only 412 rows of observations at maximum after dropping the records for the earlier years to focus only on the air passenger traffic for Changi Airport.

For the linear regression model, additional features could be added to indicate local and / or regional holiday periods to further investigate its impact on these models' performances. Other variables such as socioeconomic indicators (i.e., Gross Domestic Product, population, Consumer Price Index) could also be considered.

Lastly, the ConvLSTM2D model which is a hybrid of hybrid between Convolutional Neural Networks and Recurrent Neural Networks could be further researched on and explored for use. This is in view of the positive outcome of relatively low MAPE values of about 3% to 9% documented in the scientific article on air passenger demand forecast published by the Embry-Riddle Aeronautical University, despite including observations affected by the COVID-19 pandemic [[5]](https://commons.erau.edu/cgi/viewcontent.cgi?article=1726&context=ijaaa).