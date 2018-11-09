## Deploy a Public certificate from Key Vault secret 

In order to deploy this template, you need to have the following resources:  <br />
1. A Web App   <br />
2. A Key Vault  <br />
3. A Key Vault Secret containting public certificate in base64 encoded format <br />

Once you have the above, replace them with the actual values in the **parameters.json** file. These are the values that needs to be replaced: <br/>

+ **`YOUR-SUBSCRIPTION-ID`** - the subscription ID under which the deployment needs to be made
+ **`YOUR-WEB-APP`** - An existing web app
+ **`YOUR-RESOURCE-GROUP`** - The resource group in which the Key Vault exists
+ **`YOUR-KEY-VAULT`** - Name of the Key Vault
+ **`YOUR-SECRET`** - Key Vault Secret name

## Access to KeyVault for deployment

By default, '**`Microsoft.Azure.WebSites`**' Resource Provider (RP) doesn't have access to the Key Vault specified in the template. Hence before deploying you need to authorize it by executing 
the following PowerShell commands :  <br />
**PowerShell**
```PowerShell
Login-AzureRmAccount  <br />
Set-AzureRmContext -SubscriptionId AZURE_SUBSCRIPTION_ID  <br />
Set-AzureRmKeyVaultAccessPolicy -VaultName KEY_VAULT_NAME -ServicePrincipalName abfa0a7c-a6b6-4736-8310-5855508787cd -PermissionsToSecrets get  <br />
```


**`ServicePrincipalName`** parameter represents **`Microsoft.Azure.WebSites`** RP in user tenant and will remain same for all Azure subscriptions. Refer the Key Vault documentation for more information: [Get started with Azure Key Vault](https://azure.microsoft.com/en-us/documentation/articles/key-vault-get-started/)
