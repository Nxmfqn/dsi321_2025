# Project DSI321: Real-Time Data Pipeline with Visualization

## Bangkok Air Quality Dashboard with Streamlit, Prefect & LakeFS

![Created at](https://img.shields.io/github/created-at/Nxmfqn/dsi321_2025?color=3CB371\&labelColor=2E8B57\&label=Created%20at)
![Last Commit](https://img.shields.io/github/last-commit/Nxmfqn/dsi321_2025?color=20B2AA\&labelColor=006A6A\&label=Last%20commit)

---

## 🌆 Overview

This project, built for **DSI321: Big Data Infrastructure**, monitors **Bangkok's air quality in near real-time** using hourly PM2.5 and AQI data from Air4Thai. It also **forecasts pollution 6 hours ahead** with ARIMA, helping support public health and city planning.

All components run in Docker for consistency and reproducibility.

---

## ⚙️ Tech Stack Summary

| Layer                 | Tools                          |
| --------------------- | ------------------------------ |
| **Orchestration**     | Prefect                        |
| **Containerization**  | Docker                         |
| **Data Versioning**   | LakeFS                         |
| **Visualization**     | Streamlit                      |
| **Forecasting Model** | ARIMA                          |
| **Notebook IDE**      | JupyterLab                     |
| **Data Source**       | [Air4Thai PM2.5 API](http://air4thai.pcd.go.th/services/getNewAQI_JSON.php)|

## 🌟 Key Features

* Live AQI/PM2.5 updates from Bangkok stations
* 6-hour forecasting per station using ARIMA
* Interactive dashboard with maps, charts, and tables
* Automated flows using Prefect
* Versioned data with LakeFS
* Fully containerized with Docker

---

## 🗂️ Data Schema (processed for dashboard)

| Column        | Type     | Description               |
| ------------- | -------- | ------------------------- |
| `timestamp`   | datetime | Measurement time          |
| `stationID`   | string   | Station code              |
| `nameTH`      | string   | Station name (Thai)       |
| `areaTH`      | string   | Area name (Thai)          |
| `district`    | string   | Bangkok district name     |
| `lat`, `long` | float    | Coordinates               |
| `AQI.aqi`     | int      | Air Quality Index (0–500) |
| `PM25.value`  | float    | PM2.5 (µg/m³)             |

---

## ✅ Data Quality Checks

* ✅ 1,000+ records across stations
* ✅ 24+ hourly records per station
* ✅ ≥90% completeness
* ✅ No duplicated rows or object-type columns

📘 [View full QA notebook](data/check_data_quality.ipynb)

---

## 🚀 Quick Start

### 1. Clone the Repo

```bash
git clone https://github.com/Nxmfqn/dsi321_2025.git
cd dsi321_2025
```

### 2. Start All Services

```bash
docker-compose up --build -d
```

### 3. Access Local Services

| Service    | URL                                            |
| ---------- | ---------------------------------------------- |
| LakeFS     | [http://localhost:8001](http://localhost:8001) |
| JupyterLab | [http://localhost:8888](http://localhost:8888) |
| Prefect    | [http://localhost:4200](http://localhost:4200) |
| Streamlit  | [http://localhost:8502](http://localhost:8502) |

💡 Login for LakeFS:
`access_key` / `secret_key`

Then, create the LakeFS repo:

```bash
lakectl repo create lakefs://dust-concentration
```

---

## 🧾 Upload & Forecast (First-Time Setup)

### Upload Initial Data

```bash
docker exec -it dsi321-jupyter-1 bash
python upload.py
```

### Run Forecast Scripts

```bash
python pipeline/getdata.py
python pipeline/forecasting.py
```

or trigger via **Prefect UI** at [http://localhost:4200](http://localhost:4200)

---

## ⏰ Automate with Prefect

Schedule flows to run every hour:

```bash
# Ingest data (runs at :25)
python deploy.py

# Forecast data (runs at :27)
python deploy_ml.py
```

---

## 📊 Dashboard Overview

![Dashboard Demo](img/dashboard_demo.png)

* 🔍 Select stations and view real-time AQI/PM2.5
* 📈 Line charts for top polluted stations
* 🌍 AQI map of Bangkok with color-coded bubbles
* 📊 Forecast and data tables for all stations

---

## 🔮 Forecasting Details

* **Model**: ARIMA(1,0,1) per station
* **Target**: PM2.5 (float) & AQI (int)
* **Stored at**: `lakefs://dust-concentration/main/forecast/forecast.parquet`
* **Forecast horizon**: Next 6 hours
* **Excludes**: Incomplete or flat-line stations

---

## 📁 Repo Structure

```
.
├── data/              # Parquet files, schema, QA notebook
├── pipeline/          # Ingestion, ARIMA, and Prefect flows
├── visualization/     # Streamlit dashboard
├── prefect/           # Dockerfiles & configs for services
├── docker-compose.yml # Compose setup
└── README.md          # This file
```

