# FMCG Supply Chain Weather Intelligence

Project Overview
This project transforms raw historical weather data into a Strategic Decision Support System for FMCG operations in Australia. By analysing climate patterns, the dashboard provides actionable insights into logistics risk, storage integrity, and consumer demand triggers.
________________________________________
1. Dashboard Key Features
   
A. Seasonal Logistics Risk Index
•	Metric: Rainy Days Percentage.
•	Business Logic: High rainfall frequency directly correlates with "Last-Mile" delivery delays and increased transit risks. 
This visual identifies specific month-location combinations where the supply chain must "buffer" time for logistics.

B. Climate Variability Map (ArcGIS)
•	Visual: Spatial distribution across Australia.
•	Logic: A custom-calculated Climate Variability Score is mapped to identify "Red Zones"—regions where weather behavior is most unpredictable.
•	Calculation: This is a normalized average of the standard deviations of both rainfall and temperature range (Rainfall_std_norm+Temp_std_norm/2). It identifies volatility rather than just averages.

C. Climate-Induced Perishability Map (Scatter Plot)
•	Visual: X-Axis: Avg_Moisture_Index | Y-Axis: Avg_Temp_Range.
•	Logic: High moisture (humidity) + High Temperature Range = Accelerated Degradation.
•	Operational Action: Locations in the top-right quadrant are "High-Rotation Zones."
•	Strategy: Implement strict FEFO (First-Expired, First-Out) and reduce "Days of Inventory on Hand" (DOH) to prevent spoilage and moisture-related packaging damage (e.g., soggy cardboard boxes).

D. Demand Trigger Thresholds
•	Visual: Line chart with an Analytics Constant Line at 30°C.
•	Application: In FMCG, 30°C is a psychological and physical "Trigger Point" for cold beverages and ice cream. 
This tool allows managers to predict "Demand Spikes" and pre-position inventory before heatwaves occur.

E. Weather Predictability Analysis
•	Logic: Uses Temperature Standard Deviation as a proxy for predictability.
•	Insight: A low standard deviation suggests a stable climate (easier to forecast demand), while a high deviation indicates a "Volatile" climate where safety stock levels should be increased to prevent stockouts.

F. Interactive Location Filtering
•	Feature: Global Slicer for Location.
•	Utility: Allows regional managers to drill down into specific distribution hub profiles (e.g., Sydney vs. Darwin) to tailor local storage protocols.
________________________________________

2. Table Structure & Data Schema

Field Name--|--Type--|--Description.
Location--|--String--|--The geographical hub/city in Australia.
Date/Month--|--Time/Int--|--Temporal markers for seasonality analysis.
MaxTemp/MinTemp--|--Float--|--Daily temperature extremes.
Rainfall--|--loat--|--Daily precipitation volume (mm).
Evaporation--|--Float--|--Daily water loss from surfaces (mm).
Sunshine--|--Float--|--Daily hours of bright sunlight.
________________________________________
3. Derived Metrics & Methodology
Core Metrics
•	RainyDays: A binary flag where Rainfall>0. It counts the frequency of rain events regardless of volume.
•	HeavyRainDays: A binary flag where Rainfall>20mm. This represents "Extreme Weather" likely to cause flash flooding or total transport shutdown.
•	Temp_Range: (MaxTemp−MinTemp). Higher ranges indicate high daily thermal stress on product packaging.
•	RainDays_Percentage: (Sum of RainyDays/Total Days). Represents the probability of a rain event occurring.
________________________________________
4. Advanced Statistical Measures
   
a. Rainfall & TempRange Standard Deviation (std)
•	Why: It measures Inconsistency.
•	Application: High std means the weather is "Erratic." In visualization, this is used to identify high-risk months where baseline averages cannot be trusted for planning.

b. Moisture Index
•	Calculation: (Avg_Rainfall−Avg_Evaporation).
•	Application: Positive values indicate humid/damp conditions (risk of mold/packaging failure); negative values indicate arid conditions (static/fire risk).

c. Normalized Metrics (Rain_std_norm / Temp_std_norm)
•	Calculation: Valuenorm= x−min/max-min (min-max scaler)
•	Why: This scales different units (mm vs °C) onto a common 0 to 1 scale. This is necessary to mathematically combine temperature and rain data into a single score.

d. Climate Variability Score
•	Calculation: The mean of the normalized rainfall and temperature deviations.
•	Visual Use: Used as the primary color driver for the ArcGIS Map.
•	FMCG Value: High scores (near 1.0) signify "Strategic Risk Zones" where the business must implement flexible, highly responsive inventory models.
________________________________________
5. How to Use This Dashboard
   
a.	Select a Location via the slicer to see the specific risk profile for that distribution hub.
b.	Monitor the Demand Trigger chart during transition months (Spring/Autumn) to time the release of seasonal product lines.
c.	Audit the Logistics Heatmap monthly to adjust shipping lead times based on rainfall probability.

![Weather_data_dashboard_PowerBI](https://github.com/user-attachments/assets/c1461a2c-4f30-4454-8081-8a4d03f91fdc)

