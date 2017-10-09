如果您在部署期間使用參數檔案 toopass 參數值，您需要 toocreate JSON 檔案的格式類似 toohello，下列範例：

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

hello hello 參數檔案大小不能超過 64 KB。

如果您需要 tooprovide 機密值 （例如密碼） 的參數，新增該值 tooa 金鑰保存庫。 Hello 先前範例所示的部署期間擷取 hello 金鑰保存庫。 如需詳細資訊，請參閱 [在部署期間傳遞安全值](../articles/azure-resource-manager/resource-manager-keyvault-parameter.md)。 

