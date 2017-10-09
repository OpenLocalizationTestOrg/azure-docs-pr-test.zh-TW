
<span data-ttu-id="d9583-101">建立[API 應用程式](../articles/app-service-api/app-service-api-apps-why-best-platform.md)在 hello`myAppServicePlan`應用程式服務方案以 hello [az webapp 建立](/cli/azure/appservice/web#create)命令。</span><span class="sxs-lookup"><span data-stu-id="d9583-101">Create a [API app](../articles/app-service-api/app-service-api-apps-why-best-platform.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/appservice/web#create) command.</span></span> 

<span data-ttu-id="d9583-102">hello web 應用程式提供裝載您的 API，並提供 URL tooview hello 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="d9583-102">hello web app provides a hosting space for your API and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="d9583-103">下列命令，取代在 hello  *\<app_name >*具有唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="d9583-103">In hello following command, replace *\<app_name>* with a unique name.</span></span> <span data-ttu-id="d9583-104">如果`<app_name>`是不是唯一，您會收到 hello 錯誤訊息 「 具有指定名稱 < app_name > 網站已經存在 」。</span><span class="sxs-lookup"><span data-stu-id="d9583-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="d9583-105">hello hello web 應用程式的 URL 是的預設`https://<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="d9583-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="d9583-106">Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="d9583-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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