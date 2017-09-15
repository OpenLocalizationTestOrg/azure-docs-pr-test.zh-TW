<span data-ttu-id="34643-101">如果您在部署期間使用參數檔案傳遞參數值，您必須使用類似於下列範例的格式建立 JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="34643-101">If you use a parameter file to pass parameter values during deployment, you need to create a JSON file with a format similar to the following example:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "webSiteName": {
            "value": "ExampleSite"
        },
        "webSiteHostingPlanName": {
            "value": "DefaultPlan"
        },
        "webSiteLocation": {
            "value": "West US"
        },
        "adminPassword": {
            "reference": {
               "keyVault": {
                  "id": "/subscriptions/{guid}/resourceGroups/{group-name}/providers/Microsoft.KeyVault/vaults/{vault-name}"
               }, 
               "secretName": "sqlAdminPassword" 
            }   
        }
   }
}
```

<span data-ttu-id="34643-102">參數檔的大小不得超過 64 KB。</span><span class="sxs-lookup"><span data-stu-id="34643-102">The size of the parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="34643-103">如果您需要提供參數機密的值 (例如密碼)，請將該值加入金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="34643-103">If you need to provide a sensitive value for a parameter (such as a password), add that value to a key vault.</span></span> <span data-ttu-id="34643-104">在部署期間擷取金鑰保存庫，如先前範例所示。</span><span class="sxs-lookup"><span data-stu-id="34643-104">Retrieve the key vault during deployment as shown in the previous example.</span></span> <span data-ttu-id="34643-105">如需詳細資訊，請參閱 [在部署期間傳遞安全值](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md)。</span><span class="sxs-lookup"><span data-stu-id="34643-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

