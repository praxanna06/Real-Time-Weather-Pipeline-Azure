# ⚡ Real-Time Streaming Data Pipeline on Azure
### Live Weather API → Databricks / Azure Functions → Event Hubs → Microsoft Fabric → Power BI

![Azure](https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white)
![Databricks](https://img.shields.io/badge/Databricks-FF3621?style=for-the-badge&logo=databricks&logoColor=white)
![Microsoft Fabric](https://img.shields.io/badge/Microsoft_Fabric-742774?style=for-the-badge&logo=microsoft&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![PySpark](https://img.shields.io/badge/PySpark-E25A1C?style=for-the-badge&logo=apachespark&logoColor=white)
![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)

---

## 📌 Project Overview

A **production-style, end-to-end real-time streaming data pipeline** built on Azure. This project ingests live weather events via two independent paths — **Databricks PySpark** and **Azure Functions** — publishes them to **Azure Event Hubs**, processes streams with **Microsoft Fabric Eventstream**, persists data in **Eventhouse (Kusto/KQL)**, and delivers live insights through **Power BI dashboards** with automated alerts via **Data Activator**.

```
┌─────────────────────────────────────────────────────────────────────────────┐
│                     REAL-TIME STREAMING PIPELINE ARCHITECTURE               │
└─────────────────────────────────────────────────────────────────────────────┘

  [Live Weather API]
        │
        ├────────────────────────────────────┐
        ▼                                    ▼
 ┌─────────────┐                    ┌─────────────────┐
 │  Databricks │                    │  Azure Functions│
 │  (PySpark)  │                    │  (Serverless)   │
 └──────┬──────┘                    └────────┬────────┘
        │                                    │
        └──────────────┬─────────────────────┘
                       ▼
              ┌─────────────────┐
              │  Azure Event    │
              │  Hubs (Ingest)  │
              └────────┬────────┘
                       ▼
              ┌─────────────────┐
              │  Microsoft      │
              │  Fabric         │
              │  Eventstream    │
              └────────┬────────┘
                       ▼
              ┌─────────────────┐
              │  Eventhouse     │
              │  (Kusto / KQL)  │
              └────────┬────────┘
                       ▼
              ┌─────────────────┐      ┌──────────────────┐
              │  Power BI Live  │─────▶│  Data Activator  │
              │  Dashboard      │      │  (Alerts)        │
              └─────────────────┘      └──────────────────┘
```

---

## 🎯 What You'll Learn

- ✅ Design a **secure, scalable streaming architecture** on Azure
- ✅ Implement **dual-path ingestion** with Databricks (PySpark) and Azure Functions
- ✅ Stream events into **Event Hubs** and route with **Fabric Eventstream**
- ✅ Load and query data in **Eventhouse** using KQL
- ✅ Build **live Power BI dashboards** with real-time refresh
- ✅ Trigger automated alerts using **Data Activator**
- ✅ Monitor, troubleshoot, and **optimize for cost and performance**
- ✅ Perform full **end-to-end pipeline testing**

---

## 🏗️ Architecture Components

| Layer | Service | Purpose |
|---|---|---|
| **Data Source** | OpenWeatherMap API | Live weather event feed |
| **Ingestion Path 1** | Azure Databricks (PySpark) | Scalable batch/micro-batch ingest |
| **Ingestion Path 2** | Azure Functions | Lightweight serverless ingest |
| **Message Broker** | Azure Event Hubs | Durable event streaming (Kafka-compatible) |
| **Stream Processing** | Microsoft Fabric Eventstream | Real-time routing and transformation |
| **Storage & Query** | Eventhouse (Kusto) | High-speed time-series storage + KQL |
| **Visualization** | Power BI | Live dashboards |
| **Alerting** | Data Activator | Threshold-based real-time alerts |
| **Secrets** | Azure Key Vault | Secure credential management |

---

## 📁 Repository Structure

```
azure-realtime-weather-pipeline/
│
├── 📂 infra/                          # Infrastructure provisioning
│   ├── resource_group.md              # Resource group setup guide
│   ├── event_hubs_setup.md            # Event Hubs namespace & hub config
│   ├── key_vault_setup.md             # Key Vault + secrets config
│   └── databricks_workspace.md        # Databricks workspace & cluster setup
│
├── 📂 ingestion/
│   ├── 📂 databricks/                 # PySpark ingestion path
│   │   ├── weather_ingest.py          # Main PySpark streaming job
│   │   ├── event_hub_writer.py        # Event Hubs publisher utility
│   │   └── config.py                  # Config loader (reads from Key Vault)
│   │
│   └── 📂 azure_functions/            # Serverless ingestion path
│       ├── WeatherFetchFunction/
│       │   ├── __init__.py            # Timer-triggered Azure Function
│       │   └── function.json          # Trigger binding config
│       ├── host.json
│       └── requirements.txt
│
├── 📂 fabric/                         # Microsoft Fabric configuration
│   ├── eventstream_config.md          # Eventstream routing setup
│   └── eventhouse_tables.kql          # KQL table schemas & ingestion mappings
│
├── 📂 kql/                            # KQL queries for analysis
│   ├── create_tables.kql              # Table and schema definitions
│   ├── realtime_queries.kql           # Live analysis queries
│   └── alerts_queries.kql             # Queries used in Data Activator
│
├── 📂 powerbi/                        # Power BI assets
│   ├── dashboard_setup.md             # Step-by-step dashboard guide
│   └── data_activator_alerts.md       # Alert configuration guide
│
├── 📂 docs/                           # Project documentation
│   ├── architecture_diagram.png       # Full architecture visual
│   ├── setup_guide.md                 # End-to-end setup walkthrough
│   ├── cost_optimization.md           # Cost-saving tips & TU sizing
│   └── troubleshooting.md             # Common issues & fixes
│
├── 📂 tests/                          # End-to-end test scripts
│   ├── e2e_pipeline_test.py           # Full pipeline smoke test
│   └── event_hub_validator.py         # Verify events are arriving
│
├── .gitignore
├── requirements.txt
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites

- Azure subscription (Pay-as-you-go or Student)
- Python 3.9+
- Azure CLI installed → [Install guide](https://learn.microsoft.com/en-us/cli/azure/install-azure-cli)
- Azure Functions Core Tools → `npm install -g azure-functions-core-tools@4`
- Microsoft Fabric workspace (free trial available)
- OpenWeatherMap API key → [Get free key](https://openweathermap.org/api)

---

### 1. Clone the Repository

```bash
git clone https://github.com/<your-username>/azure-realtime-weather-pipeline.git
cd azure-realtime-weather-pipeline
```

### 2. Provision Azure Infrastructure

```bash
# Login to Azure
az login

# Create Resource Group
az group create --name rg-weather-pipeline --location eastus

# Create Event Hubs Namespace (Basic tier for dev, Standard for prod)
az eventhubs namespace create \
  --name evhns-weather-pipeline \
  --resource-group rg-weather-pipeline \
  --sku Standard \
  --location eastus

# Create Event Hub
az eventhubs eventhub create \
  --name evh-weather-events \
  --namespace-name evhns-weather-pipeline \
  --resource-group rg-weather-pipeline \
  --message-retention 1 \
  --partition-count 4

# Create Key Vault
az keyvault create \
  --name kv-weather-pipeline \
  --resource-group rg-weather-pipeline \
  --location eastus
```

### 3. Store Secrets in Key Vault

```bash
# Store Event Hubs connection string
az keyvault secret set \
  --vault-name kv-weather-pipeline \
  --name "EventHubConnectionString" \
  --value "<your-event-hub-connection-string>"

# Store Weather API key
az keyvault secret set \
  --vault-name kv-weather-pipeline \
  --name "WeatherApiKey" \
  --value "<your-openweathermap-api-key>"
```

### 4. Set Up Databricks Workspace

1. Create Databricks workspace in the Azure Portal under your resource group
2. Launch the workspace and create a cluster:
   - **Runtime**: 13.3 LTS (Spark 3.4.1, Scala 2.12)
   - **Node type**: `Standard_DS3_v2` (cost-efficient for dev)
   - **Auto-termination**: 30 minutes
3. Install required libraries on the cluster:
   - `azure-eventhub`
   - `requests`

### 5. Install Python Dependencies

```bash
pip install -r requirements.txt
```

### 6. Configure Environment Variables

```bash
cp .env.example .env
# Edit .env with your values
```

```env
WEATHER_API_KEY=your_openweathermap_api_key
EVENT_HUB_CONNECTION_STRING=your_event_hub_connection_string
EVENT_HUB_NAME=evh-weather-events
KEY_VAULT_NAME=kv-weather-pipeline
CITIES=London,New York,Tokyo,Mumbai,Sydney
```

---

## 🔄 Running the Pipeline

### Path 1: Databricks PySpark Ingestion

Upload `ingestion/databricks/weather_ingest.py` to your Databricks workspace and run it on your cluster:

```python
# weather_ingest.py — snippet
from azure.eventhub import EventHubProducerClient, EventData
import requests, json, time

def fetch_weather(city, api_key):
    url = f"https://api.openweathermap.org/data/2.5/weather?q={city}&appid={api_key}&units=metric"
    return requests.get(url).json()

def publish_to_event_hub(data, connection_str, hub_name):
    producer = EventHubProducerClient.from_connection_string(connection_str, eventhub_name=hub_name)
    with producer:
        batch = producer.create_batch()
        batch.add(EventData(json.dumps(data)))
        producer.send_batch(batch)
```

### Path 2: Azure Functions Ingestion

```bash
cd ingestion/azure_functions
func start  # Local dev
# OR deploy to Azure:
func azure functionapp publish <your-function-app-name>
```

---

## 🗄️ KQL — Eventhouse Queries

```kql
// Create the raw weather table
.create table WeatherEvents (
    city: string,
    temperature: real,
    humidity: int,
    wind_speed: real,
    description: string,
    ingestion_time: datetime
)

// Real-time average temperature by city (last 1 hour)
WeatherEvents
| where ingestion_time > ago(1h)
| summarize avg_temp = avg(temperature), avg_humidity = avg(humidity)
    by city
| order by avg_temp desc

// Detect temperature spikes (> 35°C)
WeatherEvents
| where ingestion_time > ago(15m)
| where temperature > 35
| project city, temperature, ingestion_time
| order by temperature desc
```

---

## 📊 Power BI Dashboard Setup

1. Open Power BI Desktop → **Get Data** → **Microsoft Fabric** → **Eventhouse (KQL)**
2. Connect to your Eventhouse database and import the `WeatherEvents` table
3. Set **Auto-refresh** to 1–5 minutes (DirectQuery mode)
4. Build visuals:
   - 🌡️ Real-time temperature map (filled map)
   - 💧 Humidity trend line chart (last 24h)
   - 🌬️ Wind speed gauge by city
   - 🔔 Alert table for high-temperature cities
5. Publish to Power BI Service and pin to a Live Dashboard

---

## 🔔 Data Activator Alerts

In Microsoft Fabric → Data Activator, create a reflex on the `WeatherEvents` stream:

| Alert | Condition | Action |
|---|---|---|
| High Temperature | `temperature > 35°C` | Send email notification |
| Low Humidity | `humidity < 20%` | Teams message |
| Strong Winds | `wind_speed > 50 km/h` | Email + Teams |

---

## 💰 Cost Optimization Tips

| Resource | Dev/Test Setting | Production Setting |
|---|---|---|
| Event Hubs | Basic tier, 1 TU | Standard tier, auto-inflate |
| Databricks | `Standard_DS3_v2`, auto-terminate 30min | Job clusters (not all-purpose) |
| Azure Functions | Consumption plan | Premium plan for VNET |
| Eventhouse | Free Fabric capacity (F2) | F4–F8 based on query load |
| Power BI | Pro license | Premium Per User for sharing |

> 💡 **Tip**: Use Databricks **job clusters** instead of all-purpose clusters in production — they spin up only when a job runs and auto-terminate, reducing costs by 60–80%.

---

## 🧪 End-to-End Testing

```bash
# Run the full pipeline smoke test
python tests/e2e_pipeline_test.py

# Validate events are arriving at Event Hubs
python tests/event_hub_validator.py --hub evh-weather-events --duration 60
```

Expected output:
```
✅ Weather API: Connected (200 OK)
✅ Event Hubs: 5 events published successfully
✅ Eventstream: Events routed to Eventhouse
✅ Eventhouse: 5 rows ingested in WeatherEvents table
✅ Power BI: Dataset refreshed (last refresh: <timestamp>)
```

---

## 🛠️ Troubleshooting

| Issue | Likely Cause | Fix |
|---|---|---|
| Events not reaching Event Hubs | Wrong connection string | Verify in Key Vault; check SAS policy has `Send` permission |
| Eventstream not ingesting | Consumer group conflict | Create a dedicated consumer group for Fabric |
| KQL table empty | Ingestion mapping mismatch | Check column names match JSON payload keys |
| Power BI not refreshing | DirectQuery timeout | Increase query timeout; optimize KQL with `summarize` |
| Azure Function not triggering | Timer CRON syntax error | Validate CRON in `function.json` (6-part Azure format) |

---

## 📚 Resources

- [Azure Event Hubs Documentation](https://learn.microsoft.com/en-us/azure/event-hubs/)
- [Microsoft Fabric Eventstream](https://learn.microsoft.com/en-us/fabric/real-time-intelligence/event-streams/overview)
- [KQL Quick Reference](https://learn.microsoft.com/en-us/azure/data-explorer/kql-quick-reference)
- [Databricks PySpark Structured Streaming](https://docs.databricks.com/en/structured-streaming/index.html)
- [Data Activator in Microsoft Fabric](https://learn.microsoft.com/en-us/fabric/data-activator/data-activator-introduction)
- [OpenWeatherMap API Docs](https://openweathermap.org/api)

---

## 🤝 Contributing

Contributions are welcome! Please open an issue first to discuss proposed changes.

```bash
# Fork → Clone → Branch → PR
git checkout -b feature/your-feature-name
git commit -m "feat: add your feature"
git push origin feature/your-feature-name
```

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Author

Built with ❤️ as a hands-on Azure Data Engineering portfolio project.

> ⭐ **If this project helped you, please give it a star on GitHub!**