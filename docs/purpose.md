# Purpose of the SmartHome Project

## Sunsynk + Mitsubishi + Weather APIs

Data Collected (Daily or Hourly)

1. Solar / Sunsynk Inverter Data
    * PV production (W / Wh)
    * PV strings (PV1, PV2)
    * Grid import/export (kWh)
    * Load consumption
    * Battery SoC (if you have one)
    * Battery charge/discharge (kWh)
    * Inverter temperature
    * Export to grid (kWh)
    * Solar self-consumption % (computed)
    * System alerts
2. Heat Pump / Mitsubishi Data
    * Depending on your access:
    * Heat pump power consumption (kWh)
    * Flow temperature
    * Return temperature
    * Room temps (zones)
    * Outside air temperature (from heat pump or weather)
    * Compressor frequency / status
    * COP (Coefficient of Performance) – you can calculate this!
3. Weather Data (External APIs)
    * Pull from 2–3 APIs (e.g. OpenWeather, Met Office, Tomorrow.io):
    * Outside temperature
    * Feels-like temperature
    * Humidity
    * Solar irradiation / cloud cover
    * Wind speed
    * Rainfall
