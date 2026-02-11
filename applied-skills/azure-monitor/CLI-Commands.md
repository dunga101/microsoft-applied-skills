# Azure Monitor – Reusable CLI Commands

This document contains commonly used Azure CLI commands for deploying and configuring Azure Monitor components.

All commands below are written as reusable templates and can be adapted to any environment.

---

## 1. Log Analytics Workspace

### Create a Log Analytics Workspace

```bash
az monitor log-analytics workspace create \
  --resource-group <RESOURCE_GROUP> \
  --workspace-name <WORKSPACE_NAME> \
  --location <LOCATION>
```

### View Workspace Details

```bash
az monitor log-analytics workspace show \
  --resource-group <RESOURCE_GROUP> \
  --workspace-name <WORKSPACE_NAME>
```

---

## 2. Application Insights

### Create an Application Insights Component

```bash
az monitor app-insights component create \
  --app <APP_INSIGHTS_NAME> \
  --location <LOCATION> \
  --resource-group <RESOURCE_GROUP> \
  --workspace <LOG_ANALYTICS_RESOURCE_ID> \
  --kind web
```

### List Application Insights Components

```bash
az monitor app-insights component show \
  --app <APP_INSIGHTS_NAME> \
  --resource-group <RESOURCE_GROUP>
```

---

## 3. Azure Monitor Agent on Virtual Machines

### Install Azure Monitor Agent on a Windows VM

```bash
az vm extension set \
  --resource-group <RESOURCE_GROUP> \
  --vm-name <VM_NAME> \
  --name AzureMonitorWindowsAgent \
  --publisher Microsoft.Azure.Monitor \
  --version 1.0
```

### Install Azure Monitor Agent on a Linux VM

```bash
az vm extension set \
  --resource-group <RESOURCE_GROUP> \
  --vm-name <VM_NAME> \
  --name AzureMonitorLinuxAgent \
  --publisher Microsoft.Azure.Monitor \
  --version 1.0
```

---

## 4. Data Collection Rules (DCR)

### Create a Data Collection Rule

```bash
az monitor data-collection rule create \
  --resource-group <RESOURCE_GROUP> \
  --name <DCR_NAME> \
  --location <LOCATION> \
  --data-flows '[{"streams": ["Microsoft-Event"], "destinations": ["logAnalytics"]}]' \
  --destinations '{"logAnalytics": [{"workspaceResourceId": "<WORKSPACE_ID>", "name": "logAnalytics"}]}'
```

### Associate a DCR to a Virtual Machine

```bash
az monitor data-collection rule association create \
  --name <ASSOCIATION_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --rule-id <DCR_RESOURCE_ID> \
  --resource <VM_RESOURCE_ID>
```

### List DCR Associations

```bash
az monitor data-collection rule association list \
  --resource <VM_RESOURCE_ID>
```

---

## 5. Application Availability Testing

### Create a Standard Availability Test

```bash
az monitor app-insights web-test create \
  --resource-group <RESOURCE_GROUP> \
  --web-test-name <TEST_NAME> \
  --location <LOCATION> \
  --kind standard \
  --frequency 300 \
  --timeout 30 \
  --component-name <APP_INSIGHTS_NAME> \
  --request-url "http://<TARGET_IP_OR_URL>"
```

### List Existing Availability Tests

```bash
az monitor app-insights web-test list \
  --resource-group <RESOURCE_GROUP> -o table
```

---

## 6. Action Groups for Alerts

### Create an Action Group with Email Notification

```bash
az monitor action-group create \
  --name <ACTION_GROUP_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --short-name <SHORT_NAME> \
  --action email <RECEIVER_NAME> <EMAIL_ADDRESS>
```

### List Action Groups

```bash
az monitor action-group list \
  --resource-group <RESOURCE_GROUP> -o table
```

---

## 7. Metric-Based Alerts

### Create a CPU Usage Alert Rule

```bash
az monitor metrics alert create \
  --name <ALERT_NAME> \
  --resource-group <RESOURCE_GROUP> \
  --scopes <RESOURCE_ID> \
  --condition "avg Percentage CPU > 80" \
  --window-size 5m \
  --evaluation-frequency 1m \
  --action <ACTION_GROUP_RESOURCE_ID>
```

### View Existing Alerts

```bash
az monitor metrics alert list \
  --resource-group <RESOURCE_GROUP> -o table
```

---

## 8. Diagnostics Settings

### Enable Diagnostics for a Resource

```bash
az monitor diagnostic-settings create \
  --name <SETTING_NAME> \
  --resource <RESOURCE_ID> \
  --workspace <LOG_ANALYTICS_RESOURCE_ID> \
  --logs '[{"category": "AuditLogs","enabled": true}]'
```

### List Diagnostics Settings

```bash
az monitor diagnostic-settings list \
  --resource <RESOURCE_ID>
```

---

## 9. Useful Discovery Commands

### Get VM Public IP Address

```bash
az vm show \
  --resource-group <RESOURCE_GROUP> \
  --name <VM_NAME> \
  -d --query publicIps -o tsv
```

### Show All Monitor Components in a Resource Group

```bash
az resource list \
  --resource-group <RESOURCE_GROUP> \
  --query "[?type=='Microsoft.Insights/components']"
```

---

## Notes

- Replace placeholders like `<RESOURCE_GROUP>` with your actual values.
- Most commands can be automated via scripts or pipelines.
- Use `az login` and `az account set` to select the correct subscription before running commands.

---

## References

- Azure CLI Documentation  
- Azure Monitor CLI Reference  
- Log Analytics CLI Commands  

---

### Purpose

This command set serves as a reusable reference for deploying and managing Azure Monitor resources using infrastructure-as-code principles.

