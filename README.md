# Project DSI321: Real-Time Data Pipeline with Visualization

## Bangkok Air Quality Dashboard with Streamlit, Prefect & LakeFS

![Created at](https://img.shields.io/github/created-at/Nxmfqn/dsi321_2025?color=3CB371&labelColor=2E8B57&label=Created%20at)
![Last Commit](https://img.shields.io/github/last-commit/Nxmfqn/dsi321_2025?color=20B2AA&labelColor=006A6A&label=Last%20commit)

## Project Overview

This project is part of the **DSI321: Big Data Infrastructure** course. We built a **near real-time air quality monitoring system for Bangkok** using hourly data on PM2.5 and AQI from the **Air4Thai API**. Our system not only shows current air pollution levels but also **predicts air quality for the next 6 hours**, which can help with public health decisions, city planning, and environmental research.

We used modern tools to build a reliable and scalable data pipeline:

* **Prefect** – to manage and schedule data workflows
* **LakeFS** – to keep track of changes in the data (data versioning)
* **Streamlit** – to create an easy-to-use dashboard for data visualization
* **Docker** – to package everything for consistent and simple deployment
* **ARIMA** – a time-series model used to forecast future air quality

All parts of the system run inside Docker containers to make it easy to deploy and reproduce anywhere.



