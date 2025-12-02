Project Overview

This project performs a complete Exploratory Time Series Analysis (TSA) on the classic AirPassengers dataset.
It includes:

✔ Data loading & cleaning
✔ Time series visualisation
✔ Decomposition (Additive, Multiplicative, STL)
✔ ADF stationarity testing
✔ Log-transform & differencing
✔ ACF/PACF analysis
✔ Outlier detection
✔ Feature engineering
✔ Train–Test split

This dataset contains monthly airline passenger numbers from 1949 to 1960 and is widely used to learn time-series forecasting.

📁 Dataset Details
Column	Description
Month	Monthly time index (Date)
#Passengers	Number of monthly airline passengers

📌 Total rows: 144
📌 Time range: 1949 → 1960
📌 Frequency: Monthly (MS)

🧼 Data Cleaning Steps

Converted Month column into DateTime index

Ensured numeric values

Checked missing values → 0 missing

Checked duplicate timestamps → no duplicates

Sorted values by date

📊 Exploratory Data Analysis
🔹 Raw Series Plot

Shows clear increasing trend + strong yearly seasonality + increasing variance.

plt.figure(figsize=(12,4))
plt.plot(ts.index, ts.values)
plt.title('Raw Time Series')
plt.grid(True)

🔍 Time Series Decomposition
✔ Additive Decomposition
✔ Multiplicative Decomposition
✔ STL (robust) Decomposition

All approaches confirm:

Strong upward trend

Strong 12-month seasonality

Residuals show noise

stl = STL(ts, period=12, robust=True).fit()
stl.plot()

🔧 Transformations & Stationarity
✔ Log transform
✔ First difference
✔ Seasonal difference
✔ Seasonal + First difference

These steps help stabilize variance & remove trend/seasonality.

🧪 ADF (Augmented Dickey–Fuller) Test Results
Series	Stationary?	p-value
Raw	❌ No	0.99
Log	❌ No	0.42
First Difference (log)	❌ Almost	0.07
Seasonal + First Difference	✅ Yes	0.0002

➡ Final differenced series is stationary and suitable for ARIMA/SARIMA modeling.

📉 ACF & PACF Analysis

Used to identify AR, MA, and seasonal components for ARIMA/SARIMA:

plot_acf(first_diff, lags=36)
plot_pacf(first_diff, lags=36)


Shows:

Seasonal spikes at lag 12

Useful for selecting (p, d, q) parameters

🔎 Outlier Detection

Used ±3σ threshold.
✔ No significant outliers found.

🛠 Feature Engineering

Created the following features:

year

month

rolling_12 (12-month moving average)

lag_1

pct_change_1

Saved to CSV:

ts_eda_features.csv

🧪 Train–Test Split

Last 12 months → Test set

Remaining data → Training set

train = ts.iloc[:-12]
test  = ts.iloc[-12:]


Great setup for:

✔ SARIMA
✔ ETS
✔ Prophet
✔ LSTM forecasting

🚀 Requirements

Install all libraries:

pip install pandas numpy matplotlib statsmodels

▶️ How to Run

Run in Google Colab or local Jupyter Notebook:

python timeseries_analysis.py

📚 Conclusion

The AirPassengers dataset shows strong trend + strong seasonality.

After log + seasonal differencing, the data becomes stationary.

ACF/PACF plots show seasonal patterns—perfect for SARIMA forecasting.

Clean features and train/test split make the dataset ready for time-series forecasting models.

👩‍💻 Author

Your Name Here (optional)
