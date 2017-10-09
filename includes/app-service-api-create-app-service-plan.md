<span data-ttu-id="c7454-101">建立應用程式服務方案以 hello [az 應用程式服務方案建立](/cli/azure/appservice/plan#create)命令。</span><span class="sxs-lookup"><span data-stu-id="c7454-101">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span>

[!INCLUDE [app-service-plan](app-service-plan.md)]

<span data-ttu-id="c7454-102">hello 下列範例會建立名為 App Service 方案`myAppServicePlan`在 hello**免費**定價層：</span><span class="sxs-lookup"><span data-stu-id="c7454-102">hello following example creates an App Service plan named `myAppServicePlan` in hello **Free** pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

<span data-ttu-id="c7454-103">Hello 應用程式服務方案建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="c7454-103">When hello App Service plan has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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