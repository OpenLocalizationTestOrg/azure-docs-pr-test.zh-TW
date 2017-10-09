<span data-ttu-id="1ad79-101">如果您在部署期間使用參數檔案 toopass 參數值，您需要 toocreate JSON 檔案的格式類似 toohello，下列範例：</span><span class="sxs-lookup"><span data-stu-id="1ad79-101">If you use a parameter file toopass parameter values during deployment, you need toocreate a JSON file with a format similar toohello following example:</span></span>

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

<span data-ttu-id="1ad79-102">hello hello 參數檔案大小不能超過 64 KB。</span><span class="sxs-lookup"><span data-stu-id="1ad79-102">hello size of hello parameter file cannot be more than 64 KB.</span></span>

<span data-ttu-id="1ad79-103">如果您需要 tooprovide 機密值 （例如密碼） 的參數，新增該值 tooa 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="1ad79-103">If you need tooprovide a sensitive value for a parameter (such as a password), add that value tooa key vault.</span></span> <span data-ttu-id="1ad79-104">Hello 先前範例所示的部署期間擷取 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="1ad79-104">Retrieve hello key vault during deployment as shown in hello previous example.</span></span> <span data-ttu-id="1ad79-105">如需詳細資訊，請參閱 [在部署期間傳遞安全值](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md)。</span><span class="sxs-lookup"><span data-stu-id="1ad79-105">For more information, see [Pass secure values during deployment](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md).</span></span> 

