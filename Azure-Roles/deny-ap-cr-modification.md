# Deny Azure Policy & Custom Role Modification

This Azure Policy will deny any actions (creation, deletion, updating, etc) to Azure Policies & and Custom Roles. With that said the reader will still have reader permissions on both resources (in order to see unauthorized error messages when attempting to modify the resources).This is accomplished by assigning a custom role on an Azure Account/Identity that assigns explicit deny permissions to the account. 

To find actions & data actions that you want to allow/deny in explicitly in custom roles please use this link below below:

[Azure Custom Roles Resource Provider Actions & Data Actions](https://docs.microsoft.com/en-us/azure/role-based-access-control/resource-provider-operations)
 
## Azure Custom Roles
   
To read more about Azure Custom Roles please use these links:

[Azure Custom Roles Summary](https://docs.microsoft.com/en-us/azure/role-based-access-control/custom-roles)
/
[Creation of Azure Custom Roles](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/roles-create-custom)


---

## Provider Operations Breakdown

<details>
  <summary>What this allows</summary>

* Microsoft.Authorization/roleDefinitions/read
* Microsoft.Authorization/roleAssignments/read
* Microsoft.Authorization/policySetDefinitions/read
* Microsoft.Authorization/policyDefinitions/read
* Microsoft.Authorization/policyAssignments/read
* Microsoft.Authorization/permissions/read
* Microsoft.Authorization/denyAssignments/read

</details>
<details>
  <summary>What this blocks</summary>

* Microsoft.Authorization/policyassignments/*
* Microsoft.Authorization/policydefinitions/*
* Microsoft.Authorization/policysetdefinitions/*
* Microsoft.Authorization/roleAssignments/*
* Microsoft.Authorization/roleDefinitions/*
* Microsoft.PolicyInsights/*


</details>

## Policy Definition

```json
{
    "properties": {
        "roleName": "CT-CR-Deny-Policy&RoleModification",
        "description": "This Custom Role will prevent any changes/actions (creation, deletion, etc) to Azure Policies & Custom Roles.",
        "assignableScopes": [
            "/subscriptions/6ad3f45a-7b30-4c06-9c3d-fd2b28fea7fc"
        ],
        "permissions": [
            {
                "actions": [
                    "Microsoft.Authorization/roleDefinitions/read",
                    "Microsoft.Authorization/roleAssignments/read",
                    "Microsoft.Authorization/policySetDefinitions/read",
                    "Microsoft.Authorization/policyDefinitions/read",
                    "Microsoft.Authorization/policyAssignments/read",
                    "Microsoft.Authorization/permissions/read",
                    "Microsoft.Authorization/denyAssignments/read"
                ],
                "notActions": [
                    "Microsoft.Authorization/policyassignments/*",
                    "Microsoft.Authorization/policydefinitions/*",
                    "Microsoft.Authorization/policysetdefinitions/*",
                    "Microsoft.Authorization/roleAssignments/*",
                    "Microsoft.Authorization/roleDefinitions/*",
                    "Microsoft.PolicyInsights/*"
                ],
                "dataActions": [],
                "notDataActions": []
            }
        ]
    }
}
```