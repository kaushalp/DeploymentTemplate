## Deploy a Web App certificate from Key Vault secret and use it for creating SSL binding

In order to deploy this template, you need to have the following resources:  <br />
1. A Key Vault (specified in 'existingKeyVaultId' parameter) <br />
2. A Key Vault Secret containting public certificate  in base64 encoded format <br />
3. A Web App (specified in 'existingWebAppName' parameter)  <br />
4. The App Service Plan (serverFarm) resource identifier housing the Web App specified in step 3 <br />


By default, '**Microsoft.Azure.WebSites**' Resource Provider (RP) doesn't have access to the Key Vault specified in the template hence you need to authorize it by executing 
the following PowerShell commands before deploying the template:  <br />

```PowerShell
Login-AzureRmAccount  <br />
Set-AzureRmContext -SubscriptionId AZURE_SUBSCRIPTION_ID  <br />
Set-AzureRmKeyVaultAccessPolicy -VaultName KEY_VAULT_NAME -ServicePrincipalName abfa0a7c-a6b6-4736-8310-5855508787cd -PermissionsToSecrets get  <br />
```


ServicePrincipalName parameter represents **Microsoft.Azure.WebSites** RP in user tenant and will remain same for all Azure subscriptions. This is a onetime operation. Once you have a configured a Key Vault properly, 
you can use it for deploying as many certificates as you want without executing these PowerShell commands again. You can go through the Key Vault documentation for more information: <br />
https://azure.microsoft.com/en-us/documentation/articles/key-vault-get-started/