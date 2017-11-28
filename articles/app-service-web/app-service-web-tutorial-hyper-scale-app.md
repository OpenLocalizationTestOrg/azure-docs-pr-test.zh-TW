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
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="24adb-103">在 Azure 中建置超大規模 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="24adb-104">本教學課程會示範如何 tooscale ASP.NET web 應用程式的功能在 Azure toomaximize 使用者要求。</span><span class="sxs-lookup"><span data-stu-id="24adb-104">This tutorial shows you how tooscale out an ASP.NET web app in Azure toomaximize user requests.</span></span>

<span data-ttu-id="24adb-105">再開始本教學課程，請確認[hello 安裝 Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)您的電腦上。</span><span class="sxs-lookup"><span data-stu-id="24adb-105">Before starting this tutorial, ensure that [hello Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="24adb-106">此外，您需要[Visual Studio](https://www.visualstudio.com/vs/)對本機電腦 toorun hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine toorun hello sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="24adb-107">步驟 1 - 取得範例應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="24adb-108">在此步驟中，您會將設定 hello 本機 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="24adb-108">In this step, you set up hello local ASP.NET project.</span></span>

### <a name="clone-hello-application-repository"></a><span data-ttu-id="24adb-109">複製 hello 應用程式儲存機制</span><span class="sxs-lookup"><span data-stu-id="24adb-109">Clone hello application repository</span></span>

<span data-ttu-id="24adb-110">您選擇的開啟 hello 命令列的終端機和`CD`tooa 工作目錄。</span><span class="sxs-lookup"><span data-stu-id="24adb-110">Open hello command-line terminal of your choice and `CD` tooa working directory.</span></span> <span data-ttu-id="24adb-111">然後，執行的 hello 下列命令 tooclone hello 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-111">Then, run hello following commands tooclone hello sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-hello-sample-application-in-visual-studio"></a><span data-ttu-id="24adb-112">執行 Visual Studio 中的 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-112">Run hello sample application in Visual Studio</span></span>

<span data-ttu-id="24adb-113">開啟 Visual Studio 中的 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="24adb-113">Open hello solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="24adb-114">型別`F5`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-114">Type `F5` toorun hello application.</span></span>

<span data-ttu-id="24adb-115">此範例 ASP.NET web 應用程式來自 hello 預設範本，並保存使用者工作階段，並使用 hello 輸出快取。</span><span class="sxs-lookup"><span data-stu-id="24adb-115">This sample ASP.NET web application comes from hello default template, and persists user sessions and uses hello output cache.</span></span> <span data-ttu-id="24adb-116">請看 `HighScaleApp\Controllers\HomeController.cs`。</span><span class="sxs-lookup"><span data-stu-id="24adb-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="24adb-117">hello`Index()`方法會將一段資料 toohello 工作階段。</span><span class="sxs-lookup"><span data-stu-id="24adb-117">hello `Index()` method adds a piece of data toohello session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="24adb-118">和 hello`About()`和`Contact()`方法快取其輸出。</span><span class="sxs-lookup"><span data-stu-id="24adb-118">And hello `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-tooazure"></a><span data-ttu-id="24adb-119">步驟 2-部署 tooAzure</span><span class="sxs-lookup"><span data-stu-id="24adb-119">Step 2 - Deploy tooAzure</span></span>
<span data-ttu-id="24adb-120">在此步驟中，您可以建立 Azure web 應用程式和部署您的範例 ASP.NET 應用程式 tooit。</span><span class="sxs-lookup"><span data-stu-id="24adb-120">In this step, you create an Azure web app and deploy your sample ASP.NET application tooit.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="24adb-121">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="24adb-121">Create a resource group</span></span>   
<span data-ttu-id="24adb-122">使用[az 群組建立](https://docs.microsoft.com/cli/azure/group#create)toocreate[資源群組](../azure-resource-manager/resource-group-overview.md)hello 西歐地區中。</span><span class="sxs-lookup"><span data-stu-id="24adb-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) toocreate a [resource group](../azure-resource-manager/resource-group-overview.md) in hello West Europe region.</span></span> <span data-ttu-id="24adb-123">資源群組是您放置所有 hello Azure 資源的 toomanage 在一起，例如 hello web 應用程式和任何 SQL 資料庫後端。</span><span class="sxs-lookup"><span data-stu-id="24adb-123">A resource group is where you put all hello Azure resources that you want toomanage together, such as hello web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="24adb-124">toosee 何種可能的值，您可以使用`---location`，使用 hello [az appservice 列出位置](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations)命令。</span><span class="sxs-lookup"><span data-stu-id="24adb-124">toosee what possible values you can use for `---location`, use hello [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="24adb-125">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="24adb-125">Create an App Service plan</span></span>
<span data-ttu-id="24adb-126">使用[az 應用程式服務方案建立](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create)toocreate"B1" [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="24adb-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) toocreate a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="24adb-127">App Service 方案是擴充單元，可包含任意數目的應用程式，您想 tooscale 或一起移轉出 hello 相同應用程式服務基礎結構。</span><span class="sxs-lookup"><span data-stu-id="24adb-127">An App Service plan is a scale unit, which can include any number of apps that you want tooscale up or out together over hello same App Service infrastructure.</span></span> <span data-ttu-id="24adb-128">每個方案也被指派[定價層](https://azure.microsoft.com/en-us/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="24adb-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="24adb-129">較高層包括更好的硬體和更多功能，例如更多相應放大的執行個體。</span><span class="sxs-lookup"><span data-stu-id="24adb-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="24adb-130">本教學課程，B1 是 hello 最小層，讓向外延展 toothree 執行個體。</span><span class="sxs-lookup"><span data-stu-id="24adb-130">For this tutorial, B1 is hello minimum tier that enables scale out toothree instances.</span></span> <span data-ttu-id="24adb-131">您可以移動您的應用程式向上或向下 hello 定價層更新版本執行[az 應用程式服務計劃更新](https://docs.microsoft.com/cli/azure/appservice/plan#update)。</span><span class="sxs-lookup"><span data-stu-id="24adb-131">You can always move your app up or down hello pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="24adb-132">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-132">Create a web app</span></span>
<span data-ttu-id="24adb-133">使用[az 應用程式 web 建立](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)toocreate web 應用程式使用唯一的名稱在`$appName`。</span><span class="sxs-lookup"><span data-stu-id="24adb-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="24adb-134">設定部署認證</span><span class="sxs-lookup"><span data-stu-id="24adb-134">Set deployment credentials</span></span>
<span data-ttu-id="24adb-135">使用[az appservice web 部署使用者集合](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set)tooset 帳戶層級部署應用程式服務認證。</span><span class="sxs-lookup"><span data-stu-id="24adb-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) tooset your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="24adb-136">設定 Git 部署</span><span class="sxs-lookup"><span data-stu-id="24adb-136">Configure Git deployment</span></span>
<span data-ttu-id="24adb-137">使用[az appservice 網頁原始檔控制設定的本機-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure 本機 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="24adb-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="24adb-138">此命令可讓您看起來像 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="24adb-138">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="24adb-139">使用 hello 傳回 URL tooconfigure 您 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="24adb-139">Use hello returned URL tooconfigure your Git remote.</span></span> <span data-ttu-id="24adb-140">hello 下列命令會使用 hello 前面輸出範例。</span><span class="sxs-lookup"><span data-stu-id="24adb-140">hello following command uses hello preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-hello-sample-application"></a><span data-ttu-id="24adb-141">部署 hello 範例應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-141">Deploy hello sample application</span></span>
<span data-ttu-id="24adb-142">您會立即準備 toodeploy 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-142">You are now ready toodeploy your sample application.</span></span> <span data-ttu-id="24adb-143">執行 `git push`。</span><span class="sxs-lookup"><span data-stu-id="24adb-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="24adb-144">當提示輸入密碼，請使用您指定當您執行的 hello 密碼`az appservice web deployment user set`。</span><span class="sxs-lookup"><span data-stu-id="24adb-144">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-tooazure-web-app"></a><span data-ttu-id="24adb-145">瀏覽 tooAzure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-145">Browse tooAzure web app</span></span>
<span data-ttu-id="24adb-146">使用[az appservice web 瀏覽](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)toosee 在 Azure 中，即時執行應用程式執行此命令。</span><span class="sxs-lookup"><span data-stu-id="24adb-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-tooredis"></a><span data-ttu-id="24adb-147">步驟 3-連接 tooRedis</span><span class="sxs-lookup"><span data-stu-id="24adb-147">Step 3 - Connect tooRedis</span></span>
<span data-ttu-id="24adb-148">在此步驟中，您將為外部，共置快取 tooyour Azure web 應用程式設定 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="24adb-148">In this step, you set up Azure Redis Cache as an external, colocated cache tooyour Azure web app.</span></span> <span data-ttu-id="24adb-149">您還可以快速利用 Redis toocache 網頁輸出。</span><span class="sxs-lookup"><span data-stu-id="24adb-149">You can quickly utilize Redis toocache your page output.</span></span> <span data-ttu-id="24adb-150">此外，當您稍後相應放大 Web 應用程式時，Redis 會協助您跨多個執行個體可靠地保存使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="24adb-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="24adb-151">建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="24adb-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="24adb-152">使用[az redis 建立](https://docs.microsoft.com/en-us/cli/azure/redis#create)toocreate Azure Redis 快取和儲存 hello JSON 輸出。</span><span class="sxs-lookup"><span data-stu-id="24adb-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate an Azure Redis Cache and save hello JSON output.</span></span> <span data-ttu-id="24adb-153">在 `$cacheName` 中使用唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="24adb-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-hello-application-toouse-redis"></a><span data-ttu-id="24adb-154">設定 hello 應用程式 toouse Redis</span><span class="sxs-lookup"><span data-stu-id="24adb-154">Configure hello application toouse Redis</span></span>
<span data-ttu-id="24adb-155">格式 hello 您的快取的連接字串。</span><span class="sxs-lookup"><span data-stu-id="24adb-155">Format hello connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="24adb-156">hello 第二行應可提供的輸出看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="24adb-156">hello second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="24adb-157">在 Visual Studio 中建立 web 組態檔稱為專案根目錄中的`redis.config`和 hello 貼上下列程式碼到其中。</span><span class="sxs-lookup"><span data-stu-id="24adb-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste hello following code into it.</span></span> <span data-ttu-id="24adb-158">在`value`，使用從 hello PowerShell 輸出 hello 連接字串。</span><span class="sxs-lookup"><span data-stu-id="24adb-158">In `value`, use hello connection string from hello PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="24adb-159">如果您看一下 hello`.gitignore`檔案在您的 Git 儲存機制，您會看到這個檔案從原始檔控制中排除。</span><span class="sxs-lookup"><span data-stu-id="24adb-159">If you look at hello `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="24adb-160">於是，您的機密資訊獲得安全保障。</span><span class="sxs-lookup"><span data-stu-id="24adb-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="24adb-161">開啟 `Web.config`。</span><span class="sxs-lookup"><span data-stu-id="24adb-161">Open `Web.config`.</span></span> <span data-ttu-id="24adb-162">請注意 hello`<appSettings file="redis.config">`項目，就會取得您在建立 hello 設定`redis.config`。</span><span class="sxs-lookup"><span data-stu-id="24adb-162">Notice hello `<appSettings file="redis.config">` element, which gets hello setting you created in `redis.config`.</span></span> 

<span data-ttu-id="24adb-163">尋找 hello 標記為註解 > 一節包含`<sessionState>`和`<caching>`。</span><span class="sxs-lookup"><span data-stu-id="24adb-163">Find hello commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="24adb-164">將此區段取消註解。</span><span class="sxs-lookup"><span data-stu-id="24adb-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="24adb-165">此程式碼會尋找 hello Redis 連接字串中定義您`RedisConnection`。</span><span class="sxs-lookup"><span data-stu-id="24adb-165">This code looks for hello Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="24adb-166">您的應用程式現在會使用 Redis toomanage 工作階段和快取。</span><span class="sxs-lookup"><span data-stu-id="24adb-166">Your application now uses Redis toomanage sessions and caching.</span></span> <span data-ttu-id="24adb-167">型別`F5`toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-167">Type `F5` toorun hello application.</span></span> <span data-ttu-id="24adb-168">如果需要，您可以下載 Redis 管理用戶端 toovisualize hello 資料現在儲存 toohello 快取。</span><span class="sxs-lookup"><span data-stu-id="24adb-168">If you like, you can download a Redis management client toovisualize hello data that is now saved toohello cache.</span></span>

### <a name="configure-hello-connection-string-in-azure"></a><span data-ttu-id="24adb-169">在 Azure 中設定 hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="24adb-169">Configure hello connection string in Azure</span></span>

<span data-ttu-id="24adb-170">在 Azure 中您的應用程式 toowork，您需要 tooconfigure hello Azure web 應用程式中相同的 Redis 連接字串。</span><span class="sxs-lookup"><span data-stu-id="24adb-170">For your application toowork in Azure, you need tooconfigure hello same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="24adb-171">因為`redis.config`就不會維護原始檔控制中已部署的 tooAzure 時不執行 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="24adb-171">Since `redis.config` is not maintained in source control, it is not deployed tooAzure when you run Git deployment.</span></span>

<span data-ttu-id="24adb-172">使用[az appservice web 組態 appsettings 更新](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)tooadd hello 連接字串 hello 與相同名稱 (`RedisConnection`)。</span><span class="sxs-lookup"><span data-stu-id="24adb-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd hello connection string with hello same name (`RedisConnection`).</span></span>

<span data-ttu-id="24adb-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24adb-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="24adb-174">請記住，`$connstring`包含 hello 格式化連接字串。</span><span class="sxs-lookup"><span data-stu-id="24adb-174">Remember that `$connstring` contains hello formatted connection string.</span></span>

### <a name="redeploy-hello-application-tooazure"></a><span data-ttu-id="24adb-175">重新部署 hello 應用程式 tooAzure</span><span class="sxs-lookup"><span data-stu-id="24adb-175">Redeploy hello application tooAzure</span></span>
<span data-ttu-id="24adb-176">使用 Git 命令 toopush 變更 tooAzure</span><span class="sxs-lookup"><span data-stu-id="24adb-176">Use Git commands toopush your changes tooAzure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="24adb-177">當提示輸入密碼，請使用您指定當您執行的 hello 密碼`az appservice web deployment user set`。</span><span class="sxs-lookup"><span data-stu-id="24adb-177">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="24adb-178">瀏覽 toohello Azure web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-178">Browse toohello Azure web app</span></span>
<span data-ttu-id="24adb-179">使用[az appservice web 瀏覽](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)toosee hello 變更存在於 Azure。</span><span class="sxs-lookup"><span data-stu-id="24adb-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) toosee hello changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-toomultiple-instances"></a><span data-ttu-id="24adb-180">步驟 4-小數位數 toomultiple 執行個體</span><span class="sxs-lookup"><span data-stu-id="24adb-180">Step 4 - Scale toomultiple instances</span></span>
<span data-ttu-id="24adb-181">hello 應用程式服務方案是您的 Azure web 應用程式的 hello 擴充單元。</span><span class="sxs-lookup"><span data-stu-id="24adb-181">hello App Service plan is hello scale unit for your Azure web apps.</span></span> <span data-ttu-id="24adb-182">tooscale 您 web 應用程式的功能，您可以調整 hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="24adb-182">tooscale out your web app, you scale hello App Service plan.</span></span>

<span data-ttu-id="24adb-183">使用[az 應用程式服務計劃更新](https://docs.microsoft.com/cli/azure/appservice/plan#update)tooscale 出 hello App Service 方案 toothree 執行個體，也就是 hello hello B1 定價層允許的最大數目。</span><span class="sxs-lookup"><span data-stu-id="24adb-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale out hello App Service plan toothree instances, which is hello maximum number allowed by hello B1 pricing tier.</span></span> <span data-ttu-id="24adb-184">請記住 B1 是定價層建立 hello 稍早的 App Service 方案的時所選擇的 hello。</span><span class="sxs-lookup"><span data-stu-id="24adb-184">Remember that B1 is hello pricing tier that you chose when you created hello App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="24adb-185">步驟 5 - 異地擴充</span><span class="sxs-lookup"><span data-stu-id="24adb-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="24adb-186">調整 地理位置，當您執行應用程式在多個區域的 hello Azure 雲端。</span><span class="sxs-lookup"><span data-stu-id="24adb-186">When scaling geographically, you run your app in multiple regions of hello Azure cloud.</span></span> <span data-ttu-id="24adb-187">此安裝程式的負載分攤進一步根據地理位置的應用程式並降低 hello 回應時間放入您的應用程式更接近 tooclient 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="24adb-187">This setup load-balances your app further based on geography and lowers hello response time by placing your app closer tooclient browsers.</span></span>

<span data-ttu-id="24adb-188">在此步驟中，您可以調整您 ASP.NET web 應用程式 tooa 第二個區域與[Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/)。</span><span class="sxs-lookup"><span data-stu-id="24adb-188">In this step, you scale your ASP.NET web app tooa second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="24adb-189">在 hello hello 步驟最後，您必須在西歐 （已建立） 中執行的 web 應用程式和 web 應用程式在東南亞 （尚未建立） 中執行。</span><span class="sxs-lookup"><span data-stu-id="24adb-189">At hello end of hello step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="24adb-190">兩個應用程式將會服務來自 hello 相同流量管理員 URL。</span><span class="sxs-lookup"><span data-stu-id="24adb-190">Both apps will be served from hello same Traffic Manager URL.</span></span>

### <a name="scale-up-hello-europe-app-toostandard-tier"></a><span data-ttu-id="24adb-191">向上擴充 hello 歐洲應用程式 tooStandard 層</span><span class="sxs-lookup"><span data-stu-id="24adb-191">Scale up hello Europe app tooStandard tier</span></span>
<span data-ttu-id="24adb-192">App Service 中整合搭配 Azure 流量管理員需要 hello 標準定價層。</span><span class="sxs-lookup"><span data-stu-id="24adb-192">In App Service, integration with Azure Traffic Manager requires hello Standard pricing tier.</span></span> <span data-ttu-id="24adb-193">使用[az 應用程式服務計劃更新](https://docs.microsoft.com/cli/azure/appservice/plan#update)註冊您的應用程式服務計劃 tooS1 tooscale。</span><span class="sxs-lookup"><span data-stu-id="24adb-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) tooscale up your App Service plan tooS1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="24adb-194">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="24adb-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="24adb-195">使用[az 網路流量管理員設定檔建立](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create)toocreate Traffic Manager 設定檔，然後將它加入 tooyour 資源群組。</span><span class="sxs-lookup"><span data-stu-id="24adb-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) toocreate a Traffic Manager profile and add it tooyour resource group.</span></span> <span data-ttu-id="24adb-196">在 $dnsName 中使用唯一的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="24adb-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="24adb-197">`--routing-method Performance`指定此設定檔[路由傳送使用者流量 toohello 最靠近的端點](../traffic-manager/traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="24adb-197">`--routing-method Performance` specifies that this profile [routes user traffic toohello closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-hello-resource-id-of-hello-europe-app"></a><span data-ttu-id="24adb-198">取得 hello hello 歐洲應用程式的資源識別碼</span><span class="sxs-lookup"><span data-stu-id="24adb-198">Get hello resource ID of hello Europe app</span></span>
<span data-ttu-id="24adb-199">使用[az appservice web 顯示](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show)tooget hello 資源識別碼的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-europe-app"></a><span data-ttu-id="24adb-200">加入 hello 歐洲應用程式的流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="24adb-200">Add a Traffic Manager endpoint for hello Europe app</span></span>
<span data-ttu-id="24adb-201">使用[az 網路流量管理員端點建立](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create)tooadd 端點 tooyour Traffic Manager 設定檔和您的 web 應用程式，作為使用 hello 資源識別碼 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="24adb-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd an endpoint tooyour Traffic Manager profile and use hello resource ID of your web app as hello target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-hello-traffic-manager-endpoint-url"></a><span data-ttu-id="24adb-202">取得 hello Traffic Manager 端點 URL</span><span class="sxs-lookup"><span data-stu-id="24adb-202">Get hello Traffic Manager endpoint URL</span></span>
<span data-ttu-id="24adb-203">您的 Traffic Manager 設定檔現在有端點該點 tooyour 現有 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-203">Your Traffic Manager profile now has an endpoint that points tooyour existing web app.</span></span> <span data-ttu-id="24adb-204">使用[az 網路流量管理員設定檔顯示](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show)tooget 其 URL。</span><span class="sxs-lookup"><span data-stu-id="24adb-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) tooget its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="24adb-205">Hello 輸出複製到您的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="24adb-205">Copy hello output into your browser.</span></span> <span data-ttu-id="24adb-206">您應該會再次看到您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="24adb-207">在亞洲建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="24adb-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="24adb-208">現在，您將複寫您的 Azure web 應用程式 toohello 東南亞區域。</span><span class="sxs-lookup"><span data-stu-id="24adb-208">Now, you replicate your Azure web app toohello Southeast Asia region.</span></span> <span data-ttu-id="24adb-209">toostart，使用[az redis 建立](https://docs.microsoft.com/en-us/cli/azure/redis#create)toocreate 第二個 Azure Redis 快取中東南亞。</span><span class="sxs-lookup"><span data-stu-id="24adb-209">toostart, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) toocreate a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="24adb-210">此快取需要 toobe 共置於亞洲的應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-210">This cache needs toobe colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="24adb-211">`--name $cacheName-asia`提供 hello 以 hello hello 西歐快取，快取 hello 名稱`-asia`後置詞。</span><span class="sxs-lookup"><span data-stu-id="24adb-211">`--name $cacheName-asia` gives hello cache hello name of hello West Europe cache, with hello `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="24adb-212">在亞洲建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="24adb-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="24adb-213">使用[az 應用程式服務方案建立](https://docs.microsoft.com/cli/azure/appservice/plan#create)toocreate 第二個應用程式服務計劃 hello 東南亞區域中，使用 hello 相同 S1 層當做 hello 西歐計劃。</span><span class="sxs-lookup"><span data-stu-id="24adb-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) toocreate a second App Service plan in hello Southeast Asia region, using hello same S1 tier as hello West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="24adb-214">在亞洲建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-214">Create a web app in Asia</span></span>
<span data-ttu-id="24adb-215">使用[az 應用程式 web 建立](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)toocreate 第二個 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) toocreate a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="24adb-216">`--name $appName-asia`提供以 hello hello hello 西歐應用程式，應用程式 hello 名稱`-asia`後置詞。</span><span class="sxs-lookup"><span data-stu-id="24adb-216">`--name $appName-asia` gives hello app hello name of hello West Europe app, with hello `-asia` suffix.</span></span>

### <a name="configure-hello-connection-string-for-redis"></a><span data-ttu-id="24adb-217">設定 Redis hello 連接字串</span><span class="sxs-lookup"><span data-stu-id="24adb-217">Configure hello connection string for Redis</span></span>
<span data-ttu-id="24adb-218">使用[az appservice web 組態 appsettings 更新](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)tooadd toohello web 應用程式 hello 連接字串 hello 東南亞快取。</span><span class="sxs-lookup"><span data-stu-id="24adb-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd toohello web app hello connection string for hello Southeast Asia cache.</span></span>

<span data-ttu-id="24adb-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="24adb-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-hello-asia-app"></a><span data-ttu-id="24adb-220">設定 Git 的部署 hello 亞洲應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-220">Configure Git deployment for hello Asia app.</span></span>
<span data-ttu-id="24adb-221">使用[az appservice 網頁原始檔控制設定的本機-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure hello 第二個 web 應用程式的本機 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="24adb-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) tooconfigure local Git deployment for hello second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="24adb-222">此命令可讓您看起來像 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="24adb-222">This command gives you an output that looks like hello following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="24adb-223">使用 hello 傳回 URL tooconfigure 第二個 Git 遠端的本機儲存機制。</span><span class="sxs-lookup"><span data-stu-id="24adb-223">Use hello returned URL tooconfigure a second Git remote for your local repository.</span></span> <span data-ttu-id="24adb-224">hello 下列命令會使用 hello 前面輸出範例。</span><span class="sxs-lookup"><span data-stu-id="24adb-224">hello following command uses hello preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="24adb-225">部署範例應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-225">Deploy your sample application</span></span>
<span data-ttu-id="24adb-226">執行`git push`toodeploy 您範例應用程式 toohello 第二個 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="24adb-226">Run `git push` toodeploy your sample application toohello second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="24adb-227">當提示輸入密碼，請使用您指定當您執行的 hello 密碼`az appservice web deployment user set`。</span><span class="sxs-lookup"><span data-stu-id="24adb-227">When prompted for password, use hello password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-toohello-asia-app"></a><span data-ttu-id="24adb-228">瀏覽 toohello 亞洲應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-228">Browse toohello Asia app</span></span>
<span data-ttu-id="24adb-229">使用[az appservice web 瀏覽](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)tooverify 即時 Azure 中執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) tooverify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-hello-resource-id-of-hello-asia-app"></a><span data-ttu-id="24adb-230">取得 hello hello 亞洲應用程式的資源識別碼</span><span class="sxs-lookup"><span data-stu-id="24adb-230">Get hello resource ID of hello Asia app</span></span>
<span data-ttu-id="24adb-231">使用[az appservice web 顯示](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show)tooget hello 資源識別碼東南亞在 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="24adb-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) tooget hello resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-hello-asia-app"></a><span data-ttu-id="24adb-232">加入 hello 亞洲應用程式的流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="24adb-232">Add a Traffic Manager endpoint for hello Asia app</span></span>
<span data-ttu-id="24adb-233">使用[az 網路流量管理員端點建立](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create)tooadd 第二個端點 toohello Traffic Manager 設定檔。</span><span class="sxs-lookup"><span data-stu-id="24adb-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) tooadd a second endpoint toohello Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-tooweb-apps"></a><span data-ttu-id="24adb-234">新增區域識別項 tooweb 應用程式</span><span class="sxs-lookup"><span data-stu-id="24adb-234">Add region identifier tooweb apps</span></span>
<span data-ttu-id="24adb-235">使用[az appservice web 組態 appsettings 更新](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update)tooadd 特定地區的環境變數。</span><span class="sxs-lookup"><span data-stu-id="24adb-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) tooadd a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="24adb-236">您的應用程式碼已使用此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="24adb-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="24adb-237">請看 `HighScaleApp\Views\Home\Index.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="24adb-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="24adb-238">完成！</span><span class="sxs-lookup"><span data-stu-id="24adb-238">Complete!</span></span>

<span data-ttu-id="24adb-239">現在，再次嘗試您的 Traffic Manager 設定檔，從不同的地理區域中的瀏覽器 tooaccess hello URL。</span><span class="sxs-lookup"><span data-stu-id="24adb-239">Now, try tooaccess hello URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="24adb-240">來自歐洲的用戶端瀏覽器應該會顯示「ASP.NET 西歐」，來自亞洲的用戶端瀏覽器應該會顯示「ASP.NET 東南亞」。</span><span class="sxs-lookup"><span data-stu-id="24adb-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="24adb-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="24adb-241">More resources</span></span>
