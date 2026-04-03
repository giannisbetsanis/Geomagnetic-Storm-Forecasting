# Geomagnetic Storm Prediction using Random Forest 

### Forecasting the Dst Index based on 22 Years of NASA OMNIWeb Data

## Project Overview
This project was developed as part of my **Bachelor's Thesis at the Department of Physics, University of Patras** titled **Satellite Data Processing and Analysis for Solar Wind and Space Weather** . The primary objective is to predict the **Dst (Disturbance Storm Time) index** using the **Random Forest** algorithm, using solar wind parameters to forecast geomagnetic storm intensity.

## Physical Rationale & Feature Engineering

The model's high predictive accuracy ($R^2 = 0.96$) is rooted in the integration of key magnetospheric physics principles into the feature engineering process:

### 1. Solar Wind Time Lags (1h & 2h)
I implemented **1-hour and 2-hour time lags** for solar wind parameters ($B_z$, $V_{sw}$, $N_p$). This accounts for the inherent delays in the Earth's response to solar forcing:
* **Energy Transfer:** Although OMNIWeb data is shifted to the magnetopause, energy transfer via magnetic reconnection and subsequent plasma transport to the magnetotail is not instantaneous.
* **Particle Injection:** It takes time for solar wind particles to be injected into the inner magnetosphere and enhance the Ring Current.

### 2. Dst Autocorrelation & Trend Detection
The model incorporates **lagged Dst values ($Dst_{t-1}, Dst_{t-2}$)** for two fundamental reasons:
* **Initial Conditions (Baseline):** Geomagnetic storms are continuous processes. Without the previous state ($Dst_{t-1}$), the model would lack a reference point, potentially leading to large baseline errors.
* **Trend & Gradient Identification:** By providing the two most recent values, the Random Forest can internally calculate the **rate of change** (gradient). This is crucial for distinguishing whether a storm is in its **intensification phase** (falling Dst) or **recovery phase** (rising Dst). This prevents the model from making "blind" predictions based solely on instantaneous solar wind conditions, which might not yet have manifested in the ground-based measurements.

### Result
By combining **external forcing** (lagged solar wind) with **internal system dynamics** (autocorrelation), the model successfully captures the causal links governing geomagnetic storms rather than just identifying statistical correlations.

## Key Achievements
- **High Accuracy:** Achieved a Coefficient of Determination **$R^2 = 0.9579$** and **$RMSE = 3.22$ nT** on the test set.
- **Physics-Informed Feature Engineering:** Implemented a **Time-Lagging** strategy ($t-1, t-2$ shifts) to capture the temporal evolution and inertial response of the magnetosphere.
- **Big Data Analysis:** Processed and cleaned 22 years of high-resolution time-series data (1997-2019) from NASA's OMNIWeb database.

## Visual Analysis & Results

### 1. Solar Wind Bz vs Geomagnetic Activity
![Bz vs Dst](1.Dst_Bz_component.png)
*Correlation between the Interplanetary Magnetic Field (IMF) B_z component and the geomagnetic response.*

### 2. Actual vs Predicted Dst (Regression Analysis)
![Scatter Plot](2.Actual_vs_Predicted_Dst.png)

*Scatter plot showcasing the strong linear correlation (R^2=0.96) between measured and predicted values.*

### 3. Feature Importance (Random Forest)
![Feature Importance](3.FeatureImportance.png)
*Analysis of variable contributions, highlighting the dominance of B_z and the previous state (Dst_{t-1}).*

### 4. Time-Series Prediction Performance
![Detailed Comparison](4.Measured_Dst_vs_RF_prediction.png)
*A side-by-side comparison of measured Dst values and model predictions over time.*

## Tech Stack
- **Language:** Python 3.x (Jupyter Notebook)
- **Libraries:** Scikit-learn, Pandas, NumPy, Matplotlib, Seaborn
- **Data Source:** [NASA OMNIWeb Service](https://omniweb.gsfc.nasa.gov/)

---
**Contact:** [giannisbetsanis@gmail.com] | [www.linkedin.com/in/giannis-betsanis-730018361]
