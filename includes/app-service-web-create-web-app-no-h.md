<span data-ttu-id="cecad-101">建立[web 應用程式](../articles/app-service-web/app-service-web-overview.md)在 hello`myAppServicePlan`應用程式服務方案以 hello [az webapp 建立](/cli/azure/webapp#create)命令。</span><span class="sxs-lookup"><span data-stu-id="cecad-101">Create a [web app](../articles/app-service-web/app-service-web-overview.md) in hello `myAppServicePlan` App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="cecad-102">hello web 應用程式提供裝載程式碼，並提供 URL tooview hello 部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="cecad-102">hello web app provides a hosting space for your code and provides a URL tooview hello deployed app.</span></span>

<span data-ttu-id="cecad-103">下列命令，取代在 hello  *\<app_name >*具有唯一的名稱 (有效的字元是`a-z`， `0-9`，和`-`)。</span><span class="sxs-lookup"><span data-stu-id="cecad-103">In hello following command, replace *\<app_name>* with a unique name (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="cecad-104">如果`<app_name>`是不是唯一，您會收到 hello 錯誤訊息 「 具有指定名稱 < app_name > 網站已經存在 」。</span><span class="sxs-lookup"><span data-stu-id="cecad-104">If `<app_name>` is not unique, you get hello error message "Website with given name <app_name> already exists."</span></span> <span data-ttu-id="cecad-105">hello hello web 應用程式的 URL 是的預設`https://<app_name>.azurewebsites.net`。</span><span class="sxs-lookup"><span data-stu-id="cecad-105">hello default URL of hello web app is `https://<app_name>.azurewebsites.net`.</span></span> 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="cecad-106">Hello web 應用程式建立後，hello Azure CLI 顯示資訊的類似 toohello 下列範例：</span><span class="sxs-lookup"><span data-stu-id="cecad-106">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span>

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

<span data-ttu-id="cecad-107">瀏覽 toohello 網站 toosee 您新建立的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cecad-107">Browse toohello site toosee your newly created web app.</span></span>

```bash
http://<app_name>.azurewebsites.net
```
