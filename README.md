# Real-Time Weather Streaming Pipeline — Azure

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Microsoft Fabric](https://img.shields.io/badge/Microsoft_Fabric-742774?style=for-the-badge&logo=microsoft&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

---

## What I Built

A production-style real-time streaming data pipeline on Azure — end to end, from a live Weather API all the way to a live Power BI dashboard with automated alerts.

I set up two independent ingestion paths (Databricks PySpark and Azure Functions), both publishing events into Azure Event Hubs. From there, Microsoft Fabric Eventstream routes the data into Eventhouse (Kusto), where I query it with KQL. The final layer is a live Power BI dashboard that updates in real time, with Data Activator firing alerts on threshold conditions.

Everything is wired through Azure Key Vault for secrets — no hardcoded credentials anywhere in the codebase.

---

## Architecture

```
  Live Weather API
        │
        ├─────────────────────────┐
        ▼                         ▼
  Databricks (PySpark)     Azure Functions
        │                         │
        └──────────┬──────────────┘
                   ▼
           Azure Event Hubs
                   │
                   ▼
        Microsoft Fabric Eventstream
                   │
                   ▼
          Eventhouse (KQL/Kusto)
                   │
                   ▼
        Power BI Live Dashboard
                   │
                   ▼
           Data Activator (Alerts)
```

---

## Stack

| Layer | Service |
|---|---|
| Data Source | Free Weather API |
| Ingestion | Azure Databricks (PySpark) + Azure Functions |
| Messaging | Azure Event Hubs |
| Stream Processing | Microsoft Fabric Eventstream |
| Storage & Analytics | Eventhouse (Kusto) |
| Visualization | Power BI |
| Alerting | Data Activator |
| Secrets | Azure Key Vault |

---

## Project Structure

```
azure-realtime-weather-pipeline/
│
├── ingestion/
│   ├── databricks/
│   │   └── weather-streaming-notebook.ipynb        # PySpark streaming job
│   │
│   └── azure_functions/
│       ├── function_app.py                         # Streaming
│       ├── host.json
│       └── requirements.txt
│
├── kql/
│   ├── weather_eventhouse_queryset.kql         # Analysis queries
│   └── for_alerts.kql                          # Queries powering Data Activator
│
├── architecture/
│   └── architecture-diagram.png
│
├── visualization/
│   └── Weather-Report.pbix          # PowerBI Report
│
└── README.md
```

---

## Setup

### Prerequisites
- Azure subscription
- Python 3.9+
- Azure CLI
- Azure Functions Core Tools v4
- Microsoft Fabric workspace
- Free Weather API key

### Clone & Install

```bash
git clone https://github.com/<your-username>/azure-realtime-weather-pipeline.git
cd azure-realtime-weather-pipeline
pip install -r requirements.txt
```

### Environment Variables

```bash
cp .env.example .env
```

```env
WEATHER_API_KEY=your_key_here
EVENT_HUB_CONNECTION_STRING=your_connection_string
EVENT_HUB_NAME=evh-weather-events
KEY_VAULT_NAME=kv-weather-pipeline
CITIES=London,New York,Tokyo,Mumbai,Sydney
```

### Run Databricks Ingestion

Upload `ingestion/databricks/weather_ingest.py` to your Databricks workspace and attach it to a running cluster.

### Run Azure Functions Locally

```bash
cd ingestion/azure_functions
func start
```

---

## KQL — Sample Queries

```kql
// Average temperature by city — last hour
WeatherEvents
| where ingestion_time > ago(1h)
| summarize avg_temp = avg(temperature), avg_humidity = avg(humidity) by city
| order by avg_temp desc

// High temperature alerts
WeatherEvents
| where ingestion_time > ago(15m)
| where temperature > 35
| project city, temperature, ingestion_time
```

---

## Alerts (Data Activator)

| Trigger | Condition | Notification |
|---|---|---|
| High Temperature | > 35°C | Email |
| Low Humidity | < 20% | Teams message |
| Strong Winds | > 50 km/h | Email + Teams |

---

## End-to-End Test

```bash
python tests/e2e_pipeline_test.py
```

```
✅ Weather API: Connected
✅ Event Hubs: Events published
✅ Eventstream: Routed to Eventhouse
✅ Eventhouse: Rows ingested
✅ Power BI: Dataset refreshed
```

---

## License

MIT