# Azure Monitor – Reusable Azure CLI Commands

The following commands are generic patterns used for Azure monitoring deployments.

# Create a Log Analytics Workspace
az monitor log-analytics workspace create \
  --resource-group <ResourceGroup> \
  --workspace-name <WorkspaceName> \
  --location <AzureRegion>

#Install Azure Monitor Agent on a VM
az vm extension set \
  --resource-group <ResourceGroup> \
  --vm-name <VMName> \
  --name AzureMonitorWindowsAgent \
  --publisher Microsoft.Azure.Monitor \
  --version 1.0

#Create a Data Collection Rule (DCR)
az monitor data-collection rule create \
  --resource-group <ResourceGroup> \
  --location <AzureRegion> \
  --name <DCR-Name> \
  --workspace-name <WorkspaceName>

#Associate DCR with a Virtual Machine
az monitor data-collection rule association create \
  --name <AssociationName> \
  --resource-group <ResourceGroup> \
  --rule-id <DCR-Resource-ID> \
  --resource $(az vm show -g <ResourceGroup> -n <VMName> --query id -o tsv)

#Retrieve Public IP of a Virtual Machine
az vm show \
  --resource-group <ResourceGroup> \
  --name <VMName> \
  --show-details \
  --query publicIps \
  --output tsv

#Create an Action Group for Alerts
az monitor action-group create \
  --name <ActionGroupName> \
  --resource-group <ResourceGroup> \
  --short-name <ShortName> \
  --email-receiver alerts user@example.com

#Configure a Metric Alert
az monitor metrics alert create \
  --name <AlertName> \
  --resource-group <ResourceGroup> \
  --scopes <ResourceID> \
  --condition "avg Percentage CPU > 80" \
  --window-size 5m \
  --evaluation-frequency 1m \
  --action <ActionGroupName> \
  --severity 2

#Validation Commands
az monitor action-group list -g <ResourceGroup> -o table
az monitor metrics alert list -g <ResourceGroup> -o table
az monitor data-collection rule list -g <ResourceGroup> -o table
