# 🌦️ Real-Time Weather Streaming Pipeline on Azure

## 📌 Overview
This project demonstrates a **production-style real-time data engineering pipeline** built on Azure. It ingests live weather data from an external API, streams it through an event-driven architecture, processes it in real time, and visualizes insights using live dashboards with alerting.

The pipeline is designed to be **scalable, secure, and cost-efficient**, mimicking real-world enterprise data platforms.

---

## 🏗️ Architecture


Weather API
│
├── Azure Databricks (PySpark)
├── Azure Functions
│
▼
Azure Event Hubs
▼
Microsoft Fabric Eventstream
▼
Eventhouse (Kusto DB)
▼
Power BI Dashboard + Data Activator Alerts


---

## 🚀 Tech Stack

- Microsoft Azure (Cloud Platform)
- Azure Databricks (PySpark)
- Azure Event Hubs (Streaming ingestion)
- Microsoft Fabric (Eventstream)
- Azure Functions (Serverless ingestion)
- Azure Key Vault (Secrets management)
- Eventhouse (Kusto Database)
- Power BI (Visualization & dashboards)
- Python
- KQL (Kusto Query Language)

---

## ⚙️ Key Features

✅ Real-time data ingestion from Weather API  
✅ Dual ingestion paths:
- Azure Databricks (PySpark streaming)
- Azure Functions (event-driven)

✅ Event-driven architecture using Event Hubs  
✅ Stream processing with Microsoft Fabric Eventstream  
✅ Fast querying using Kusto (Eventhouse)  
✅ Live dashboards in Power BI  
✅ Real-time alerts using Data Activator  
✅ Secure secret management via Key Vault  
✅ Cost optimization strategies applied  

---

## 🔐 Security

- Secrets stored in Azure Key Vault  
- No hardcoded credentials  
- Role-based access control (RBAC)  
- Secure service-to-service communication  

---

## 📂 Project Structure


real-time-weather-pipeline-azure/
│
├── ingestion/
│ ├── databricks/
│ │ └── weather_stream.py
│ └── azure_functions/
│ └── function_app.py
│
├── streaming/
│ └── eventhub_config.json
│
├── processing/
│ └── fabric_eventstream_setup.md
│
├── storage/
│ └── kusto_queries.kql
│
├── visualization/
│ └── dashboard_screenshots/
│
├── config/
│ └── .env.example
│
├── architecture/
│ └── architecture-diagram.png
│
└── docs/
├── setup_guide.md
└── troubleshooting.md


---

## 🛠️ Setup Guide

### 1️⃣ Create Azure Resources
- Resource Group  
- Azure Databricks Workspace & Cluster  
- Event Hubs Namespace & Hub  
- Azure Key Vault  
- Microsoft Fabric Workspace  

---

### 2️⃣ Configure Key Vault
Store:
- Weather API Key  
- Event Hub Connection String  

---

### 3️⃣ Setup Data Ingestion

#### Option A: Databricks (PySpark)
- Run streaming job to fetch API data
- Push events to Event Hub  

#### Option B: Azure Functions
- Timer-trigger or HTTP-trigger function  
- Sends events to Event Hub  

---

### 4️⃣ Configure Event Streaming
- Connect Event Hub to Fabric Eventstream  
- Apply transformations if needed  

---

### 5️⃣ Store Data in Eventhouse
- Create database and table  
- Ingest streaming data  

---

### 6️⃣ Query with KQL
Example:

```kql
WeatherData
| where Temperature > 30
| summarize avg(Temperature) by City
7️⃣ Build Dashboard
Connect Power BI to Eventhouse
Create real-time visuals
Configure Data Activator alerts
📊 Sample Outputs
📈 Live temperature trends
🌍 City-wise weather analytics
🚨 Real-time alerts for extreme conditions

(Add screenshots in /visualization folder)

📈 Monitoring & Optimization
Event Hub Throughput Units tuning
Databricks cluster autoscaling
Query optimization using KQL
Logging & retry mechanisms
⚠️ Challenges & Learnings
Handling real-time streaming latency
Managing schema evolution
Optimizing ingestion throughput
Cost-performance trade-offs
Designing fault-tolerant pipelines
🔮 Future Improvements
Add CI/CD using GitHub Actions
Infrastructure as Code (Terraform/Bicep)
Data quality validation layer
Multi-region deployment
Streaming anomaly detection
👨‍💻 Author

Your Name
GitHub: https://github.com/yourusername