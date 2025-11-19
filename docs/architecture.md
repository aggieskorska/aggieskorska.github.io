# Rough Architecture ConsiderationsIngestion
1. Azure Data Factory
    * Triggers hourly (solar) / daily (heat pump + weather)
    * Calls Azure Functions or Databricks jobs to hit APIs
    * Writes raw JSON into ADLS Gen2 (Bronze)
    * Processing
1. Databricks
    * PySpark notebooks
    * Delta Lake Bronze → Silver → Gold
    * Auto Loader if you want streaming
    * MLflow for model tracking
1. Storage
    * ADLS Gen2 with Delta Lake
    * Bronze: raw JSON
    * Silver: cleaned tables
    * Gold: analytical models, aggregations
1. Transformation
    * DBT inside Databricks (optional but very impressive)
1. Serving
    * Power BI / Databricks SQL dashboards
    * REST API endpoint via Databricks Serving
1. Orchestration
    * ADF pipeline
    * Extract → Load → Transform
    * Alerts + retries
    * Logging + monitoring
1. Infrastructure-as-Code
    * Databricks workspace
    * KeyVault
    * Storage
    * ADF
    * Functions
    * Networking

## Data Model (Bronze → Silver → Gold)

1. Bronze (Raw). Unmodified, just stored.
    * /solar/raw/yyyy/mm/dd/deviceid_*.json
    * /heatpump/raw/yyyy/mm/dd/*
    * /weather/raw/yyyy/mm/dd/api=owm/*

1. Silver (Cleaned)
    1. Solar (solar_readings):
        * timestamp, pv_watts, grid_import, export_kwh, load_watts, battery_soc…
    1. Heat pump (heatpump_readings):
        * timestamp, flow_temp, return_temp, outside_temp, power_kwh…
    1. Weather (weather_combined):
        * timestamp, temp_api1, temp_api2, temp_api3, temp_mean, solar_radiation…
1. Gold (Modelled)
    1. Daily Energy Balance
        * Solar produced
        * Heat pump consumed
        * Home load vs solar contribution
        * Net export
        * Solar self-consumption %
    2. Heat Pump Efficiency Model
        * COP = thermal output / electrical input
        * Correlate COP vs outside temperature
        * COP vs flow temperature
        * Efficiency heatmap
    3. Home Energy Forecast Model
        * Predict solar generation next day
        * Predict heat pump usage based on weather
        * Forecast grid import/export
    4. Anomaly Detection
        * Identify days where the heat pump consumes more than expected
        * Detect inverter or PV issues
