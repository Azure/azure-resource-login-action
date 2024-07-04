# Get Azure Resource Token Action

Get raw access token for an specific type of resource in Azure. 

## When to use it

Use `azure-resource-login` for intereacting with Azure components on behalf of an Azure Service Principal when an authentication token is required. You can use the authentication token to use any Azure API, dependening on the resource type you selected.

## Getting Started

### Prerequisites

- A Service Principal created in the tenant.
- The Client ID, Client Secret and Tenant ID associated with the indicated service principal.

### Inputs

| Name | Description | Required |
| --- | --- | --- |
| `creds` | The Azure Active Directory Service Principal credentials to be used in the login process. This information has to be provided in the form of a JSON string [as indicated in this example](https://github.com/marketplace/actions/azure-login#configure-deployment-credentials). You can use <nobr>`${{ secrets.AZURE_CREDENTIALS }}`</nobr> to store the credentials in a secret named `AZURE_CREDENTIALS`. | true |
| <nobr>`resource-url`</nobr> | Canonical resource url for what you want the token for. The resource class GUID can also be used as a URL. | false |
| <nobr>`resource-type-name`</nobr> | Optional resouce type name, supported values: AadGraph, AnalysisServices, Arm, Attestation, Batch, DataLake, KeyVault, OperationalInsights, ResourceManager, Storage, Synapse. Default value is Arm if not specified. | false |

### Example usage

#### Get an access token for a Azure SQL Database, Azure Synapse Analytics or Azure SQL MI

```
id: sql-login
name: Adquiring SQL Access Token
uses: Azure/azure-resource-login-action@v1.1.0
with:
    creds: ${{ secrets.AZURE_CREDENTIALS }}
    resource-url: "https://database.windows.net"
```

> You can use the generated token later as `${{ steps.sql-login.outputs.token }}`

#### Get an access token for managing an Azure Resource

```
id: mgnt-login
name: Adquiring Azure Resource Management Access Token
uses: Azure/azure-resource-login-action@v1.0.0
with:
    creds: ${{ secrets.AZURE_CREDENTIALS }}
    resource-url: "https://management.core.windows.net/"
```

> You can use the generated token later as `${{ steps.mgnt-login.outputs.token }}`

#### Get raw access token for Azure Databricks

```
id: adb-login
name: Adquiring ADB Access Token
uses: Azure/azure-resource-login-action@v1.0.0
with:
    creds: ${{ secrets.AZURE_CREDENTIALS }}
    resource-url: 2ff814a6-3304-4ab8-85cb-cd0e6f879c1d
```

> You can use the generated token later as `${{ steps.adb-login.outputs.token }}`

#### Get raw access token for AAD graph

```
id: aadgraph-login
name: Adquiring AAD graph Access Token
uses: Azure/azure-resource-login-action@v1.0.0
with:
    creds: ${{ secrets.AZURE_CREDENTIALS }}
    resource-type-name: AadGraph
```

## Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

## Trademarks

This project may contain trademarks or logos for projects, products, or services. Authorized use of Microsoft 
trademarks or logos is subject to and must follow 
[Microsoft's Trademark & Brand Guidelines](https://www.microsoft.com/en-us/legal/intellectualproperty/trademarks/usage/general).
Use of Microsoft trademarks or logos in modified versions of this project must not cause confusion or imply Microsoft sponsorship.
Any use of third-party trademarks or logos are subject to those third-party's policies.
