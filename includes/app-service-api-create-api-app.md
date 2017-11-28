
<span data-ttu-id="4a8c8-101">使用 [az webapp create](/cli/azure/appservice/web#create) 命令，在 `myAppServicePlan` App Service 方案中建立 [API 應用程式](../articles/app-service-api/app-service-api-apps-why-best-platform.md)。</span><span class="sxs-lookup"><span data-stu-id="4a8c8-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in the `myAppServicePlan` App Service plan with the [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="4a8c8-102">Web 應用程式會為您的 API 提供裝載空間，以及提供 URL 來檢視已部署的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4a8c8-102">The web app provides a hosting space for your API and provides a URL to view the deployed app.</span></span>

<span data-ttu-id="4a8c8-103">在下列命令中，使用唯一的名稱取代 *\<app_name>*。</span><span class="sxs-lookup"><span data-stu-id="4a8c8-103">In the following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="4a8c8-104">如果 `<app_name>` 不是唯一的，您會收到錯誤訊息「具有指定名稱 <app_name> 的網站已經存在」。</span><span class="sxs-lookup"><span data-stu-id="4a8c8-104">If `<app_name>` is not unique, you get the error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="4a8c8-105">Web 應用程式的預設 URL 是 `https://<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="4a8c8-105">The default URL of the web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="4a8c8-106">建立 Web 應用程式後，Azure CLI 會顯示類似下列範例的資訊：</span><span class="sxs-lookup"><span data-stu-id="4a8c8-106">When the web app has been created, the Azure CLI shows information similar to the following example:</span></span>

```json
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "<app_name>.azurewebsites.net",
    "<app_name>.scm.azurewebsites.net"
  ],
  "gatewaySiteName": null,
  "hostNameSslStates": [
    {
      "hostType": "Standard",
      "name": "<app_name>.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "virtualIp": null
    }
    < JSON data removed for brevity. >
}
```