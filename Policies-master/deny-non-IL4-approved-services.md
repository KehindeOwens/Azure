# Deny Non-IL4 Approved Services

This Azure Policy definition prevents changes the provisioning of services that aren't Impact level 4 (IL4) approved.  This is accomplished by allowing creation privileges on services and sub-services that have met the requirements of the US Federal Risk & Authorization Management Program (FedRAMP) as well as the Department of Defense. All other Azure services and features not approved have been excluded from the creation list and validation of the service will fail if a creation attempt occurs.

For a full list of current resource provider operations, you can do one of the following:

## Website

Navigate to the [Azure Resource Manager resource provider operations](https://docs.microsoft.com/en-us/azure/role-based-access-control/resource-provider-operations) website.

## Azure CLI

1. Install the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
2. Run the command `az login` to authenticate to your Azure account.
3. Run the command `az provider operation list -o tsv` to get all current resource provider operations.
    * You can filter this output by using `show` instead of `list` and adding a `--namespace` flag followed by a base namespace i.e. `Microsoft.OperationInsights` or `Microsoft.OperationsManagement`.
    * You can format this differently by changing the `--output | -o` flag to json, jsonc, table, tsv, or yaml.  Using tsv will allow for an easy import into a spreadsheet.

## Azure Powershell

1. Install the [Az Powershell Module](https://docs.microsoft.com/en-us/powershell/azure/install-az-ps?view=azps-3.6.1)
2. Run the command `Connect-AzAccount` to authenticate your Azure account.
3. Run the command `Get-AzProviderOperation` to get all current resource provider operations.
    * You can filter this output with wildcards on any portion of the provider namespace i.e. `*operation*` or `*/workspaces/*`
    * You can format this output by piping to your preferred formatting method i.e. `| Format-Table` or `| Out-GridView`.

## DOD SRG References
   
To read more about the Center for Internet Security as well as CIS Hardened Images in Azure please use these links:


[Department of Defense (DoD) in Azure Government](https://docs.microsoft.com/en-us/azure/azure-government/documentation-government-overview-dod)
/
[DOD Approved Services - IL4 & IL5](https://docs.microsoft.com/en-us/microsoft-365/compliance/offering-cis-benchmark?view=o365-worldwide)


---


## Policy Definition

```json
{
  "mode": "All",
  "policyRule": {
    "if": {
      "not": {
        "field": "type",
        "in": [
          "Microsoft.ApiManagement/service",
          "Microsoft.Automation/automationAccounts",
          "Microsoft.AAD/domainServices",
          "Microsoft.AzureActiveDirectory/",
          "Microsoft.Batch/batchAccounts",
          "Microsoft.Advisor/",
          "Microsoft.AnalysisServices/servers",
          "Microsoft.Blueprint/blueprints",
          "Microsoft.Blueprint/blueprintAssignments",
          "Microsoft.BotService/botServices",
          "Microsoft.BotService/enterpriseChannels",
          "Microsoft.Cache/Redis",
          "Microsoft.ClassicCompute/domainNames",
          "Microsoft.CloudService/",
          "Microsoft.Compute/availabilitySets",
          "Microsoft.Compute/disks",
          "Microsoft.Compute/virtualMachines",
          "Microsoft.Compute/virtualMachines/extensions",
          "Microsoft.Compute/virtualMachineScaleSets",
          "Microsoft.ContainerRegistry/registries",
          "Microsoft.ContainerInstance/containerGroups",
          "Microsoft.ContainerService/",
          "Microsoft.ContainerService/managedClusters",
          "Microsoft.CostManagement/",
          "Microsoft.CostManagementExports/",
          "Microsoft.CognitiveServices/accounts",
          "Microsoft.DataBoxEdge/",
          "Microsoft.DataFactory/factories",
          "Microsoft.DataExplorer/",
          "Microsoft.DataLakeStore/",
          "Microsoft.DataMigration/services",
          "Microsoft.DataLakeStore/accounts",
          "Microsoft.DBforMariaDB/servers",
          "Microsoft.DBforMySQL/servers",
          "Microsoft.DBforPostgreSQL/servers",
          "Microsoft.Devices/",
          "Microsoft.DevTestLab/labs",
          "Microsoft.DevTestLab/schedules",
          "Microsoft.DocumentDB/databaseAccounts",
          "Microsoft.EventHub/namespaces",
          "Microsoft.EventGrid/domains",
          "Microsoft.EventGrid/topics",
          "Microsoft.HardwareSecurityModules/dedicatedhsms",
          "Microsoft.HDInsight/clusters",
          "Microsoft.InformationProtection/",
          "Microsoft.Insights/",
          "Microsoft.Intune/",
          "Microsoft.ImportExport/jobs",
          "Microsoft.KeyVault/vaults",
          "Microsoft.Kubernetes/",
          "Microsoft.KubernetesConfiguration/",
          "Microsoft.LabServices/labaccounts",
          "Microsoft.Logic/integrationAccounts",
          "Microsoft.Logic/workflows",
          "Microsoft.ManagedServices",
          "Microsoft.Maps/accounts",
          "Microsoft.Media/mediaservices",
          "Microsoft.Migrate/operations",
          "Microsoft.Migrate/projects",
          "Microsoft.Network/applicationGateways",
          "Microsoft.Network/ApplicationGatewayWebApplicationFirewallPolicies",
          "Microsoft.Network/azureFirewalls",
          "Microsoft.Network/dnsOperationResults",
          "Microsoft.Network/dnsOperationStatuses",
          "Microsoft.Network/dnszones",
          "Microsoft.Network/expressRouteCircuits",
          "Microsoft.Network/expressRouteCrossConnections",
          "Microsoft.Network/expressRouteGateways",
          "Microsoft.Network/ExpressRoutePorts",
          "Microsoft.Network/frontDoors",
          "Microsoft.Network/FrontDoorWebApplicationFirewallPolicies",
          "Microsoft.Network/loadBalancers",
          "Microsoft.Network/NetworkExperimentProfiles",
          "Microsoft.Network/networkInterfaces",
          "Microsoft.Network/networkSecurityGroups",
          "Microsoft.Network/networkWatchers",
          "Microsoft.Network/privateDnsOperationResults",
          "Microsoft.Network/privateOperationStatuses",
          "Microsoft.Network/privateDnsZones",
          "Microsoft.Network/publicIPAddresses",
          "Microsoft.Network/routeTables",
          "Microsoft.Network/trafficmanagerprofiles",
          "Microsoft.Network/virtualNetworks",
          "Microsoft.Network/vpnGateways",
          "Microsoft.NotificationHubs",
          "Microsoft.OperationsManagement/ManagementAssociations",
          "Microsoft.OperationsManagement/solutions",
          "Microsoft.Portal/dashboards",
          "Microsoft.PowerBIDedicated/",
          "Microsoft.Resources/deployments",
          "Microsoft.Resources/deploymentScripts",
          "Microsoft.Resources/resourceGroups",
          "Microsoft.Resources/tags",
          "Microsoft.ResourceGraph/",
          "Microsoft.RecoveryServices/",
          "Microsoft.RecoveryServices/vaults",
          "Microsoft.RecoveryServices/locations",
          "Microsoft.Security/",
          "Microsoft.ServiceBus/namespaces",
          "Microsoft.ServiceFabric/clusters",
          "Microsoft.Scheduler/jobCollections",
          "Microsoft.Solutions/",
          "Microsoft.Sql/servers/databases",
          "Microsoft.StreamAnalytics/streamingJobs",
          "Microsoft.Storage/storageAccounts",
          "Microsoft.StorSimple/managers",
          "Microsoft.Synapse/",
          "Microsoft.Web/serverfarms",
          "Microsoft.Web/sites"
        ]
      }
    },
    "then": {
      "effect": "deny"
    }
  },
  "parameters": {}
}
```