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
# <a name="high-density-hosting-on-azure-app-service"></a>Azure App Service 上的高密度託管
使用應用程式服務時，您的應用程式就可以分隔由兩個概念配置 tooit hello 容量：

* **hello 應用程式：**代表 hello 應用程式和其執行階段組態。 例如，它包含 hello hello 執行階段的.NET 版本應該載入，hello 應用程式設定。
* **App Service 方案的 hello:**定義 hello 特性 hello 容量、 可用的功能集和位置的 hello 應用程式。 例如，特性可能是大型 (四個核心) 機器、四個執行個體、美國東部的進階功能。

應用程式連結的 tooan App Service 方案，但是 App Service 方案可以提供容量 tooone 或更多應用程式。

如此一來，hello 平台提供 hello 彈性 tooisolate 單一應用程式，或有多個共用資源的共用 App Service 方案的應用程式。

不過，當多個應用程式共用 App Service 方案時，該 App Service 方案的每個執行個體上便會執行該應用程式的執行個體。

## <a name="per-app-scaling"></a>每一應用程式調整
*每一應用程式調整* 是可在 App Service 方案層級啟用，然後以每一應用程式為基礎來使用的功能。

每一應用程式調整會獨立縮放應用程式，不受裝載它的 App Service 方案所影響。 如此一來，應用程式服務計劃可以縮放 too10 執行個體，但應用程式可以設定 toouse 只有五個。

   >[!NOTE]
   >只有「進階」SKU App Service 方案才能使用個別應用程式調整
   >

### <a name="per-app-scaling-using-powershell"></a>使用 PowerShell 進行個別應用程式調整

您可以建立計劃設定為*每個應用程式調整*計劃，透過傳入 hello```-perSiteScaling $true```屬性 toohello ```New-AzureRmAppServicePlan``` commandlet

```
New-AzureRmAppServicePlan -ResourceGroupName $ResourceGroup -Name $AppServicePlan `
                            -Location $Location `
                            -Tier Premium -WorkerSize Small `
                            -NumberofWorkers 5 -PerSiteScaling $true
```

如果您想 tooupdate 現有的應用程式服務計劃 toouse 這項功能： 

- 取得 hello 目標計劃```Get-AzureRmAppServicePlan```
- 修改本機 hello 屬性```$newASP.PerSiteScaling = $true```
- 張貼您的變更回復 tooazure```Set-AzureRmAppServicePlan``` 

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

在 hello 應用程式層級中，我們需要 tooconfigure hello 數目 hello 應用程式可以在 hello 應用程式服務方案中使用的執行個體。

在下面 hello 範例中，hello 應用程式會是有限的 tootwo 不論多少個執行個體的執行個體 hello 基礎應用程式服務方案的規模出。

```
# Get hello app we want tooconfigure toouse "PerSiteScaling"
$newapp = Get-AzureRmWebApp -ResourceGroupName $ResourceGroup -Name $webapp
    
# Modify hello NumberOfWorkers setting toohello desired value.
$newapp.SiteConfig.NumberOfWorkers = 2
    
# Post updated app back tooazure
Set-AzureRmWebApp $newapp
```

> [!IMPORTANT]
> $newapp.SiteConfig.NumberOfWorkers 不同於 $newapp.MaxNumberOfWorkers。 每個應用程式擴充會使用 $newapp。SiteConfig.NumberOfWorkers toodetermine hello 小數位數的特性 hello 應用程式。

### <a name="per-app-scaling-using-azure-resource-manager"></a>使用 Azure Resource Manager 進行個別應用程式調整

hello 下列*Azure Resource Manager 範本*建立：

- 向外延展 too10 執行個體的應用程式服務方案
- 應用程式設定 tooscale tooa 最大的五個執行個體。

hello 應用程式服務方案設定 hello **PerSiteScaling**屬性 tootrue ```"perSiteScaling": true```。 hello 應用程式正在設定 hello**數目的工作者**toouse too5 ```"properties": { "numberOfWorkers": "5" }```。

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

## <a name="recommended-configuration-for-high-density-hosting"></a>高密度裝載的建議組態
每個應用程式調整是全域 Azure 區域和 App Service Environment 中啟用的功能。 不過，hello 建議策略是使用應用程式服務環境 tootake 利用進階的功能和容量的 hello 較大的集區。  

請遵循這些步驟 tooconfigure 高密度裝載您的應用程式：

1. 設定 App Service 環境的 hello 和選擇是專用的 toohello 較高的密度，裝載案例的背景工作集區。
1. 建立單一的應用程式服務方案，並調整它 toouse 所有 hello hello 背景工作集區上的可用容量。
1. 設定 hello PerSiteScaling 旗標 tootrue hello 應用程式服務方案。
1. 新的應用程式會建立並指派 toothat 應用程式服務計劃與**numberOfWorkers**屬性設定太**1**。 使用此設定會產生 hello 最高密度可能此背景工作集區上。
1. hello 背景工作數目可以視需要設定獨立每個應用程式 toogrant 其他資源。 例如：
    - 高用量應用程式可以設定**numberOfWorkers**太**3** toohave 多個處理針對該應用程式的容量。 
    - 低使用率的應用程式會設定**numberOfWorkers**太**1**。

## <a name="next-steps"></a>後續步驟

- [Azure App Service 方案深入概觀](azure-web-sites-web-hosting-plans-in-depth-overview.md)
- [簡介 tooApp Service 環境](../app-service-web/app-service-app-service-environment-intro.md)
