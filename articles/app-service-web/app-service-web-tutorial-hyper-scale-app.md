---
title: "在 Azure 中的大規模應用程式 aaaBuild |Microsoft 文件"
description: "了解如何 toouse 不同的 Azure 服務 toomaximize hello Azure 中的 ASP.NET 應用程式的效能。"
services: app-service\web
documentationcenter: dotnet
author: cephalin
manager: erikre
editor: 
ms.assetid: a4d49ac7-0f97-4997-84c5-cdb9c4465757
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 03/23/2017
ms.author: cephalin
ms.openlocfilehash: 7952647b49a82c286c6a737eb41a7f23a13fd75e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a>在 Azure 中建置超大規模 Web 應用程式

本教學課程會示範如何 tooscale ASP.NET web 應用程式的功能在 Azure toomaximize 使用者要求。

再開始本教學課程，請確認[hello 安裝 Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)您的電腦上。 此外，您需要[Visual Studio](https://www.visualstudio.com/vs/)對本機電腦 toorun hello 範例應用程式。

## <a name="step-1---get-sample-application"></a>步驟 1 - 取得範例應用程式
在此步驟中，您會將設定 hello 本機 ASP.NET 專案。

### <a name="clone-hello-application-repository"></a>複製 hello 應用程式儲存機制

您選擇的開啟 hello 命令列的終端機和`CD`tooa 工作目錄。 然後，執行的 hello 下列命令 tooclone hello 範例應用程式。 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a>執行 Visual Studio 中的 hello 範例應用程式

開啟 Visual Studio 中的 hello 方案。

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

型別`F5`toorun hello 應用程式。

此範例 ASP.NET web 應用程式來自 hello 預設範本，並保存使用者工作階段，並使用 hello 輸出快取。 請看 `HighScaleApp\Controllers\HomeController.cs`。 hello`Index()`方法會將一段資料 toohello 工作階段。

```csharp
Session.Add("visited", "true"); 
```

和 hello`About()`和`Contact()`方法快取其輸出。

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a>步驟 2-部署 tooAzure
在此步驟中，您可以建立 Azure web 應用程式和部署您的範例 ASP.NET 應用程式 tooit。

### <a name="create-a-resource-group"></a>建立資源群組   
使用[az 群組建立](https://docs.microsoft.com/cli/azure/group#create)toocreate[資源群組](../azure-resource-manager/resource-group-overview.md)hello 西歐地區中。 資源群組是您放置所有 hello Azure 資源的 toomanage 在一起，例如 hello web 應用程式和任何 SQL 資料庫後端。

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

toosee 何種可能的值，您可以使用`---location`，使用 hello [az appservice 列出位置](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations)命令。

### <a name="create-an-app-service-plan"></a>建立應用程式服務方案
使用[az 應用程式服務方案建立](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create)toocreate"B1" [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

App Service 方案是擴充單元，可包含任意數目的應用程式，您想 tooscale 或一起移轉出 hello 相同應用程式服務基礎結構。 每個方案也被指派[定價層](https://azure.microsoft.com/en-us/pricing/details/app-service/)。 較高層包括更好的硬體和更多功能，例如更多相應放大的執行個體。

本教學課程，B1 是 hello 最小層，讓向外延展 toothree 執行個體。 您可以移動您的應用程式向上或向下 hello 定價層更新版本執行[az 應用程式服務計劃更新](https://docs.microsoft.com/cli/azure/appservice/plan#update)。 

### <a name="create-a-web-app"></a>建立 Web 應用程式
使用[az 應用程式 web 建立](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)toocreate web 應用程式使用唯一的名稱在`$appName`。

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a>設定部署認證
使用[az appservice web 部署使用者集合](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set)tooset 帳戶層級部署應用程式服務認證。

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a>設定 Git 部署
使用[az appservice 網頁原始檔控制設定的本機-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure 本機 Git 部署。

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

此命令可讓您看起來像 hello 下列輸出：

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

使用 hello 傳回 URL tooconfigure 您 Git 遠端。 hello 下列命令會使用 hello 前面輸出範例。

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a>部署 hello 範例應用程式
您會立即準備 toodeploy 範例應用程式。 執行 `git push`。

```powershell
git push azure master
```

當提示輸入密碼，請使用您指定當您執行的 hello 密碼`az appservice web deployment user set`。

### <a name="browse-tooazure-web-app"></a>瀏覽 tooAzure web 應用程式
使用[az appservice web 瀏覽](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)toosee 在 Azure 中，即時執行應用程式執行此命令。

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a>步驟 3-連接 tooRedis
在此步驟中，您將為外部，共置快取 tooyour Azure web 應用程式設定 Azure Redis 快取。 您還可以快速利用 Redis toocache 網頁輸出。 此外，當您稍後相應放大 Web 應用程式時，Redis 會協助您跨多個執行個體可靠地保存使用者工作階段。

### <a name="create-an-azure-redis-cache"></a>建立 Azure Redis 快取
使用[az redis 建立](https://docs.microsoft.com/en-us/cli/azure/redis#create)toocreate Azure Redis 快取和儲存 hello JSON 輸出。 在 `$cacheName` 中使用唯一名稱。

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a>設定 hello 應用程式 toouse Redis
格式 hello 您的快取的連接字串。

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

hello 第二行應可提供的輸出看起來像這樣：

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

在 Visual Studio 中建立 web 組態檔稱為專案根目錄中的`redis.config`和 hello 貼上下列程式碼到其中。 在`value`，使用從 hello PowerShell 輸出 hello 連接字串。

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

如果您看一下 hello`.gitignore`檔案在您的 Git 儲存機制，您會看到這個檔案從原始檔控制中排除。 於是，您的機密資訊獲得安全保障。 

開啟 `Web.config`。 請注意 hello`<appSettings file="redis.config">`項目，就會取得您在建立 hello 設定`redis.config`。 

尋找 hello 標記為註解 > 一節包含`<sessionState>`和`<caching>`。 將此區段取消註解。

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

此程式碼會尋找 hello Redis 連接字串中定義您`RedisConnection`。 

您的應用程式現在會使用 Redis toomanage 工作階段和快取。 型別`F5`toorun hello 應用程式。 如果需要，您可以下載 Redis 管理用戶端 toovisualize hello 資料現在儲存 toohello 快取。

### <a name="configure-hello-connection-string-in-azure"></a>在 Azure 中設定 hello 連接字串

在 Azure 中您的應用程式 toowork，您需要 tooconfigure hello Azure web 應用程式中相同的 Redis 連接字串。 因為`redis.config`就不會維護原始檔控制中已部署的 tooAzure 時不執行 Git 部署。

使用[az appservice web 組態 appsettings 更新](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)tooadd hello 連接字串 hello 與相同名稱 (`RedisConnection`)。

az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup

請記住，`$connstring`包含 hello 格式化連接字串。

### <a name="redeploy-hello-application-tooazure"></a>重新部署 hello 應用程式 tooAzure
使用 Git 命令 toopush 變更 tooAzure

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

當提示輸入密碼，請使用您指定當您執行的 hello 密碼`az appservice web deployment user set`。

### <a name="browse-toohello-azure-web-app"></a>瀏覽 toohello Azure web 應用程式
使用[az appservice web 瀏覽](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)toosee hello 變更存在於 Azure。

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a>步驟 4-小數位數 toomultiple 執行個體
hello 應用程式服務方案是您的 Azure web 應用程式的 hello 擴充單元。 tooscale 您 web 應用程式的功能，您可以調整 hello 應用程式服務方案。

使用[az 應用程式服務計劃更新](https://docs.microsoft.com/cli/azure/appservice/plan#update)tooscale 出 hello App Service 方案 toothree 執行個體，也就是 hello hello B1 定價層允許的最大數目。 請記住 B1 是定價層建立 hello 稍早的 App Service 方案的時所選擇的 hello。 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a>步驟 5 - 異地擴充
調整 地理位置，當您執行應用程式在多個區域的 hello Azure 雲端。 此安裝程式的負載分攤進一步根據地理位置的應用程式並降低 hello 回應時間放入您的應用程式更接近 tooclient 瀏覽器。

在此步驟中，您可以調整您 ASP.NET web 應用程式 tooa 第二個區域與[Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/)。 在 hello hello 步驟最後，您必須在西歐 （已建立） 中執行的 web 應用程式和 web 應用程式在東南亞 （尚未建立） 中執行。 兩個應用程式將會服務來自 hello 相同流量管理員 URL。

### <a name="scale-up-hello-europe-app-toostandard-tier"></a>向上擴充 hello 歐洲應用程式 tooStandard 層
App Service 中整合搭配 Azure 流量管理員需要 hello 標準定價層。 使用[az 應用程式服務計劃更新](https://docs.microsoft.com/cli/azure/appservice/plan#update)註冊您的應用程式服務計劃 tooS1 tooscale。 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a>建立流量管理員設定檔 
使用[az 網路流量管理員設定檔建立](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create)toocreate Traffic Manager 設定檔，然後將它加入 tooyour 資源群組。 在 $dnsName 中使用唯一的 DNS 名稱。

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> `--routing-method Performance`指定此設定檔[路由傳送使用者流量 toohello 最靠近的端點](../traffic-manager/traffic-manager-routing-methods.md)。

### <a name="get-hello-resource-id-of-hello-europe-app"></a>取得 hello hello 歐洲應用程式的資源識別碼
使用[az appservice web 顯示](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show)tooget hello 資源識別碼的 web 應用程式。

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a>加入 hello 歐洲應用程式的流量管理員端點
使用[az 網路流量管理員端點建立](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create)tooadd 端點 tooyour Traffic Manager 設定檔和您的 web 應用程式，作為使用 hello 資源識別碼 hello 目標。

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a>取得 hello Traffic Manager 端點 URL
您的 Traffic Manager 設定檔現在有端點該點 tooyour 現有 web 應用程式。 使用[az 網路流量管理員設定檔顯示](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show)tooget 其 URL。 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

Hello 輸出複製到您的瀏覽器。 您應該會再次看到您的 Web 應用程式。

### <a name="create-an-azure-redis-cache-in-asia"></a>在亞洲建立 Azure Redis 快取
現在，您將複寫您的 Azure web 應用程式 toohello 東南亞區域。 toostart，使用[az redis 建立](https://docs.microsoft.com/en-us/cli/azure/redis#create)toocreate 第二個 Azure Redis 快取中東南亞。 此快取需要 toobe 共置於亞洲的應用程式。

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

`--name $cacheName-asia`提供 hello 以 hello hello 西歐快取，快取 hello 名稱`-asia`後置詞。

### <a name="create-an-app-service-plan-in-asia"></a>在亞洲建立 App Service 方案
使用[az 應用程式服務方案建立](https://docs.microsoft.com/cli/azure/appservice/plan#create)toocreate 第二個應用程式服務計劃 hello 東南亞區域中，使用 hello 相同 S1 層當做 hello 西歐計劃。

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a>在亞洲建立 Web 應用程式
使用[az 應用程式 web 建立](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)toocreate 第二個 web 應用程式。

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

`--name $appName-asia`提供以 hello hello hello 西歐應用程式，應用程式 hello 名稱`-asia`後置詞。

### <a name="configure-hello-connection-string-for-redis"></a>設定 Redis hello 連接字串
使用[az appservice web 組態 appsettings 更新](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)tooadd toohello web 應用程式 hello 連接字串 hello 東南亞快取。

az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup

### <a name="configure-git-deployment-for-hello-asia-app"></a>設定 Git 的部署 hello 亞洲應用程式。
使用[az appservice 網頁原始檔控制設定的本機-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure hello 第二個 web 應用程式的本機 Git 部署。

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

此命令可讓您看起來像 hello 下列輸出：

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

使用 hello 傳回 URL tooconfigure 第二個 Git 遠端的本機儲存機制。 hello 下列命令會使用 hello 前面輸出範例。

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a>部署範例應用程式
執行`git push`toodeploy 您範例應用程式 toohello 第二個 Git 遠端。 

```bash
git push azure-asia master
```

當提示輸入密碼，請使用您指定當您執行的 hello 密碼`az appservice web deployment user set`。

### <a name="browse-toohello-asia-app"></a>瀏覽 toohello 亞洲應用程式
使用[az appservice web 瀏覽](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)tooverify 即時 Azure 中執行您的應用程式。

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a>取得 hello hello 亞洲應用程式的資源識別碼
使用[az appservice web 顯示](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show)tooget hello 資源識別碼東南亞在 web 應用程式。

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a>加入 hello 亞洲應用程式的流量管理員端點
使用[az 網路流量管理員端點建立](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create)tooadd 第二個端點 toohello Traffic Manager 設定檔。

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a>新增區域識別項 tooweb 應用程式
使用[az appservice web 組態 appsettings 更新](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)tooadd 特定地區的環境變數。

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

您的應用程式碼已使用此應用程式設定。 請看 `HighScaleApp\Views\Home\Index.cshtml`。

### <a name="complete"></a>完成！

現在，再次嘗試您的 Traffic Manager 設定檔，從不同的地理區域中的瀏覽器 tooaccess hello URL。 來自歐洲的用戶端瀏覽器應該會顯示「ASP.NET 西歐」，來自亞洲的用戶端瀏覽器應該會顯示「ASP.NET 東南亞」。

## <a name="more-resources"></a>其他資源
