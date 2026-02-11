# Azure Monitor Implementation – Hands-on CLI Guide

This section documents a practical implementation of **Azure Monitor services using Azure CLI**, including Log Analytics, Application Insights, VM monitoring, availability testing, and alerting.

The content below is designed as a reusable reference for real-world environments.  
No proprietary or assessment-related material is included.

---

## 🔧 Implementation Overview

The following Azure monitoring capabilities were configured using Azure CLI:

- Log Analytics Workspace deployment  
- Application Insights configuration  
- Enabling VM telemetry collection  
- Data Collection Rules (DCR)  
- Web application monitoring  
- Availability testing  
- Action Groups and Alert Rules  

All resources were deployed and configured programmatically using Azure CLI to ensure repeatability and automation.

---

## 🧩 Architecture Components

### Core Services Implemented

| Component | Purpose |
|--------|--------|
| Log Analytics Workspace | Centralized log and telemetry repository |
| Application Insights | Application-level monitoring and diagnostics |
| Azure Monitor Agent | Collects OS and application telemetry from VMs |
| Data Collection Rules | Defines what data is collected from monitored systems |
| Availability Tests | External monitoring of application endpoints |
| Action Groups | Notification and response framework |
| Metric Alerts | Automated alerting based on thresholds |

---

## 📘 Key Concepts

### Log Analytics Workspace
- Central storage location for Azure Monitor logs  
- Used as the backend for:
  - VM monitoring  
  - Application telemetry  
  - Diagnostic logs  
  - Alerting logic  

### Application Insights
- Provides performance and usage monitoring  
- Tracks:
  - HTTP requests  
  - Failures  
  - Response times  
  - Availability  

### Data Collection Rules (DCR)
- Define what logs and metrics are collected from virtual machines  
- Can include:
  - Event logs  
  - IIS logs  
  - Performance counters  

---

## 🚀 What Was Achieved

The implementation successfully demonstrated:

- End-to-end configuration of Azure Monitor using only CLI  
- Monitoring of virtual machines with the Azure Monitor Agent  
- Centralized logging to Log Analytics  
- Application Insights integration  
- Availability monitoring  
- Automated alerting for abnormal conditions  

All configurations were validated using Azure Monitor dashboards and CLI verification commands.

---

## 🛠 Tools Used

- Azure CLI  
- Azure Monitor  
- Log Analytics  
- Application Insights  
- Azure Portal (for verification only)

---

## 💡 Lessons Learned

- Azure CLI enables full automation of monitoring configurations  
- Most monitoring components can be deployed without manual portal interaction  
- Policy restrictions can impact certain monitoring features  
- Availability tests may require organizational permissions  
- Data Collection Rules are central to VM telemetry collection  

---

## 📌 Best Practices Followed

- Infrastructure-as-code approach using CLI  
- Reusable command patterns  
- Minimal manual configuration  
- Centralized logging architecture  
- Role-based access control for monitoring resources  

---

## 📂 Repository Structure

```
microsoft-applied-skills/
└── applied-skills/
    └── azure-monitor/
        ├── README.md
        └── CLI-Commands.md
```

---

## 🔗 References

- Azure Monitor Documentation  
- Azure CLI Reference  
- Log Analytics Overview  
- Application Insights Guide  

---

### Author

Documented and implemented as part of hands-on Azure learning and automation practice.

