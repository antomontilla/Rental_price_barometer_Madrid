# Project: Building a rental price barometer for Madrid using Idealista
Project for building a rental price barometer using Idealista for the city of Madrid.
Antonio Montilla, December 2023.

## Introduction and motivation
- Despite a recent economic slowdown prompted by increased policy interest rates globally, housing markets in major advanced economies remain notably tight. Nominal housing prices have sustained positive growth in 2023, as reported by the Bank of International Settlements (3.7% YoY in Spain and 2.4% in the US during the first half of the year).
- Unfavorable borrowing costs, stricter lending standards, and overall housing supply constraints have compelled many potential buyers to opt for renting, intensifying demand and subsequently driving up rental prices. Notably, cities like Madrid experienced a record-high average rental price in November, marking a 12% increase from the end of 2022, according to rental portal Idealista.
- In response to this dynamic market, our project aims to address the need for timely and precise information on rental conditions. Monthly publications of rental price data and the challenge of obtaining daily aggregate information from various real estate portals underscore the importance of a solution.
- Our project introduces a rental price barometer utilizing listings from the Idealista portal. Specifically, we develop a predictive model for rental prices in Madrid based on the portal's information at the beginning of December 2023, adding up to 4,500 listed properties. While the model lacks real-time updates due to data limitations, potential development in that direction is acknowledged.
- The trained model is incorporated into a rental barometer interface, engaging users in providing property features for a model-based prediction aligned with market prices as of December 2023. The interface provides users a predicted rental price range, statistical insights (average, minimum, and maximum) on current available properties matching the criteria, and a curated list of up to 5 potential listings. Additionally, users can access socio-economic information for the searched district sourced from Madrid’s government open data portal, featuring details on parks, health facilities, and resident demographics.

## Objectives
1. **Data Extraction.** Define and implement a robust process for extracting rental price listings using the Idealista API.
2. **Exploratory Data Analysis (EDA).** Conduct in-depth exploratory data analysis using statistical and visual techniques to unveil correlations, trends, and anomalies. Implement feature engineering, data cleaning, and wrangling techniques to prepare the data for modeling.
3. **Machine Learning Regression Modelling.** Construct a regression model using machine learning techniques to predict rental prices based on selected features. Compare and evaluate various regression models through cross-validation and hyperparameter search to determine the most suitable algorithm and model specification for the dataset.
4. **Model Deployment.** Develop a user interface for the rental price barometer app, integrating the selected regression model. Implement filters to allow users to select listings from the database, with the beta version serving as a prototype for potential future development.
5. **Complementary Database Integration.** Enhance the rental price barometer by incorporating socio-economic features of each district (demographics, median income, park availability) as optional information provided to users upon request.

## Data extraction
- The data for this project was obtained by the Idealista API, using a API-key and passwords kindly provided by the web portal for academic and research purposes.
- The process to obtain the data is explained and performed in the notebook Rental_price_barometer1_data_extraction.ipynb saved in this repository.
- The data obtained for this project consists of 4,500 listed properties in Idealista for rent in the city of Madrid. The main steps for obtaining the data were:
    * Building a function to URL encode API-key and password provided by Idealista, following the criteria set by the API documentation.
    * Setting a function to connect with the API and make requests for listed properties with the given specifications: rental properties in the city of Madrid, sorted by distance from Puerta del Sol geographical position and with a ratio limit of 10 km.
    * Transforming each response from Json format into a dataframe.
    * Producing a function to make requests for multiple pages, given that each response has a limit of 50 listings. This step allowed to store each response as separate csv file and combined all results into a final dataframe, which would be imported for analysis and modelling in this notebook.
- Due to data privacy, sensible information (API-key, csv files, information for each listing) is stored separately  and not published in this repository.
- Finally, for objective 5, socio-economic and demographic data is obtained from Madrid regional government open portal (see https://datos.madrid.es/portal/site/egob/menuitem.c05c1f754a33a9fbe4b2e4b284f1a5a0/?vgnextoid=71359583a773a510VgnVCM2000001f4a900aRCRD&vgnextchannel=374512b9ace9f310VgnVCM100000171f5a0aRCRD&vgnextfmt=default).

## Tech/framework used & links to other resources
- The project was developed using Jupyter in Python. There are 3 main notebooks saved in this git repository:
    * Rental_price_barometer1_data_extraction: for the data extraction using Idealista API.
    * Rental_price_barometer2_EDA_modelling: for processing and cleaning the data, exploration, analysis and modelling.
    * Rental_price_barometer3_deployment: for the deployment of the rental barometer.
- A presentation with main insights of the project can be found also in the repository.

## Main findings, caveats and further analysis
- This projected aimed to construct a price rental barometer to help both tenants and landlords get access to aggregated information on prices of the rental market in the city of Madrid.
- We successfully constructed a regression model using the random forest algorithm, leveraging the Idealista API for data extraction. The model, trained and tested on data from Idealista, demonstrated robust predictive capabilities with an accuracy score (R2) on the test set of 0.8. This high accuracy attests to the effectiveness of our approach in capturing rental price variations based on property features.
- The model's deployment in the form of a user-friendly rental barometer interface marked a significant step forward. This interface not only enables users to input property details for personalized price predictions but also serves as a reference point for current market trends. By providing statistics on rental prices from Idealista listings and suggesting relevant property links, the barometer empowers users in their property evaluation process.
- In addition to predictive pricing, our rental barometer offers users the ability to access socio-economic information about the desired district, providing a holistic view of the neighborhood. This integration enhances the user experience by considering broader factors beyond just rental prices.
- Despite the project's success, we acknowledge several limitations in the current version.
    * The model's training data, limited to properties listed as of December 11, 2023, poses a constraint on real-time prediction accuracy.
    * Furthermore, the inability to make real-time recommendations due to constraints in accessing live data from the Idealista API is a recognized challenge.
    * The user interface, while functional, requires refinement to enhance user-friendliness.
- In conclusion, our rental price barometer prototype offers a valuable tool for navigating the Madrid rental market. While acknowledging its current limitations, we view it as a stepping stone for further development.
