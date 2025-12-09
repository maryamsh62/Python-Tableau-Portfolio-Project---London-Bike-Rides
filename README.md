# London Bike Rides 2015-2016

This project analyzes the [London Bike Sharing dataset](https://www.kaggle.com/datasets/hmavrodiev/london-bike-sharing-dataset) from Kaggle and turns it into an interactive Tableau dashboard. Python is used for data access and preparation, and Tableau is used for visual exploration of bike-sharing patterns over time and weather conditions.


![London Bike Rides Dashboard](https://github.com/maryamsh62/Python-Tableau-Portfolio-Project---London-Bike-Rides/blob/master/London%20Bike%20Rides%20Dashboard.png)

[TableauPublic](https://public.tableau.com/app/profile/maryamsadat.shakeri/viz/LondonBikeRides_17652456944070/LondonBikeRidesDashboard)



---

## Project Overview

1. Use the **Kaggle API** in Python to programmatically download the *London Bike Sharing* dataset.
2. Explore, assess, and clean the data with **pandas**.
3. Export the final, cleaned dataset to Excel as `london_bike_rides_final.xlsx`.
4. Build an interactive **Tableau** dashboard that lets the user:
   - See the total number of bike rides over the analysis period. 
   - Explore a **moving average** of rides with user-defined parameters.
   - Analyze how **temperature** and **wind speed** relate to the number of rides.
   - Drill down into rides by **weather type** and **hour of day** via tooltip charts.
   

This dashboard shows that London’s bike usage is strongly seasonal and weather-dependent, peaking in mild spring–summer conditions and dropping in colder, windier weather.

---

## Dataset

The **original** Kaggle **London Bike Sharing dataset** has:
- `17,414 rows`
- `10 columns`

This dataset contains hourly records of bike rentals in London, along with weather and seasonal information.

It includes variables such as `temperature`, `wind speed`, `humidity`, `weather conditions`, and whether the day is a working day or holiday.

This structure makes it ideal for exploring how the time of day and weather affect bike usage patterns.


---

## Project Files & Tools

- `london_merged.csv`
- `london-bike-sharing-dataset.zip`
- `london_bike_rides_final.xlsx`
- `london_bike_rides.ipynb`
- `London Bike Rides.twbx`
- `London Bike Rides Dashboard.png`
- `README.md`

**Tools**: `Python`, `pandas`, `Kaggle API`, `Visual Studio Code`, `Tableau Desktop / Tableau Public.`



---

## Tableau Dashboard

The dashboard contains five views built on top of the cleaned dataset:

1. **Total London Bike Rides**  
   - A big KPI card showing the total number of rides between the selected start and end dates.

2. **Moving Average Rides (Timeline)**  
   - A line chart showing the number of rides and their moving average.
   - Driven by user-defined parameters (timeframe and window length).
   - A highlighted segment shows the currently selected timeframe.

3. **Temperature vs Wind Speed Heatmap**  
   - A heatmap with **temperature (°C)** on one axis and **wind speed (kph)** on the other.
   - Cell color encodes the number of rides for each temp–wind combination.

4. **Weather Tooltip Chart**  
   - Appears when hovering over a mark on the main views.
   - Shows bike rides split by **weather condition**.

5. **Hour Tooltip Chart**  
   - Also displayed via tooltip.
   - Shows bike rides split by **hour of day**, allowing a quick view of peak usage times.

Hovering over the heatmap or moving-average timeline reveals the tooltip charts, so users can instantly see how rides break down by weather and hour for the selected point or range.

---

## Parameters & Calculated Fields in Tableau

The dashboard relies on a set of user-defined parameters and calculated fields to keep it interactive and flexible.

### 1. Parameters

1. **Moving Average Duration**  
   - Numeric parameter controlling the size of the moving-average window.  
   - Used inside the moving-average calculation instead of a hard-coded value (e.g., `-2`).

2. **Moving Average Timeframe**  
   - Date parameter that works with a range slider.
   - Defines the period the user is currently exploring.

---

### 2. Data Type Adjustments

- The original **time** field from the dataset is converted from **string** to **date & time**.
- A new calculated field **` Moving Average Timeframe`** is created, and its data type is changed to **Date** (instead of Date & Time) to simplify filtering and display in the slider. 

---

### 3. Sets & Helper Calculations

1. **Moving Average Timeframe Set**  
   - A set based on the `Moving Average Timeframe` field.
   - Used to highlight the selected portion of the timeline.

2. **` Min Month` and `Max Month`** (calculated fields)  
   - Capture the minimum and maximum months in the dataset.
   - Useful for setting up axis ranges and default slider values.

3. **`Range`** (calculated field)  
   - Used to color the line chart differently for the selected timeframe vs. the rest of the data.
   - When a date is in the `Moving Average Timeframe` set, it’s one color; otherwise, another.

---

### 4. Moving Average Calculation

**Calculated field: `Moving Average Rides`**

- Implements the moving average logic driven by the **Moving Average Duration** parameter.
- Conceptually:
  - Instead of using a fixed window (e.g., `-2` to represent “current day + previous two days”), the window size is controlled by the parameter.
  - This creates a dynamic rolling window of *N* days, where *N* is defined by the user.
  - A duration of 3 days, for example, would take the current day and the two previous days.

This makes the moving average **fully interactive**—users can switch between short-term and long-term trends without modifying the underlying calculation.

---

### 5. Additional Calculations

1. **`hour`**  
   - Extracts just the **hour of day** from the datetime field.
   - Used in the tooltip chart that shows bike rides by hour.

2. **Tooltip Charts (Weather & Hour)**  
   - Two separate worksheets:
     - **Bike rides by weather**
     - **Bike rides by hour**
   - Added to tooltips of the main views so that hovering over the line chart or heatmap reveals detailed breakdowns.






