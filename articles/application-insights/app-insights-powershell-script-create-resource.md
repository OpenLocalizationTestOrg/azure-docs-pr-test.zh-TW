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
# <a name="powershell-script-toocreate-an-application-insights-resource"></a>PowerShell 指令碼 toocreate Application Insights 資源


當您想要 toomonitor 新的應用程式-或新版本的應用程式-與[Azure Application Insights](https://azure.microsoft.com/services/application-insights/)，您設定 Microsoft Azure 中新的資源。 此資源是其中分析及顯示 hello 遙測資料從您的應用程式。 

您可以使用 PowerShell 來自動化 hello 建立新的資源。

例如，如果您正在開發行動裝置應用程式，則客戶可能會在任何時候，同時使用數個已發行的應用程式版本。 您不想要從不同版本混 tooget hello 遙測結果。 因此您會取得您的建置程序 toocreate 新資源每個組建。

> [!NOTE]
> 如果您想 toocreate 一組資源的所有項目 hello 相同的時間，請考慮[建立 hello 資源使用 Azure 範本](app-insights-powershell.md)。
> 
> 

## <a name="script-toocreate-an-application-insights-resource"></a>指令碼 toocreate Application Insights 資源
請參閱 hello 相關的指令程式規格：

* [New-AzureRmResource](https://msdn.microsoft.com/library/mt652510.aspx)
* [New-AzureRmRoleAssignment](https://msdn.microsoft.com/library/mt678995.aspx)

*PowerShell 指令碼*  

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

## <a name="what-toodo-with-hello-ikey"></a>與 hello iKey 哪些 toodo
每項資源均是由其檢測金鑰 (iKey) 識別。 hello iKey 是 hello 資源建立指令碼的輸出。 組建指令碼應該提供 hello iKey toohello 內嵌在您的應用程式的 Application Insights SDK。

有兩種方式 toomake hello iKey 可用 toohello SDK:

* 在 [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md)中： 
  * `<instrumentationkey>`*ikey*`</instrumentationkey>`
* 或在 [初始化程式碼](app-insights-api-custom-events-metrics.md)中： 
  * `Microsoft.ApplicationInsights.Extensibility.
    TelemetryConfiguration.Active.InstrumentationKey = "`*iKey*`";`

## <a name="see-also"></a>另請參閱
* [從範本建立 Application Insights 和 Web 測試資源](app-insights-powershell.md)
* [Set 使用 PowerShell 設定 Azure 診斷的監視](app-insights-powershell-azure-diagnostics.md) 
* [使用 PowerShell 設定警示](app-insights-powershell-alerts.md)

