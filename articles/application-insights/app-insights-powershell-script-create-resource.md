---
title: "建立 Application Insights 資源的 PowerShell 指令碼 | Microsoft Docs"
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
ms.openlocfilehash: a828af9c7d207dd84cc626fc70206018fd67e2dd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="powershell-script-to-create-an-application-insights-resource"></a><span data-ttu-id="145a5-103">建立 Application Insights 資源的 PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="145a5-103">PowerShell script to create an Application Insights resource</span></span>


<span data-ttu-id="145a5-104">當您想要使用 [Azure Application Insights](https://azure.microsoft.com/services/application-insights/) 來監視新的應用程式或新版應用程式時，需在 Microsoft Azure 中設定新的資源。</span><span class="sxs-lookup"><span data-stu-id="145a5-104">When you want to monitor a new application - or a new version of an application - with [Azure Application Insights](https://azure.microsoft.com/services/application-insights/), you set up a new resource in Microsoft Azure.</span></span> <span data-ttu-id="145a5-105">此資源是分析和顯示應用程式之遙測資料的位置。</span><span class="sxs-lookup"><span data-stu-id="145a5-105">This resource is where the telemetry data from your app is analyzed and displayed.</span></span> 

<span data-ttu-id="145a5-106">您可以使用 PowerShell 將建立新資源的過程自動化。</span><span class="sxs-lookup"><span data-stu-id="145a5-106">You can automate the creation of a new resource by using PowerShell.</span></span>

<span data-ttu-id="145a5-107">例如，如果您正在開發行動裝置應用程式，則客戶可能會在任何時候，同時使用數個已發行的應用程式版本。</span><span class="sxs-lookup"><span data-stu-id="145a5-107">For example, if you are developing a mobile device app, it's likely that, at any time, there will be several published versions of your app in use by your customers.</span></span> <span data-ttu-id="145a5-108">您不想取得不同版本混在一起的遙測結果。</span><span class="sxs-lookup"><span data-stu-id="145a5-108">You don't want to get the telemetry results from different versions mixed up.</span></span> <span data-ttu-id="145a5-109">因此您讓建置流程針對每個新組建建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="145a5-109">So you get your build process to create a new resource for each build.</span></span>

> [!NOTE]
> <span data-ttu-id="145a5-110">如果您想要同時建立一組資源，請考慮[使用 Azure 範本來建立資源](app-insights-powershell.md)。</span><span class="sxs-lookup"><span data-stu-id="145a5-110">If you want to create a set of resources all at the same time, consider [creating the resources using an Azure template](app-insights-powershell.md).</span></span>
> 
> 

## <a name="script-to-create-an-application-insights-resource"></a><span data-ttu-id="145a5-111">建立 Application Insights 資源的指令碼</span><span class="sxs-lookup"><span data-stu-id="145a5-111">Script to create an Application Insights resource</span></span>
<span data-ttu-id="145a5-112">請參閱相關的 Cmdlet 規格：</span><span class="sxs-lookup"><span data-stu-id="145a5-112">See the relevant cmdlet specs:</span></span>

* [<span data-ttu-id="145a5-113">New-AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="145a5-113">New-AzureRmResource</span></span>](https://msdn.microsoft.com/library/mt652510.aspx)
* [<span data-ttu-id="145a5-114">New-AzureRmRoleAssignment</span><span class="sxs-lookup"><span data-stu-id="145a5-114">New-AzureRmRoleAssignment</span></span>](https://msdn.microsoft.com/library/mt678995.aspx)

<span data-ttu-id="145a5-115">*PowerShell 指令碼*</span><span class="sxs-lookup"><span data-stu-id="145a5-115">*PowerShell Script*</span></span>  

```PowerShell


###########################################
# Set Values
###########################################

# If running manually, uncomment before the first 
# execution to login to the Azure Portal:

# Add-AzureRmAccount / Login-AzureRmAccount

# Set the name of the Application Insights Resource

$appInsightsName = "TestApp"

# Set the application name used for the value of the Tag "AppInsightsApp" 

$applicationTagName = "MyApp"

# Set the name of the Resource Group to use.  
# Default is the application name.
$resourceGroupName = "MyAppResourceGroup"

###################################################
# Create the Resource and Output the name and iKey
###################################################

# Select the azure subscription
Select-AzureSubscription -SubscriptionName "MySubscription"

# Create the App Insights Resource


$resource = New-AzureRmResource `
  -ResourceName $appInsightsName `
  -ResourceGroupName $resourceGroupName `
  -Tag @{ applicationType = "web"; applicationName = $applicationTagName} `
  -ResourceType "Microsoft.Insights/components" `
  -Location "East US" `  # or North Europe, West Europe, South Central US
  -PropertyObject @{"Application_Type"="web"} `
  -Force

# Give owner access to the team

New-AzureRmRoleAssignment `
  -SignInName "myteam@fabrikam.com" `
  -RoleDefinitionName Owner `
  -Scope $resource.ResourceId 


# Display iKey
Write-Host "App Insights Name = " $resource.Name
Write-Host "IKey = " $resource.Properties.InstrumentationKey

```

## <a name="what-to-do-with-the-ikey"></a><span data-ttu-id="145a5-116">如何使用 iKey</span><span class="sxs-lookup"><span data-stu-id="145a5-116">What to do with the iKey</span></span>
<span data-ttu-id="145a5-117">每項資源均是由其檢測金鑰 (iKey) 識別。</span><span class="sxs-lookup"><span data-stu-id="145a5-117">Each resource is identified by its instrumentation key (iKey).</span></span> <span data-ttu-id="145a5-118">iKey 是資源建立指令碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="145a5-118">The iKey is an output of the resource creation script.</span></span> <span data-ttu-id="145a5-119">您的建置指令碼應該將 iKey 提供給內嵌在您應用程式中的 Application Insights SDK。</span><span class="sxs-lookup"><span data-stu-id="145a5-119">Your build script should provide the iKey to the Application Insights SDK embedded in your app.</span></span>

<span data-ttu-id="145a5-120">有兩種方式可讓 SDK 取得 iKey：</span><span class="sxs-lookup"><span data-stu-id="145a5-120">There are two ways to make the iKey available to the SDK:</span></span>

* <span data-ttu-id="145a5-121">在 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)中：</span><span class="sxs-lookup"><span data-stu-id="145a5-121">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md):</span></span> 
  * <span data-ttu-id="145a5-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span><span class="sxs-lookup"><span data-stu-id="145a5-122">`<instrumentationkey>`*ikey*`</instrumentationkey>`</span></span>
* <span data-ttu-id="145a5-123">或在 [初始化程式碼](app-insights-api-custom-events-metrics.md)中：</span><span class="sxs-lookup"><span data-stu-id="145a5-123">Or in [initialization code](app-insights-api-custom-events-metrics.md):</span></span> 
  * <span data-ttu-id="145a5-124">`Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span><span class="sxs-lookup"><span data-stu-id="145a5-124">`Microsoft.ApplicationInsights.Extensibility.
TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`</span></span>

## <a name="see-also"></a><span data-ttu-id="145a5-125">另請參閱</span><span class="sxs-lookup"><span data-stu-id="145a5-125">See also</span></span>
* [<span data-ttu-id="145a5-126">從範本建立 Application Insights 和 Web 測試資源</span><span class="sxs-lookup"><span data-stu-id="145a5-126">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="145a5-127">Set 使用 PowerShell 設定 Azure 診斷的監視</span><span class="sxs-lookup"><span data-stu-id="145a5-127">Set up monitoring of Azure diagnostics with PowerShell</span></span>](app-insights-powershell-azure-diagnostics.md) 
* [<span data-ttu-id="145a5-128">使用 PowerShell 設定警示</span><span class="sxs-lookup"><span data-stu-id="145a5-128">Set alerts by using PowerShell</span></span>](app-insights-powershell-alerts.md)

