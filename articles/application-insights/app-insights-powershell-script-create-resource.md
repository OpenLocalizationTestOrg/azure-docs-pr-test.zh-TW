---
title: "aaaPowerShell 指令碼 toocreate Application Insights 資源 |Microsoft 文件"
description: "自動建立 Application Insights 資源。"
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: f0082c9b-43ad-4576-a417-4ea8e0daf3d9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/19/2016
ms.author: bwren
ms.openlocfilehash: 2ac00376d38026d64c2c5deabfaca60588924510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="powershell-script-toocreate-an-application-insights-resource"></a><span data-ttu-id="364bc-103">PowerShell 指令碼 toocreate Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="364bc-103">PowerShell script toocreate an Application Insights resource</span></span>


<span data-ttu-id="364bc-104">當您想要 toomonitor 新的應用程式-或新版本的應用程式-與[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)，您設定 Microsoft Azure 中新的資源。</span><span class="sxs-lookup"><span data-stu-id="364bc-104">When you want toomonitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="364bc-105">此資源是其中分析及顯示 hello 遙測資料從您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="364bc-105">This resource is where hello telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="364bc-106">您可以使用 PowerShell 來自動化 hello 建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="364bc-106">You can automate hello creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="364bc-107">例如，如果您正在開發行動裝置應用程式，則客戶可能會在任何時候，同時使用數個已發行的應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="364bc-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="364bc-108">您不想要從不同版本混 tooget hello 遙測結果。</span><span class="sxs-lookup"><span data-stu-id="364bc-108">You don't want tooget hello telemetry results from different versions mixed up.</span></span> <span data-ttu-id="364bc-109">因此您會取得您的建置程序 toocreate 新資源每個組建。</span><span class="sxs-lookup"><span data-stu-id="364bc-109">So you get your build process toocreate a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="364bc-110">如果您想 toocreate 一組資源的所有項目 hello 相同的時間，請考慮[建立 hello 資源使用 Azure 範本](app-insights-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="364bc-110">If you want toocreate a set of resources all at hello same time, consider [creating hello resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a><span data-ttu-id="364bc-111">指令碼 toocreate Application Insights 資源</span><span class="sxs-lookup"><span data-stu-id="364bc-111">Script toocreate an Application Insights resource</span></span>
<span data-ttu-id="364bc-112">請參閱 hello 相關的指令程式規格：</span><span class="sxs-lookup"><span data-stu-id="364bc-112">See hello relevant cmdlet specs:</span></span>

* [<span data-ttu-id="364bc-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="364bc-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="364bc-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="364bc-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="364bc-115">*PowerShell 指令碼*</span><span class="sxs-lookup"><span data-stu-id="364bc-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before hello first 
# execution toologin toohello Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set hello name of hello Application Insights Resource

$appInsightsName = "TestApp"

# Set hello application name used for hello value of hello Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set hello name of hello Resource Group toouse.  
# Default is hello application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create hello Resource and Output hello name and iKey
###################################################

# Select hello azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create hello App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access toohello team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-toodo-with-hello-ikey"></a><span data-ttu-id="364bc-116">與 hello iKey 哪些 toodo</span><span class="sxs-lookup"><span data-stu-id="364bc-116">What toodo with hello iKey</span></span>
<span data-ttu-id="364bc-117">每項資源均是由其檢測金鑰 (iKey) 識別。</span><span class="sxs-lookup"><span data-stu-id="364bc-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="364bc-118">hello iKey 是 hello 資源建立指令碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="364bc-118">hello iKey is an output of hello resource creation script.</span></span> <span data-ttu-id="364bc-119">組建指令碼應該提供 hello iKey toohello 內嵌在您的應用程式的 Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="364bc-119">Your build script should provide hello iKey toohello Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="364bc-120">有兩種方式 toomake hello iKey 可用 toohello SDK:</span><span class="sxs-lookup"><span data-stu-id="364bc-120">There are two ways toomake hello iKey available toohello SDK:</span></span>

* <span data-ttu-id="364bc-121">在 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)中：</span><span class="sxs-lookup"><span data-stu-id="364bc-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="364bc-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="364bc-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="364bc-123">或在 [初始化程式碼](app-insights-api-custom-events-metrics.md)中：</span><span class="sxs-lookup"><span data-stu-id="364bc-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="364bc-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="364bc-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="364bc-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="364bc-125">See also</span></span>
* [<span data-ttu-id="364bc-126">從範本建立 Application Insights 和 Web 測試資源</span><span class="sxs-lookup"><span data-stu-id="364bc-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="364bc-127">Set 使用 PowerShell 設定 Azure 診斷的監視</span><span class="sxs-lookup"><span data-stu-id="364bc-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="364bc-128">使用 PowerShell 設定警示</span><span class="sxs-lookup"><span data-stu-id="364bc-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

