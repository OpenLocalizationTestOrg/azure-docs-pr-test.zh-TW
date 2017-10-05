---
title: "Azure App Service 上的高密度裝載 | Microsoft Docs"
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
ms.openlocfilehash: 459a310a719695f6366470976d857ec2f9d6f4a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="high-density-hosting-on-azure-app-service"></a><span data-ttu-id="98fe5-103">Azure App Service 上的高密度託管</span><span class="sxs-lookup"><span data-stu-id="98fe5-103">High density hosting on Azure App Service</span></span>
<span data-ttu-id="98fe5-104">在使用 App Service 時，應用程式會經由兩種概念與其所配置的容量分離：</span><span class="sxs-lookup"><span data-stu-id="98fe5-104">When using App Service, your application is decoupled from the capacity allocated to it by two concepts:</span></span>

* <span data-ttu-id="98fe5-105">**應用程式︰** 代表應用程式和其執行階段組態。</span><span class="sxs-lookup"><span data-stu-id="98fe5-105">**The Application:** Represents the app and its runtime configuration.</span></span> <span data-ttu-id="98fe5-106">例如，它包含執行階段應載入的 .NET 版本、應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="98fe5-106">For example, it includes the version of .NET that the runtime should load, the app settings.</span></span>
* <span data-ttu-id="98fe5-107">**App Service 方案︰** 定義容量、可用功能集和應用程式位置的特性。</span><span class="sxs-lookup"><span data-stu-id="98fe5-107">**The App Service Plan:** Defines the characteristics of the capacity, available feature set, and locality of the application.</span></span> <span data-ttu-id="98fe5-108">例如，特性可能是大型 (四個核心) 機器、四個執行個體、美國東部的進階功能。</span><span class="sxs-lookup"><span data-stu-id="98fe5-108">For example, characteristics might be large (four cores) machine, four instances, Premium features in East US.</span></span>

<span data-ttu-id="98fe5-109">應用程式一律會連結至 App Service 方案，但 App Service 方案可以提供容量給一或多個應用程式。</span><span class="sxs-lookup"><span data-stu-id="98fe5-109">An app is always linked to an App Service plan, but an App Service plan can provide capacity to one or more apps.</span></span>

<span data-ttu-id="98fe5-110">因此，平台可提供隔離單一應用程式的彈性，或透過共用 App Service 方案而讓多個應用程式共用資源。</span><span class="sxs-lookup"><span data-stu-id="98fe5-110">As a result, the platform provides the flexibility to isolate a single app or have multiple apps share resources by sharing an App Service plan.</span></span>

<span data-ttu-id="98fe5-111">不過，當多個應用程式共用 App Service 方案時，該 App Service 方案的每個執行個體上便會執行該應用程式的執行個體。</span><span class="sxs-lookup"><span data-stu-id="98fe5-111">However, when multiple apps share an App Service plan, an instance of that app runs on every instance of that App Service plan.</span></span>

## <a name="per-app-scaling"></a><span data-ttu-id="98fe5-112">每一應用程式調整</span><span class="sxs-lookup"><span data-stu-id="98fe5-112">Per app scaling</span></span>
<span data-ttu-id="98fe5-113">*每一應用程式調整* 是可在 App Service 方案層級啟用，然後以每一應用程式為基礎來使用的功能。</span><span class="sxs-lookup"><span data-stu-id="98fe5-113">*Per app scaling* is a feature that can be enabled at the App Service plan level and then used per application.</span></span>

<span data-ttu-id="98fe5-114">每一應用程式調整會獨立縮放應用程式，不受裝載它的 App Service 方案所影響。</span><span class="sxs-lookup"><span data-stu-id="98fe5-114">Per app scaling scales an app independently from the App Service plan that hosts it.</span></span> <span data-ttu-id="98fe5-115">如此一來，App Service 方案可以調整為 10 個執行個體，但是應用程式可以設定為僅使用五個。</span><span class="sxs-lookup"><span data-stu-id="98fe5-115">This way, an App Service plan can be scaled to 10 instances, but an app can be set to use only five.</span></span>

   >[!NOTE]
   ><span data-ttu-id="98fe5-116">只有「進階」SKU App Service 方案才能使用個別應用程式調整</span><span class="sxs-lookup"><span data-stu-id="98fe5-116">Per app scaling is available only for **Premium** SKU App Service plans</span></span>
   >

### <a name="per-app-scaling-using-powershell"></a><span data-ttu-id="98fe5-117">使用 PowerShell 進行個別應用程式調整</span><span class="sxs-lookup"><span data-stu-id="98fe5-117">Per app scaling using PowerShell</span></span>

<span data-ttu-id="98fe5-118">您可以透過將 ```-perSiteScaling $true``` 屬性傳遞給 ```New-AzureRmAppServicePlan``` Commandlet，建立一個設定為「個別應用程式調整」方案的方案</span><span class="sxs-lookup"><span data-stu-id="98fe5-118">You can create a plan configured as a *Per app scaling* plan by passing in the ```-perSiteScaling $true``` attribute to the ```New-AzureRmAppServicePlan``` commandlet</span></span>

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

<span data-ttu-id="98fe5-119">如果您想要將現有的 App Service 方案更新成使用此功能：</span><span class="sxs-lookup"><span data-stu-id="98fe5-119">If you want to update an existing App Service plan to use this feature:</span></span> 

- <span data-ttu-id="98fe5-120">取得目標方案 ```Get-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="98fe5-120">get the target plan ```Get-AzureRmAppServicePlan```</span></span>
- <span data-ttu-id="98fe5-121">在本機修改屬性 ```$newASP.PerSiteScaling = $true```</span><span class="sxs-lookup"><span data-stu-id="98fe5-121">modifying the property locally ```$newASP.PerSiteScaling = $true```</span></span>
- <span data-ttu-id="98fe5-122">將您的變更張貼回 Azure ```Set-AzureRmAppServicePlan```</span><span class="sxs-lookup"><span data-stu-id="98fe5-122">posting your changes back to azure ```Set-AzureRmAppServicePlan```</span></span> 

```
# Get the new App Service Plan and modify the "PerSiteScaling" property.
$newASP = Get-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan
$newASP

#Modify the local copy to use "PerSiteScaling" property.
$newASP.PerSiteScaling = $true
$newASP
    
#Post updated app service plan back to azure
Set-AzureRmAppServicePlan $newASP
```

<span data-ttu-id="98fe5-123">在應用程式層級，我們需要設定應用程式在 App Service 方案中可以使用的執行個體數目。</span><span class="sxs-lookup"><span data-stu-id="98fe5-123">At the app level, we need to configure the number of instances the app can use in the app service plan.</span></span>

<span data-ttu-id="98fe5-124">在以下範例中，應用程式限制為 2 個執行個體，不論其基礎 App Service 方案的規模相應放大到多少個執行個體。</span><span class="sxs-lookup"><span data-stu-id="98fe5-124">In the example below, the app is limited to two instances regardless of how many instances the underlying app service plan scales out to.</span></span>

```
# Get the app we want to configure to use "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify the NumberOfWorkers setting to the desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back to azure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> <span data-ttu-id="98fe5-125">$newapp.SiteConfig.NumberOfWorkers 不同於 $newapp.MaxNumberOfWorkers。</span><span class="sxs-lookup"><span data-stu-id="98fe5-125">$newapp.SiteConfig.NumberOfWorkers is different form $newapp.MaxNumberOfWorkers.</span></span> <span data-ttu-id="98fe5-126">每個應用程式調整會使用 $newapp.SiteConfig.NumberOfWorkers 來決定應用程式的調整特性。</span><span class="sxs-lookup"><span data-stu-id="98fe5-126">Per app scaling uses $newapp.SiteConfig.NumberOfWorkers to determine the scale characteristics of the app.</span></span>

### <a name="per-app-scaling-using-azure-resource-manager"></a><span data-ttu-id="98fe5-127">使用 Azure Resource Manager 進行個別應用程式調整</span><span class="sxs-lookup"><span data-stu-id="98fe5-127">Per app scaling using Azure Resource Manager</span></span>

<span data-ttu-id="98fe5-128">下列「Azure Resource Manager 範本」會建立：</span><span class="sxs-lookup"><span data-stu-id="98fe5-128">The following *Azure Resource Manager template* creates:</span></span>

- <span data-ttu-id="98fe5-129">規模相應放大到 10 個執行個體的 App Service 方案</span><span class="sxs-lookup"><span data-stu-id="98fe5-129">An App Service plan that's scaled out to 10 instances</span></span>
- <span data-ttu-id="98fe5-130">已設定為將上限調整成 5 個執行個體的應用程式。</span><span class="sxs-lookup"><span data-stu-id="98fe5-130">an app that's configured to scale to a max of five instances.</span></span>

<span data-ttu-id="98fe5-131">App Service 方案會將 **PerSiteScaling** 屬性設為 true (```"perSiteScaling": true```)。</span><span class="sxs-lookup"><span data-stu-id="98fe5-131">The App Service plan is setting the **PerSiteScaling** property to true ```"perSiteScaling": true```.</span></span> <span data-ttu-id="98fe5-132">應用程式會將要使用的「背景工作角色數目」設定為 5 (```"properties": { "numberOfWorkers": "5" }```)。</span><span class="sxs-lookup"><span data-stu-id="98fe5-132">The app is setting the **number of workers** to use to 5 ```"properties": { "numberOfWorkers": "5" }```.</span></span>

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

## <a name="recommended-configuration-for-high-density-hosting"></a><span data-ttu-id="98fe5-133">高密度裝載的建議組態</span><span class="sxs-lookup"><span data-stu-id="98fe5-133">Recommended configuration for high density hosting</span></span>
<span data-ttu-id="98fe5-134">每個應用程式調整是全域 Azure 區域和 App Service Environment 中啟用的功能。</span><span class="sxs-lookup"><span data-stu-id="98fe5-134">Per app scaling is a feature that is enabled in both global Azure regions and App Service Environments.</span></span> <span data-ttu-id="98fe5-135">不過，建議策略是使用 App Service 環境，以利用其進階功能和較大的容量集區。</span><span class="sxs-lookup"><span data-stu-id="98fe5-135">However, the recommended strategy is to use App Service Environments to take advantage of their advanced features and the larger pools of capacity.</span></span>  

<span data-ttu-id="98fe5-136">請遵循下列步驟來設定應用程式的高密度裝載：</span><span class="sxs-lookup"><span data-stu-id="98fe5-136">Follow these steps to configure high density hosting for your apps:</span></span>

1. <span data-ttu-id="98fe5-137">設定 App Service 環境，並選擇專用於高密度裝載案例的背景工作角色集區。</span><span class="sxs-lookup"><span data-stu-id="98fe5-137">Configure the App Service Environment and choose a worker pool that is dedicated to the high density hosting scenario.</span></span>
1. <span data-ttu-id="98fe5-138">建立單一 App Service 方案，並將其調整為使用背景工作角色集區上所有可用的容量。</span><span class="sxs-lookup"><span data-stu-id="98fe5-138">Create a single App Service plan, and scale it to use all the available capacity on the worker pool.</span></span>
1. <span data-ttu-id="98fe5-139">在 App Service 方案上將 PerSiteScaling 旗標設定為 true。</span><span class="sxs-lookup"><span data-stu-id="98fe5-139">Set the PerSiteScaling flag to true on the App Service plan.</span></span>
1. <span data-ttu-id="98fe5-140">新應用程式會建立並指派給該 App Service 方案，其中 **numberOfWorkers** 屬性會設定為 **1**。</span><span class="sxs-lookup"><span data-stu-id="98fe5-140">New apps are created and assigned to that App Service plan with the **numberOfWorkers** property set to **1**.</span></span> <span data-ttu-id="98fe5-141">使用此設定會產生此背景工作角色集區上所能允許的最高密度。</span><span class="sxs-lookup"><span data-stu-id="98fe5-141">Using this configuration yields the highest density possible on this worker pool.</span></span>
1. <span data-ttu-id="98fe5-142">背景工作角色數目可依每個應用程式單獨設定，以視需要授與額外資源。</span><span class="sxs-lookup"><span data-stu-id="98fe5-142">The number of workers can be configured independently per app to grant additional resources as needed.</span></span> <span data-ttu-id="98fe5-143">例如：</span><span class="sxs-lookup"><span data-stu-id="98fe5-143">For example:</span></span>
    - <span data-ttu-id="98fe5-144">高用量應用程式可以將 **numberOfWorkers** 設定為 **3**，讓該應用程式具有更多的處理容量。</span><span class="sxs-lookup"><span data-stu-id="98fe5-144">A high-use app can set **numberOfWorkers** to **3** to have more processing capacity for that app.</span></span> 
    - <span data-ttu-id="98fe5-145">低用量應用程式會將 **numberOfWorkers** 設定為 **1**。</span><span class="sxs-lookup"><span data-stu-id="98fe5-145">Low-use apps would set **numberOfWorkers** to **1**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98fe5-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="98fe5-146">Next Steps</span></span>

- [<span data-ttu-id="98fe5-147">Azure App Service 方案深入概觀</span><span class="sxs-lookup"><span data-stu-id="98fe5-147">Azure App Service plans in-depth overview</span></span>](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [<span data-ttu-id="98fe5-148">App Service 環境簡介</span><span class="sxs-lookup"><span data-stu-id="98fe5-148">Introduction to App Service Environment</span></span>](../app-service-web/app-service-app-service-environment-intro.md)