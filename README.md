# Predicting Tracheal, Bronchus and Lung Cancer Deaths in India using Air Quality Data
## Riya Chaturvedi

## I. INTRODUCTION & BACKGROUND 

India has been experiencing worsening air quality over the past 5 years. New Delhi, bearing the brunt of this crisis, sees AQI levels exceed 800 almost annually, particularly in the periods of September-December. Meanwhile, Air Quality Index benchmarks a levels of 100 to be unsuitable for breathing. India's air pollution crisis has created a public health burden with the population increasingly facing lung and respiratory issues, developing chronic illnesses and exacerbating current ones. A study by Jagannathan et al. (2024) found that long-term exposure to air pollution increased deaths by 1.5 million per year in India, when compared to conditions if India met the World Health Organization’s recommendations for safe exposure. 

While Delhi is at the forefrunt of the crisis, states in other regions of India also face increasing air pollution levels 2016 onwards, contributing to the public health crisis. 

This project aims to predict lung cancer deaths in India using air quality data, such as NO2, SO2, PM 2.5 AND PM 10 levels, among other relevant variables. The aim of this model is to eventually predict the long-run impact of worsening air quality in the country, especially since effects of air pollution are observed in lags. Moreover, by predicting lung cancer mortality over a period of time, we can quantify the effects of worsening air quality and also anticipate the additional public health or cancer infrastructural burden that will fall on India's health system. 

Given the size of the dataset and several missing values, I use two ML methods to train and predict the data- using the best model to make the predictions. Due to the data set being small, I use a Bootstrapped Lasso-regularized regression and given many missing values in the data set I also implement an XGBoost model that is adept in dealing with missingness of data. I will compare the RMSE and MSE's of the two models. 

## II. DATA & STUDY DESIGN 

For this project I use a dataset that I created using sources like the IHME Global Burden of Disease data for Indian states and India's National Family Health Survey 5 (2019-21). For air quality data, I used India's Central Pollution Control Board's (CPCB) AQI repository. The final dataset covers 33 Indian states between 2017-21, containing the following relevant variables- 

1. State: Name of Indian State
2. Year
3. tbl_deaths: Tracheal, Bronchal or Lung Cancer deaths (raw number) (IHME)
4. SO2: SO2 concentration in µg/m3 (CPCB)
5. NO2: NO2 concentration in µg/m3 (CPCB)
6. PM10: PM 10 concentration in µg/m3 (CPCB)
7. PM2.5: PM2.5 concentration in µg/m3 (CPCB)
8. Population: total population in each state (IHME)
9. total_tobacco_rate: Total % of population that uses tobacco in any form in each state (NFHS Prediction- Halder et al. 2024)
10. male_tobacco_perc: % of Men that use any type of tobacco in each state (NFHS-5) (data for only 2019-21)
11. female_tobacco_perc:  % of Women that use any type of tobacco in each state (NFHS-5) (data for only 2019-21)
12. hale: Health-adjusted Life Expectancy at birth (0-6months) to control for population health differences in each state (IHME)
13. covid_deaths: Covid-19 total number of deaths in each state for each year (0 before 2020), using this in order to account for the changes in air quality between 2020-21 as well as the possible impact of Covid-19 infections on those with comorbidities like lung cancer. This variable aims to capture the extend of the impact fo Covid-19 (IHME)
14. tbl_rate: Tracheal, Bronchus and Lung Cancer Rates -- main outcome feature (IHME)
