# Deny Non-CIS Imaged VMs & VMSS

This Azure Policy will restrict the deployment of Virtual Machines & Virtual Machine Scale Sets to only those using CIS Images. This is accomplished by only allowing images from the publisher "center-for-internet-security-inc". Azure Marketplace CIS Images are preconfigured to the security recommendations of the CIS Benchmarks, trusted configuration guidelines developed and used by a global community of IT experts. In Azure they are often used in substitution of STIG Images; one should consult their security engineer to confirm/deny if CIS imaged Virtual Machines and Virtual Machine Scale Sets are up to par with an organization's security standard. 

To find publishers that you want to approve for use in your Azure environment, follow the steps below:

1. Install the [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)
2. Run the command `az login` to authenticate to your Azure account.
3. Run the command `az vm image list-publishers -l eastus | grep name`. Replace `eastus` with the region your environment is in.
This will output data like below:
```json
    "name": "zerodown_software",
    "name": "zerto",
    "name": "zettalane_systems-5254599",
    "name": "zevenet",
    "name": "zoomdata",
    "name": "zscaler",
```
4. If you are looking for a particular vendor (for example, RedHat), you can append the following to the command above: ` | grep RedHat`.
5. Copy the value for the `name` field and place it into the policy, following the existing example. 

 
## CIS References
   
To read more about the Center for Internet Security as well as CIS Hardened Images in Azure please use these links:

[Azure Documentation on CIS](https://docs.microsoft.com/en-us/microsoft-365/compliance/offering-cis-benchmark?view=o365-worldwide)
/
[Available CIS Images in Azure](https://www.cisecurity.org/cis-hardened-images/microsoft/)


---

## Provider Operations Breakdown

<details>
  <summary>What this allows</summary>

* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachinesScaleSets
* Microsoft.Compute/imagePublisher if equal "center-for-internet-security-inc"

</details>
<details>
  <summary>What this blocks</summary>

* Images from any other provider other then Center for Internet Security Inc (CIS)


</details>

## Policy Definition

```json
{
  "mode": "All",
  "policyRule": {
    "if": {
      "allOf": [
        {
          "field": "type",
          "in": [
            "Microsoft.Compute/virtualMachines",
            "Microsoft.Compute/virtualMachineScaleSets"
          ]
        },
        {
          "not": {
            "field": "Microsoft.Compute/imagePublisher",
            "equals": "center-for-internet-security-inc"
          }
        }
      ]
    },
    "then": {
      "effect": "deny"
    }
  },
  "parameters": {}
}
```