建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。

[!INCLUDE [app-service-plan](app-service-plan.md)]

hello 下列範例會建立名為 App Service 方案`myAppServicePlan`在 hello**免費**定價層：

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Hello 應用程式服務方案建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：

```json
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/0000-0000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan",
  "kind": "app",
  "location": "West Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  < JSON data removed for brevity. >
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
} 
```