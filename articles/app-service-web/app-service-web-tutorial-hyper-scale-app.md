---
title: "在 Azure 中建置超大規模應用程式 | Microsoft Docs"
description: "了解如何使用不同的 Azure 服務，將 Azure 中的 ASP.NET 應用程式效能最大化。"
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
ms.openlocfilehash: eac9c5b0d8d0f7802d88e6f4f27d9d23c406e025
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="build-a-hyper-scale-web-app-in-azure"></a><span data-ttu-id="650be-103">在 Azure 中建置超大規模 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-103">Build a hyper-scale web app in Azure</span></span>

<span data-ttu-id="650be-104">本教學課程示範如何相應放大 Azure 中的 ASP.NET Web 應用程式，以處理最多的使用者要求。</span><span class="sxs-lookup"><span data-stu-id="650be-104">This tutorial shows you how to scale out an ASP.NET web app in Azure to maximize user requests.</span></span>

<span data-ttu-id="650be-105">開始本教學課程之前，請確認您的電腦上[已安裝 Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="650be-105">Before starting this tutorial, ensure that [the Azure CLI is installed](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli) on your machine.</span></span> <span data-ttu-id="650be-106">此外，本機電腦上還需要 [Visual Studio](https://www.visualstudio.com/vs/) 以執行範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-106">In addition, you need [Visual Studio](https://www.visualstudio.com/vs/) on your local machine to run the sample application.</span></span>

## <a name="step-1---get-sample-application"></a><span data-ttu-id="650be-107">步驟 1 - 取得範例應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-107">Step 1 - Get sample application</span></span>
<span data-ttu-id="650be-108">在此步驟中，您要設定本機的 ASP.NET 專案。</span><span class="sxs-lookup"><span data-stu-id="650be-108">In this step, you set up the local ASP.NET project.</span></span>

### <a name="clone-the-application-repository"></a><span data-ttu-id="650be-109">複製應用程式存放庫</span><span class="sxs-lookup"><span data-stu-id="650be-109">Clone the application repository</span></span>

<span data-ttu-id="650be-110">開啟您選擇的命令列終端機，並 `CD` 到工作目錄。</span><span class="sxs-lookup"><span data-stu-id="650be-110">Open the command-line terminal of your choice and `CD` to a working directory.</span></span> <span data-ttu-id="650be-111">然後，執行下列命令來複製範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-111">Then, run the following commands to clone the sample application.</span></span> 

```powershell
git clone https://github.com/cephalin/HighScaleApp.git
```

### <a name="run-the-sample-application-in-visual-studio"></a><span data-ttu-id="650be-112">在 Visual Studio 中執行範例應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-112">Run the sample application in Visual Studio</span></span>

<span data-ttu-id="650be-113">在 Visual Studio 中開啟解決方案。</span><span class="sxs-lookup"><span data-stu-id="650be-113">Open the solution in Visual Studio.</span></span>

```powershell
cd HighScaleApp
.\HighScaleApp.sln
```

<span data-ttu-id="650be-114">輸入 `F5` 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-114">Type `F5` to run the application.</span></span>

<span data-ttu-id="650be-115">此範例 ASP.NET Web 應用程式來自預設範本，可保存使用者工作階段，且使用輸出快取。</span><span class="sxs-lookup"><span data-stu-id="650be-115">This sample ASP.NET web application comes from the default template, and persists user sessions and uses the output cache.</span></span> <span data-ttu-id="650be-116">請看 `HighScaleApp\Controllers\HomeController.cs`。</span><span class="sxs-lookup"><span data-stu-id="650be-116">Take a look at `HighScaleApp\Controllers\HomeController.cs`.</span></span> <span data-ttu-id="650be-117">`Index()` 方法將一份資料新增至工作階段。</span><span class="sxs-lookup"><span data-stu-id="650be-117">The `Index()` method adds a piece of data to the session.</span></span>

```csharp
Session.Add("visited", "true"); 
```

<span data-ttu-id="650be-118">`About()` 和 `Contact()` 方法會快取其輸出。</span><span class="sxs-lookup"><span data-stu-id="650be-118">And the `About()` and `Contact()` methods cache their output.</span></span>

```csharp
[OutputCache(Duration = 60)]
```

## <a name="step-2---deploy-to-azure"></a><span data-ttu-id="650be-119">步驟 2 - 部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="650be-119">Step 2 - Deploy to Azure</span></span>
<span data-ttu-id="650be-120">在此步驟中，您將建立 Azure Web 應用程式，然後在其中部署範例 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-120">In this step, you create an Azure web app and deploy your sample ASP.NET application to it.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="650be-121">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="650be-121">Create a resource group</span></span>   
<span data-ttu-id="650be-122">使用 [az group create](https://docs.microsoft.com/cli/azure/group#create) 在西歐區域建立[資源群組](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="650be-122">Use [az group create](https://docs.microsoft.com/cli/azure/group#create) to create a [resource group](../azure-resource-manager/resource-group-overview.md) in the West Europe region.</span></span> <span data-ttu-id="650be-123">您想要一起管理的所有 Azure 資源都放在資源群組中，例如 Web 應用程式和任何 SQL Database 後端。</span><span class="sxs-lookup"><span data-stu-id="650be-123">A resource group is where you put all the Azure resources that you want to manage together, such as the web app and any SQL Database back end.</span></span>

```azurecli
az group create --location "West Europe" --name myResourceGroup
```

<span data-ttu-id="650be-124">若要查看可用於 `---location` 的可能值，請使用 [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) 命令。</span><span class="sxs-lookup"><span data-stu-id="650be-124">To see what possible values you can use for `---location`, use the [az appservice list-locations](https://docs.microsoft.com/en-us/cli/azure/appservice#list-locations) command.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="650be-125">建立應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="650be-125">Create an App Service plan</span></span>
<span data-ttu-id="650be-126">使用 [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) 建立 "B1" [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)</span><span class="sxs-lookup"><span data-stu-id="650be-126">Use [az appservice plan create](https://docs.microsoft.com/en-us/cli/azure/appservice/plan#create) to create a "B1" [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span> 

```azurecli
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku B1
```

<span data-ttu-id="650be-127">App Service 方案是縮放單位，可包含您想在相同 App Service 基礎結構上一起相應增加或相應放大的應用程式，不限數目。</span><span class="sxs-lookup"><span data-stu-id="650be-127">An App Service plan is a scale unit, which can include any number of apps that you want to scale up or out together over the same App Service infrastructure.</span></span> <span data-ttu-id="650be-128">每個方案也被指派[定價層](https://azure.microsoft.com/en-us/pricing/details/app-service/)。</span><span class="sxs-lookup"><span data-stu-id="650be-128">Each plan is also assigned a [pricing tier](https://azure.microsoft.com/en-us/pricing/details/app-service/).</span></span> <span data-ttu-id="650be-129">較高層包括更好的硬體和更多功能，例如更多相應放大的執行個體。</span><span class="sxs-lookup"><span data-stu-id="650be-129">Higher tiers include better hardware and more features, such as more scale-out instances.</span></span>

<span data-ttu-id="650be-130">本教學課程中，B1 是可相應放大至三個執行個體的最低層。</span><span class="sxs-lookup"><span data-stu-id="650be-130">For this tutorial, B1 is the minimum tier that enables scale out to three instances.</span></span> <span data-ttu-id="650be-131">稍後，您隨時可以執行 [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update)，在定價層上移或下移您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-131">You can always move your app up or down the pricing tier later by running [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update).</span></span> 

### <a name="create-a-web-app"></a><span data-ttu-id="650be-132">建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-132">Create a web app</span></span>
<span data-ttu-id="650be-133">使用 [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)，以 `$appName` 中的唯一名稱建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-133">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a web app with a unique name in `$appName`.</span></span>

```azurecli
$appName = "<replace-with-a-unique-name>"
az appservice web create --name $appName --resource-group myResourceGroup --plan myAppServicePlan
```

### <a name="set-deployment-credentials"></a><span data-ttu-id="650be-134">設定部署認證</span><span class="sxs-lookup"><span data-stu-id="650be-134">Set deployment credentials</span></span>
<span data-ttu-id="650be-135">使用 [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) 為 App Service 設定您的帳戶等級部署認證。</span><span class="sxs-lookup"><span data-stu-id="650be-135">Use [az appservice web deployment user set](https://docs.microsoft.com/en-us/cli/azure/appservice/web/deployment/user#set) to set your account-level deployment credentials for App Service.</span></span>

```azurecli
az appservice web deployment user set --user-name <letters-numbers> --password <mininum-8-char-captital-lowercase-letters-numbers>
```

### <a name="configure-git-deployment"></a><span data-ttu-id="650be-136">設定 Git 部署</span><span class="sxs-lookup"><span data-stu-id="650be-136">Configure Git deployment</span></span>
<span data-ttu-id="650be-137">使用 [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) 設定本機 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="650be-137">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName --resource-group myResourceGroup
```

<span data-ttu-id="650be-138">此命令會產生如下的輸出︰</span><span class="sxs-lookup"><span data-stu-id="650be-138">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="650be-139">使用傳回的 URL 來設定 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="650be-139">Use the returned URL to configure your Git remote.</span></span> <span data-ttu-id="650be-140">下列命令使用上述的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="650be-140">The following command uses the preceding output example.</span></span>

```powershell
git remote add azure https://user123@myuniqueappname.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-the-sample-application"></a><span data-ttu-id="650be-141">部署範例應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-141">Deploy the sample application</span></span>
<span data-ttu-id="650be-142">您現在已準備好部署範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-142">You are now ready to deploy your sample application.</span></span> <span data-ttu-id="650be-143">執行 `git push`。</span><span class="sxs-lookup"><span data-stu-id="650be-143">Run `git push`.</span></span>

```powershell
git push azure master
```

<span data-ttu-id="650be-144">提示您輸入密碼時，請使用您執行 `az appservice web deployment user set` 時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="650be-144">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-azure-web-app"></a><span data-ttu-id="650be-145">瀏覽至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-145">Browse to Azure web app</span></span>
<span data-ttu-id="650be-146">使用 [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse)查看您正在 Azure 中執行的應用程式，請執行這個命令。</span><span class="sxs-lookup"><span data-stu-id="650be-146">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see your app running live in Azure, run this command.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-3---connect-to-redis"></a><span data-ttu-id="650be-147">步驟 3 - 連線至 Redis</span><span class="sxs-lookup"><span data-stu-id="650be-147">Step 3 - Connect to Redis</span></span>
<span data-ttu-id="650be-148">在此步驟中，您要將 Azure Redis 快取設定為外部、共置的快取給 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-148">In this step, you set up Azure Redis Cache as an external, colocated cache to your Azure web app.</span></span> <span data-ttu-id="650be-149">您可以快速利用 Redis 來快取頁面輸出。</span><span class="sxs-lookup"><span data-stu-id="650be-149">You can quickly utilize Redis to cache your page output.</span></span> <span data-ttu-id="650be-150">此外，當您稍後相應放大 Web 應用程式時，Redis 會協助您跨多個執行個體可靠地保存使用者工作階段。</span><span class="sxs-lookup"><span data-stu-id="650be-150">In addition, when you scale out your web apps later, Redis helps you persist user sessions across multiple instances reliably.</span></span>

### <a name="create-an-azure-redis-cache"></a><span data-ttu-id="650be-151">建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="650be-151">Create an Azure Redis Cache</span></span>
<span data-ttu-id="650be-152">使用 [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) 建立 Azure Redis 快取和儲存 JSON 輸出。</span><span class="sxs-lookup"><span data-stu-id="650be-152">Use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create an Azure Redis Cache and save the JSON output.</span></span> <span data-ttu-id="650be-153">在 `$cacheName` 中使用唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="650be-153">Use a unique name in `$cacheName`.</span></span>

```powershell
$cacheName = "<replace-with-a-unique-cache-name>"
$redis = (az redis create --name $cacheName --resource-group myResourceGroup --location "West Europe" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

### <a name="configure-the-application-to-use-redis"></a><span data-ttu-id="650be-154">將應用程式設定為使用 Redis</span><span class="sxs-lookup"><span data-stu-id="650be-154">Configure the application to use Redis</span></span>
<span data-ttu-id="650be-155">格式化快取的連接字串。</span><span class="sxs-lookup"><span data-stu-id="650be-155">Format the connection string for your cache.</span></span>

```powershell
$connstring = "$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False"
$connstring 
```

<span data-ttu-id="650be-156">第二行應該會產生如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="650be-156">The second line should give you an output that looks like this:</span></span>

```
mycachename.redis.cache.windows.net:6380,password=/rQP/TLz1mrEPpmh9b/gnfns/t9vBRXqXn3i1RwBjGA=,ssl=True,abortConnect=False
```

<span data-ttu-id="650be-157">在 Visual Studio 中，在專案根目錄中建立名為 `redis.config` 的 Web 組態檔並貼入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="650be-157">In Visual Studio, create a web configuration file in your project root called `redis.config` and paste the following code into it.</span></span> <span data-ttu-id="650be-158">在 `value` 中，使用 PowerShell 輸出的連接字串。</span><span class="sxs-lookup"><span data-stu-id="650be-158">In `value`, use the connection string from the PowerShell output.</span></span>

```xml
<appSettings>
  <add key="RedisConnection" value="your-azure-redis-cache-connection-string"/>
</appSettings>
```

<span data-ttu-id="650be-159">如果您查看 Git 存放庫中的 `.gitignore` 檔案，您會看到這個檔案已自原始檔控制中排除。</span><span class="sxs-lookup"><span data-stu-id="650be-159">If you look at the `.gitignore` file in your Git repository, you'll see that this file is excluded from source control.</span></span> <span data-ttu-id="650be-160">於是，您的機密資訊獲得安全保障。</span><span class="sxs-lookup"><span data-stu-id="650be-160">That way your sensitive information is kept safe.</span></span> 

<span data-ttu-id="650be-161">開啟 `Web.config`。</span><span class="sxs-lookup"><span data-stu-id="650be-161">Open `Web.config`.</span></span> <span data-ttu-id="650be-162">請注意 `<appSettings file="redis.config">` 元素，它可取得您在 `redis.config` 中建立的設定。</span><span class="sxs-lookup"><span data-stu-id="650be-162">Notice the `<appSettings file="redis.config">` element, which gets the setting you created in `redis.config`.</span></span> 

<span data-ttu-id="650be-163">尋找包含 `<sessionState>` 和 `<caching>` 的註解區段。</span><span class="sxs-lookup"><span data-stu-id="650be-163">Find the commented section that includes `<sessionState>` and `<caching>`.</span></span> <span data-ttu-id="650be-164">將此區段取消註解。</span><span class="sxs-lookup"><span data-stu-id="650be-164">Uncomment this section.</span></span>

![](./media/app-service-web-tutorial-hyper-scale-app/redisproviders.png)

<span data-ttu-id="650be-165">此程式碼會尋找您在 `RedisConnection` 中定義的 Redis 連接字串。</span><span class="sxs-lookup"><span data-stu-id="650be-165">This code looks for the Redis connection string you defined in `RedisConnection`.</span></span> 

<span data-ttu-id="650be-166">您的應用程式現在會使用 Redis 管理工作階段和快取。</span><span class="sxs-lookup"><span data-stu-id="650be-166">Your application now uses Redis to manage sessions and caching.</span></span> <span data-ttu-id="650be-167">輸入 `F5` 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-167">Type `F5` to run the application.</span></span> <span data-ttu-id="650be-168">喜歡的話，您可以下載 Redis 管理用戶端，以視覺化方式檢視現在已儲存至快取的資料。</span><span class="sxs-lookup"><span data-stu-id="650be-168">If you like, you can download a Redis management client to visualize the data that is now saved to the cache.</span></span>

### <a name="configure-the-connection-string-in-azure"></a><span data-ttu-id="650be-169">在 Azure 中設定連接字串。</span><span class="sxs-lookup"><span data-stu-id="650be-169">Configure the connection string in Azure</span></span>

<span data-ttu-id="650be-170">若要讓應用程式在 Azure 中運作，您需要在 Azure Web 應用程式中設定相同的 Redis 連接字串。</span><span class="sxs-lookup"><span data-stu-id="650be-170">For your application to work in Azure, you need to configure the same Redis connection string in your Azure web app.</span></span> <span data-ttu-id="650be-171">因為 `redis.config` 不是在原始檔控制中維護，它不會在您執行 Git 部署時部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="650be-171">Since `redis.config` is not maintained in source control, it is not deployed to Azure when you run Git deployment.</span></span>

<span data-ttu-id="650be-172">使用 [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) 新增相同名稱的連接字串 (`RedisConnection`)。</span><span class="sxs-lookup"><span data-stu-id="650be-172">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add the connection string with the same name (`RedisConnection`).</span></span>

<span data-ttu-id="650be-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="650be-173">az appservice web config appsettings update --settings "RedisConnection=$connstring" --name $appName --resource-group myResourceGroup</span></span>

<span data-ttu-id="650be-174">請記住，`$connstring` 包含格式化的連接字串。</span><span class="sxs-lookup"><span data-stu-id="650be-174">Remember that `$connstring` contains the formatted connection string.</span></span>

### <a name="redeploy-the-application-to-azure"></a><span data-ttu-id="650be-175">將應用程式重新部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="650be-175">Redeploy the application to Azure</span></span>
<span data-ttu-id="650be-176">使用 Git 命令將您的變更推送至 Azure</span><span class="sxs-lookup"><span data-stu-id="650be-176">Use Git commands to push your changes to Azure</span></span>

```bash
git add .
git commit -m "now use Redis providers"
git push azure master
```

<span data-ttu-id="650be-177">提示您輸入密碼時，請使用您執行 `az appservice web deployment user set` 時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="650be-177">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="650be-178">瀏覽至 Azure Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-178">Browse to the Azure web app</span></span>
<span data-ttu-id="650be-179">使用 [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) 查看 Azure 中生效的變更。</span><span class="sxs-lookup"><span data-stu-id="650be-179">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to see the changes live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName --resource-group myResourceGroup
```

## <a name="step-4---scale-to-multiple-instances"></a><span data-ttu-id="650be-180">步驟 4 - 擴充至多個執行個體</span><span class="sxs-lookup"><span data-stu-id="650be-180">Step 4 - Scale to multiple instances</span></span>
<span data-ttu-id="650be-181">App Service 方案是 Azure Web 應用程式的縮放單位。</span><span class="sxs-lookup"><span data-stu-id="650be-181">The App Service plan is the scale unit for your Azure web apps.</span></span> <span data-ttu-id="650be-182">若要相應放大的 Web 應用程式，您可以擴充 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="650be-182">To scale out your web app, you scale the App Service plan.</span></span>

<span data-ttu-id="650be-183">使用 [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) 將 App Service 方案相應放大至三個執行個體，這是 B1 定價層允許的最大數目。</span><span class="sxs-lookup"><span data-stu-id="650be-183">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale out the App Service plan to three instances, which is the maximum number allowed by the B1 pricing tier.</span></span> <span data-ttu-id="650be-184">請記住，B1 是您稍早建立 App Service 方案時選擇的定價層。</span><span class="sxs-lookup"><span data-stu-id="650be-184">Remember that B1 is the pricing tier that you chose when you created the App Service plan earlier.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --number-of-workers 3 
```

## <a name="step-5---scale-geographically"></a><span data-ttu-id="650be-185">步驟 5 - 異地擴充</span><span class="sxs-lookup"><span data-stu-id="650be-185">Step 5 - Scale geographically</span></span>
<span data-ttu-id="650be-186">異地擴充時，您會在 Azure 雲端的多個區域執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-186">When scaling geographically, you run your app in multiple regions of the Azure cloud.</span></span> <span data-ttu-id="650be-187">這項設定會根據地理位置，進一步平衡應用程式的負載，並將應用程式放在更靠近用戶端瀏覽器的位置，以縮短回應時間。</span><span class="sxs-lookup"><span data-stu-id="650be-187">This setup load-balances your app further based on geography and lowers the response time by placing your app closer to client browsers.</span></span>

<span data-ttu-id="650be-188">在此步驟中，您可以使用 [Azure 流量管理員](https://docs.microsoft.com/en-us/azure/traffic-manager/)，將 ASP.NET Web 應用程式調整至第二個區域。</span><span class="sxs-lookup"><span data-stu-id="650be-188">In this step, you scale your ASP.NET web app to a second region with [Azure Traffic Manager](https://docs.microsoft.com/en-us/azure/traffic-manager/).</span></span> <span data-ttu-id="650be-189">此步驟結束時，您會有一個在西歐執行的 Web 應用程式 (已建立) 和一個在東南亞執行的 Web 應用程式 (尚未建立)。</span><span class="sxs-lookup"><span data-stu-id="650be-189">At the end of the step, you will have a web app running in West Europe (already created) and a web app running in Southeast Asia (not yet created).</span></span> <span data-ttu-id="650be-190">兩個應用程式都從相同的流量管理員 URL 供應。</span><span class="sxs-lookup"><span data-stu-id="650be-190">Both apps will be served from the same Traffic Manager URL.</span></span>

### <a name="scale-up-the-europe-app-to-standard-tier"></a><span data-ttu-id="650be-191">將歐洲應用程式相應增加至標準層</span><span class="sxs-lookup"><span data-stu-id="650be-191">Scale up the Europe app to Standard tier</span></span>
<span data-ttu-id="650be-192">在 App Service 中，需要標準定價層才能與 Azure 流量管理員整合。</span><span class="sxs-lookup"><span data-stu-id="650be-192">In App Service, integration with Azure Traffic Manager requires the Standard pricing tier.</span></span> <span data-ttu-id="650be-193">使用 [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) 將 App Service 方案相應增加至 S1。</span><span class="sxs-lookup"><span data-stu-id="650be-193">Use [az appservice plan update](https://docs.microsoft.com/cli/azure/appservice/plan#update) to scale up your App Service plan to S1.</span></span> 

```azurecli
az appservice plan update --name myAppServicePlan --resource-group myResourceGroup --sku S1
```
### <a name="create-a-traffic-manager-profile"></a><span data-ttu-id="650be-194">建立流量管理員設定檔</span><span class="sxs-lookup"><span data-stu-id="650be-194">Create a Traffic Manager profile</span></span> 
<span data-ttu-id="650be-195">使用 [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) 建立流量管理員設定檔，並新增至資源群組。</span><span class="sxs-lookup"><span data-stu-id="650be-195">Use [az network traffic-manager profile create](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#create) to create a Traffic Manager profile and add it to your resource group.</span></span> <span data-ttu-id="650be-196">在 $dnsName 中使用唯一的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="650be-196">Use a unique DNS name in $dnsName.</span></span>

```azurecli
$dnsName = "<replace-with-unique-dns-name>"
az network traffic-manager profile create --name myTrafficManagerProfile --resource-group myResourceGroup --routing-method Performance --unique-dns-name $dnsName
```

> [!NOTE]
> <span data-ttu-id="650be-197">`--routing-method Performance` 指定此設定檔[將使用者流量路由傳送至最靠近的端點](../traffic-manager/traffic-manager-routing-methods.md)。</span><span class="sxs-lookup"><span data-stu-id="650be-197">`--routing-method Performance` specifies that this profile [routes user traffic to the closest endpoint](../traffic-manager/traffic-manager-routing-methods.md).</span></span>

### <a name="get-the-resource-id-of-the-europe-app"></a><span data-ttu-id="650be-198">取得歐洲應用程式的資源識別碼</span><span class="sxs-lookup"><span data-stu-id="650be-198">Get the resource ID of the Europe app</span></span>
<span data-ttu-id="650be-199">使用 [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) 取得 Web 應用程式的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="650be-199">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app.</span></span>

```azurecli
$appId = az appservice web show --name $appName --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-europe-app"></a><span data-ttu-id="650be-200">新增歐洲應用程式的流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="650be-200">Add a Traffic Manager endpoint for the Europe app</span></span>
<span data-ttu-id="650be-201">使用 [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) 將端點新增至流量管理員設定檔，並使用 Web 應用程式的資源識別碼作為目標。</span><span class="sxs-lookup"><span data-stu-id="650be-201">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add an endpoint to your Traffic Manager profile and use the resource ID of your web app as the target.</span></span>

```azurecli
az network traffic-manager endpoint create --name myWestEuropeEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appId
```

### <a name="get-the-traffic-manager-endpoint-url"></a><span data-ttu-id="650be-202">取得流量管理員端點 URL</span><span class="sxs-lookup"><span data-stu-id="650be-202">Get the Traffic Manager endpoint URL</span></span>
<span data-ttu-id="650be-203">流量管理員設定檔現在有一個端點指向現有的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-203">Your Traffic Manager profile now has an endpoint that points to your existing web app.</span></span> <span data-ttu-id="650be-204">使用 [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) 取得其 URL。</span><span class="sxs-lookup"><span data-stu-id="650be-204">Use [az network traffic-manager profile show](https://docs.microsoft.com/cli/azure/network/traffic-manager/profile#show) to get its URL.</span></span> 

```azurecli
az network traffic-manager profile show --name myTrafficManagerProfile --resource-group myResourceGroup --query dnsConfig.fqdn --output tsv
```

<span data-ttu-id="650be-205">將輸出複製到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="650be-205">Copy the output into your browser.</span></span> <span data-ttu-id="650be-206">您應該會再次看到您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-206">You should see your web app again.</span></span>

### <a name="create-an-azure-redis-cache-in-asia"></a><span data-ttu-id="650be-207">在亞洲建立 Azure Redis 快取</span><span class="sxs-lookup"><span data-stu-id="650be-207">Create an Azure Redis Cache in Asia</span></span>
<span data-ttu-id="650be-208">現在，您要將 Azure Web 應用程式複寫至東南亞區域。</span><span class="sxs-lookup"><span data-stu-id="650be-208">Now, you replicate your Azure web app to the Southeast Asia region.</span></span> <span data-ttu-id="650be-209">若要開始，請使用 [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) 在東南亞建立第二個 Azure Redis 快取。</span><span class="sxs-lookup"><span data-stu-id="650be-209">To start, use [az redis create](https://docs.microsoft.com/en-us/cli/azure/redis#create) to create a second Azure Redis Cache in Southeast Asia.</span></span> <span data-ttu-id="650be-210">此快取和您的應用程式必須共置於亞洲。</span><span class="sxs-lookup"><span data-stu-id="650be-210">This cache needs to be colocated with your app in Asia.</span></span>

```powershell
$redis = (az redis create --name $cacheName-asia --resource-group myResourceGroup --location "Southeast Asia" --sku-capacity 0 --sku-family C --sku-name Basic | ConvertFrom-Json)
```

<span data-ttu-id="650be-211">`--name $cacheName-asia` 將快取命名為西歐快取的名稱，尾碼是 `-asia`。</span><span class="sxs-lookup"><span data-stu-id="650be-211">`--name $cacheName-asia` gives the cache the name of the West Europe cache, with the `-asia` suffix.</span></span>

### <a name="create-an-app-service-plan-in-asia"></a><span data-ttu-id="650be-212">在亞洲建立 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="650be-212">Create an App Service plan in Asia</span></span>
<span data-ttu-id="650be-213">使用 [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create)，以西歐方案使用的相同 S1 層，在東南亞區域建立第二個 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="650be-213">Use [az appservice plan create](https://docs.microsoft.com/cli/azure/appservice/plan#create) to create a second App Service plan in the Southeast Asia region, using the same S1 tier as the West Europe plan.</span></span>

```azurecli
az appservice plan create --name myAppServicePlanAsia --resource-group myResourceGroup --location "Southeast Asia" --sku S1
```

### <a name="create-a-web-app-in-asia"></a><span data-ttu-id="650be-214">在亞洲建立 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-214">Create a web app in Asia</span></span>
<span data-ttu-id="650be-215">使用 [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create)，建立第二個 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-215">Use [az appservice web create](https://docs.microsoft.com/en-us/cli/azure/appservice/web#create) to create a second web app.</span></span>

```azurecli
az appservice web create --name $appName-asia --resource-group myResourceGroup --plan myAppServicePlanAsia
```

<span data-ttu-id="650be-216">`--name $appName-asia` 將應用程式命名為西歐應用程式的名稱，尾碼是 `-asia`。</span><span class="sxs-lookup"><span data-stu-id="650be-216">`--name $appName-asia` gives the app the name of the West Europe app, with the `-asia` suffix.</span></span>

### <a name="configure-the-connection-string-for-redis"></a><span data-ttu-id="650be-217">設定 Redis 的連接字串</span><span class="sxs-lookup"><span data-stu-id="650be-217">Configure the connection string for Redis</span></span>
<span data-ttu-id="650be-218">使用 [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) 將東南亞快取的連接字串新增至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="650be-218">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add to the web app the connection string for the Southeast Asia cache.</span></span>

<span data-ttu-id="650be-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="650be-219">az appservice web config appsettings update --settings "RedisConnection=$($redis.hostname):$($redis.sslPort),password=$($redis.accessKeys.primaryKey),ssl=True,abortConnect=False" --name $appName-asia --resource-group myResourceGroup</span></span>

### <a name="configure-git-deployment-for-the-asia-app"></a><span data-ttu-id="650be-220">設定亞洲應用程式的 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="650be-220">Configure Git deployment for the Asia app.</span></span>
<span data-ttu-id="650be-221">使用 [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) 設定第二個 Web 應用程式的本機 Git 部署。</span><span class="sxs-lookup"><span data-stu-id="650be-221">Use [az appservice web source-control config-local-git](https://docs.microsoft.com/en-us/cli/azure/appservice/web/source-control#config-local-git) to configure local Git deployment for the second web app.</span></span>

```azurecli
az appservice web source-control config-local-git --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="650be-222">此命令會產生如下的輸出︰</span><span class="sxs-lookup"><span data-stu-id="650be-222">This command gives you an output that looks like the following:</span></span>

```json
{
  "url": "https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git"
}
```

<span data-ttu-id="650be-223">使用傳回的 URL 來設定本機存放庫的第二個 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="650be-223">Use the returned URL to configure a second Git remote for your local repository.</span></span> <span data-ttu-id="650be-224">下列命令使用上述的輸出範例。</span><span class="sxs-lookup"><span data-stu-id="650be-224">The following command uses the preceding output example.</span></span>

```bash
git remote add azure-asia https://user123@myuniqueappname-asia.scm.azurewebsites.net/myuniqueappname.git
```

### <a name="deploy-your-sample-application"></a><span data-ttu-id="650be-225">部署範例應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-225">Deploy your sample application</span></span>
<span data-ttu-id="650be-226">執行 `git push` 將範例應用程式部署至第二個 Git 遠端。</span><span class="sxs-lookup"><span data-stu-id="650be-226">Run `git push` to deploy your sample application to the second Git remote.</span></span> 

```bash
git push azure-asia master
```

<span data-ttu-id="650be-227">提示您輸入密碼時，請使用您執行 `az appservice web deployment user set` 時所指定的密碼。</span><span class="sxs-lookup"><span data-stu-id="650be-227">When prompted for password, use the password that you specified when you ran `az appservice web deployment user set`.</span></span>

### <a name="browse-to-the-asia-app"></a><span data-ttu-id="650be-228">瀏覽至亞洲應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-228">Browse to the Asia app</span></span>
<span data-ttu-id="650be-229">使用 [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) 驗證您的應用程式正在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="650be-229">Use [az appservice web browse](https://docs.microsoft.com/en-us/cli/azure/appservice/web#browse) to verify that your app is running live in Azure.</span></span>

```azurecli
az appservice web browse --name $appName-asia --resource-group myResourceGroup
```

### <a name="get-the-resource-id-of-the-asia-app"></a><span data-ttu-id="650be-230">取得亞洲應用程式的資源識別碼</span><span class="sxs-lookup"><span data-stu-id="650be-230">Get the resource ID of the Asia app</span></span>
<span data-ttu-id="650be-231">使用 [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) 取得 Web 應用程式在東南亞的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="650be-231">Use [az appservice web show](https://docs.microsoft.com/en-us/cli/azure/appservice/web#show) to get the resource ID of your web app in Southeast Asia.</span></span>

```azurecli
$appIdAsia = az appservice web show --name $appName-asia --resource-group myResourceGroup --query id --output tsv
```

### <a name="add-a-traffic-manager-endpoint-for-the-asia-app"></a><span data-ttu-id="650be-232">新增亞洲應用程式的流量管理員端點</span><span class="sxs-lookup"><span data-stu-id="650be-232">Add a Traffic Manager endpoint for the Asia app</span></span>
<span data-ttu-id="650be-233">使用 [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) 將第二個端點新增至流量管理員設定檔。</span><span class="sxs-lookup"><span data-stu-id="650be-233">Use [az network traffic-manager endpoint create](https://docs.microsoft.com/cli/azure/network/traffic-manager/endpoint#create) to add a second endpoint to the Traffic Manager profile.</span></span>

```azurecli
az network traffic-manager endpoint create --name myAsiaEndpoint --profile-name myTrafficManagerProfile --resource-group myResourceGroup --type azureEndpoints --target-resource-id $appIdAsia
```

### <a name="add-region-identifier-to-web-apps"></a><span data-ttu-id="650be-234">將區域識別碼新增至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="650be-234">Add region identifier to web apps</span></span>
<span data-ttu-id="650be-235">使用 [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) 新增區域特定的環境變數。</span><span class="sxs-lookup"><span data-stu-id="650be-235">Use [az appservice web config appsettings update](https://docs.microsoft.com/cli/azure/appservice/web/config/appsettings#update) to add a region-specific environment variable.</span></span>

```azurecli
az appservice web config appsettings update --settings "Region=West Europe" --name $appName --resource-group myResourceGroup
az appservice web config appsettings update --settings "Region=Southeast Asia" --name $appName-asia --resource-group myResourceGroup
```

<span data-ttu-id="650be-236">您的應用程式碼已使用此應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="650be-236">Your application code already uses this application setting.</span></span> <span data-ttu-id="650be-237">請看 `HighScaleApp\Views\Home\Index.cshtml`。</span><span class="sxs-lookup"><span data-stu-id="650be-237">Take a look at `HighScaleApp\Views\Home\Index.cshtml`.</span></span>

### <a name="complete"></a><span data-ttu-id="650be-238">完成！</span><span class="sxs-lookup"><span data-stu-id="650be-238">Complete!</span></span>

<span data-ttu-id="650be-239">現在，嘗試從不同地理區域的瀏覽器，存取流量管理員設定檔的 URL。</span><span class="sxs-lookup"><span data-stu-id="650be-239">Now, try to access the URL of your Traffic Manager profile from browsers in different geographical regions.</span></span> <span data-ttu-id="650be-240">來自歐洲的用戶端瀏覽器應該會顯示「ASP.NET 西歐」，來自亞洲的用戶端瀏覽器應該會顯示「ASP.NET 東南亞」。</span><span class="sxs-lookup"><span data-stu-id="650be-240">Client browsers from Europe should show "ASP.NET West Europe", and client browser from Asia should show "ASP.NET Southeast Asia."</span></span>

## <a name="more-resources"></a><span data-ttu-id="650be-241">其他資源</span><span class="sxs-lookup"><span data-stu-id="650be-241">More resources</span></span>
