---
title: "Azure App Service 上裝載的 aaaHigh 密度 |Microsoft 文件"
description: "Azure App Service 上的高密度託管"
author: btardif
manager: erikre
editor: 
services: app-service\web
documentationcenter: 
ms.assetid: a903cb78-4927-47b0-8427-56412c4e3e64
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 06/12/2017
ms.author: byvinyal
ms.openlocfilehash: a10cb81ace13ba6992b572a44361061ecf72b266
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="c005d-103">Azure App Service 上的高密度託管</span><span class="sxs-lookup"><span data-stu-id="c005d-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="c005d-104">使用應用程式服務時，您的應用程式就可以分隔由兩個概念配置 tooit hello 容量：</span><span class="sxs-lookup"><span data-stu-id="c005d-104">When using App Service, your application is decoupled from hello capacity allocated tooit by two concepts:</span></span>

* <span data-ttu-id="c005d-105">**hello 應用程式：**代表 hello 應用程式和其執行階段組態。</span><span class="sxs-lookup"><span data-stu-id="c005d-105">**hello Application:** Represents hello app and its runtime configuration.</span></span> <span data-ttu-id="c005d-106">例如，它包含 hello hello 執行階段的.NET 版本應該載入，hello 應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="c005d-106">For example, it includes hello version of .NET that hello runtime should load, hello app settings.</span></span>
* <span data-ttu-id="c005d-107">**App Service 方案的 hello:**定義 hello 特性 hello 容量、 可用的功能集和位置的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c005d-107">**hello App Service Plan:** Defines hello characteristics of hello capacity, available feature set, and locality of hello application.</span></span> <span data-ttu-id="c005d-108">例如，特性可能是大型 (四個核心) 機器、四個執行個體、美國東部的進階功能。</span><span class="sxs-lookup"><span data-stu-id="c005d-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="c005d-109">應用程式連結的 tooan App Service 方案，但是 App Service 方案可以提供容量 tooone 或更多應用程式。</span><span class="sxs-lookup"><span data-stu-id="c005d-109">An app is always linked tooan App Service plan, but an App Service plan can provide capacity tooone or more apps.</span></span>

<span data-ttu-id="c005d-110">如此一來，hello 平台提供 hello 彈性 tooisolate 單一應用程式，或有多個共用資源的共用 App Service 方案的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c005d-110">As a result, hello platform provides hello flexibility tooisolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="c005d-111">不過，當多個應用程式共用 App Service 方案時，該 App Service 方案的每個執行個體上便會執行該應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c005d-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="c005d-112">每一應用程式調整</span><span class="sxs-lookup"><span data-stu-id="c005d-112">Per app scaling</span></span>
<span data-ttu-id="c005d-113">*每一應用程式調整* 是可在 App Service 方案層級啟用，然後以每一應用程式為基礎來使用的功能。</span><span class="sxs-lookup"><span data-stu-id="c005d-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="c005d-114">每一應用程式調整會獨立縮放應用程式，不受裝載它的 App Service 方案所影響。</span><span class="sxs-lookup"><span data-stu-id="c005d-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="c005d-115">如此一來，應用程式服務計劃可以縮放 too10 執行個體，但應用程式可以設定 toouse 只有五個。</span><span class="sxs-lookup"><span data-stu-id="c005d-115">This way, an App Service plan can be scaled too10 instances, but an app can be set toouse only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="c005d-116">只有「進階」SKU App Service 方案才能使用個別應用程式調整</span><span class="sxs-lookup"><span data-stu-id="c005d-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="c005d-117">使用 PowerShell 進行個別應用程式調整</span><span class="sxs-lookup"><span data-stu-id="c005d-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="c005d-118">您可以建立計劃設定為*每個應用程式調整*計劃，透過傳入 hello```-perSiteScaling $true```屬性 toohello ```New-AzureRmAppServicePlan``` commandlet</span><span class="sxs-lookup"><span data-stu-id="c005d-118">You can create a plan configured as a *Per app scaling* plan by passing in hello ```-perSiteScaling $true``` attribute toohello ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="c005d-119">如果您想 tooupdate 現有的應用程式服務計劃 toouse 這項功能：</span><span class="sxs-lookup"><span data-stu-id="c005d-119">If you want tooupdate an existing App Service plan toouse this feature:</span></span> 

- <span data-ttu-id="c005d-120">取得 hello 目標計劃```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="c005d-120">get hello target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="c005d-121">修改本機 hello 屬性```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="c005d-121">modifying hello property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="c005d-122">張貼您的變更回復 tooazure```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="c005d-122">posting your changes back tooazure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get hello new App Service Plan and modify hello "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify hello local copy toouse "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back tooazure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="c005d-123">在 hello 應用程式層級中，我們需要 tooconfigure hello 數目 hello 應用程式可以在 hello 應用程式服務方案中使用的執行個體。</span><span class="sxs-lookup"><span data-stu-id="c005d-123">At hello app level, we need tooconfigure hello number of instances hello app can use in hello app service plan.</span></span>

<span data-ttu-id="c005d-124">在下面 hello 範例中，hello 應用程式會是有限的 tootwo 不論多少個執行個體的執行個體 hello 基礎應用程式服務方案的規模出。</span><span class="sxs-lookup"><span data-stu-id="c005d-124">In hello example below, hello app is limited tootwo instances regardless of how many instances hello underlying app service plan scales out to.</span></span>

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="c005d-125">$newapp.SiteConfig.NumberOfWorkers 不同於 $newapp.MaxNumberOfWorkers。</span><span class="sxs-lookup"><span data-stu-id="c005d-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="c005d-126">每個應用程式擴充會使用 $newapp。SiteConfig.NumberOfWorkers toodetermine hello 小數位數的特性 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c005d-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers toodetermine hello scale characteristics of hello app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="c005d-127">使用 Azure Resource Manager 進行個別應用程式調整</span><span class="sxs-lookup"><span data-stu-id="c005d-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="c005d-128">hello 下列*Azure Resource Manager 範本*建立：</span><span class="sxs-lookup"><span data-stu-id="c005d-128">hello following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="c005d-129">向外延展 too10 執行個體的應用程式服務方案</span><span class="sxs-lookup"><span data-stu-id="c005d-129">An App Service plan that's scaled out too10 instances</span></span>
- <span data-ttu-id="c005d-130">應用程式設定 tooscale tooa 最大的五個執行個體。</span><span class="sxs-lookup"><span data-stu-id="c005d-130">an app that's configured tooscale tooa max of five instances.</span></span>

<span data-ttu-id="c005d-131">hello 應用程式服務方案設定 hello **PerSiteScaling**屬性 tootrue ```"perSiteScaling": true```。</span><span class="sxs-lookup"><span data-stu-id="c005d-131">hello App Service plan is setting hello **PerSiteScaling** property tootrue ```"perSiteScaling": true```.</span></span> <span data-ttu-id="c005d-132">hello 應用程式正在設定 hello**數目的工作者**toouse too5 ```"properties": { "numberOfWorkers": "5" }```。</span><span class="sxs-lookup"><span data-stu-id="c005d-132">hello app is setting hello **number of workers** toouse too5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

```
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters":{
        "appServicePlanName": { "type": "string" },
        "appName": { "type": "string" }
        },
    "resources": [
    {
        "comments": "App Service Plan with per site perSiteScaling = true",
        "type": "Microsoft.Web/serverFarms",
        "sku": {
            "name": "P1",
            "tier": "Premium",
            "size": "P1",
            "family": "P",
            "capacity": 10
            },
        "name": "[parameters('appServicePlanName')]",
        "apiVersion": "2015-08-01",
        "location": "West US",
        "properties": {
            "name": "[parameters('appServicePlanName')]",
            "perSiteScaling": true
        }
    },
    {
        "type": "Microsoft.Web/sites",
        "name": "[parameters('appName')]",
        "apiVersion": "2015-08-01-preview",
        "location": "West US",
        "dependsOn": [ "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" ],
        "properties": { "serverFarmId": "[resourceId('Microsoft.Web/serverFarms', parameters('appServicePlanName'))]" },
        "resources": [ {
                "comments": "",
                "type": "config",
                "name": "web",
                "apiVersion": "2015-08-01",
                "location": "West US",
                "dependsOn": [ "[resourceId('Microsoft.Web/Sites', parameters('appName'))]" ],
                "properties": { "numberOfWorkers": "5" }
            } ]
        }]
}
```

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="c005d-133">高密度裝載的建議組態</span><span class="sxs-lookup"><span data-stu-id="c005d-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="c005d-134">每個應用程式調整是全域 Azure 區域和 App Service Environment 中啟用的功能。</span><span class="sxs-lookup"><span data-stu-id="c005d-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="c005d-135">不過，hello 建議策略是使用應用程式服務環境 tootake 利用進階的功能和容量的 hello 較大的集區。</span><span class="sxs-lookup"><span data-stu-id="c005d-135">However, hello recommended strategy is to use App Service Environments tootake advantage of their advanced features and hello larger pools of capacity.</span></span>  

<span data-ttu-id="c005d-136">請遵循這些步驟 tooconfigure 高密度裝載您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="c005d-136">Follow these steps tooconfigure high density hosting for your apps:</span></span>

1. <span data-ttu-id="c005d-137">設定 App Service 環境的 hello 和選擇是專用的 toohello 較高的密度，裝載案例的背景工作集區。</span><span class="sxs-lookup"><span data-stu-id="c005d-137">Configure hello App Service Environment and choose a worker pool that is dedicated toohello high density hosting scenario.</span></span>
1. <span data-ttu-id="c005d-138">建立單一的應用程式服務方案，並調整它 toouse 所有 hello hello 背景工作集區上的可用容量。</span><span class="sxs-lookup"><span data-stu-id="c005d-138">Create a single App Service plan, and scale it toouse all hello available capacity on hello worker pool.</span></span>
1. <span data-ttu-id="c005d-139">設定 hello PerSiteScaling 旗標 tootrue hello 應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="c005d-139">Set hello PerSiteScaling flag tootrue on hello App Service plan.</span></span>
1. <span data-ttu-id="c005d-140">新的應用程式會建立並指派 toothat 應用程式服務計劃與**numberOfWorkers**屬性設定太**1**。</span><span class="sxs-lookup"><span data-stu-id="c005d-140">New apps are created and assigned toothat App Service plan with the **numberOfWorkers** property set too**1**.</span></span> <span data-ttu-id="c005d-141">使用此設定會產生 hello 最高密度可能此背景工作集區上。</span><span class="sxs-lookup"><span data-stu-id="c005d-141">Using this configuration yields hello highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="c005d-142">hello 背景工作數目可以視需要設定獨立每個應用程式 toogrant 其他資源。</span><span class="sxs-lookup"><span data-stu-id="c005d-142">hello number of workers can be configured independently per app toogrant additional resources as needed.</span></span> <span data-ttu-id="c005d-143">例如：</span><span class="sxs-lookup"><span data-stu-id="c005d-143">For example:</span></span>
    - <span data-ttu-id="c005d-144">高用量應用程式可以設定**numberOfWorkers**太**3** toohave 多個處理針對該應用程式的容量。</span><span class="sxs-lookup"><span data-stu-id="c005d-144">A high-use app can set **numberOfWorkers** too**3** toohave more processing capacity for that app.</span></span> 
    - <span data-ttu-id="c005d-145">低使用率的應用程式會設定**numberOfWorkers**太**1**。</span><span class="sxs-lookup"><span data-stu-id="c005d-145">Low-use apps would set **numberOfWorkers** too**1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c005d-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c005d-146">Next Steps</span></span>

- [<span data-ttu-id="c005d-147">Azure App Service 方案深入概觀</span><span class="sxs-lookup"><span data-stu-id="c005d-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="c005d-148">簡介 tooApp Service 環境</span><span class="sxs-lookup"><span data-stu-id="c005d-148">Introduction tooApp Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)
