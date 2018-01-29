---
title: "Azure Service Fabric 事件分析與 Application Insights | Microsoft Docs"
description: "了解如何使用 Application Insights 視覺化及分析事件，來監視和診斷 Azure Service Fabric 叢集。"
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 10/15/2017
ms.author: dekapur
ms.openlocfilehash: 34f14f42150e46edae2d1352827f96a411117a62
ms.sourcegitcommit: a7c01dbb03870adcb04ca34745ef256414dfc0b3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/17/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>使用 Application Insights 進行事件分析和視覺效果

Azure Application Insights 是監視和診斷應用程式的擴充式平台。 它包含強大的分析和查詢工具、可自訂的儀表板和視覺效果，以及包括自動化警示的進一步選項。 我們建議使用此平台監視和診斷 Service Fabric 應用程式和服務。

## <a name="setting-up-application-insights"></a>設定 Application Insights

### <a name="creating-an-ai-resource"></a>建立 AI 資源

若要建立 AI 資源，請前往 Azure Marketplace 搜尋 "Application Insights"。 它應該會顯示為第一個解決方案 (在 [Web + 行動] 類別目錄下)。 找到正確的資源時，請按一下 [建立] (確認您的路徑與下圖相符)。

![新增 Application Insights 資源](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

您需要填寫一些資訊以正確佈建資源。 如果您要使用任何 Service Fabric 的程式設計模型或將 .NET 應用程式發佈至叢集，[應用程式類型] 欄位請使用 [ASP.NET Web 應用程式]。 如果您要部署來賓可執行檔和容器，請使用 [一般]。 一般情況下預設使用 [ASP.NET Web 應用程式] 以在日後保持開放選項。 名稱隨您的喜好設定，資源群組和訂用帳戶都可以在資源部署後變更。 我們建議 AI 資源與您的叢集位於相同的資源群組。 如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。

您需要使用 AI 檢測金鑰設定 AI 搭配事件彙總工具。 完成 AI 資源設定後 (佈署後花幾分鐘驗證)，請在左側的導覽列上瀏覽並尋找 [屬性] 區段。 顯示「檢測金鑰」的新刀鋒視窗隨即開啟。 如果您需要變更訂用帳戶或資源的資源群組，也可以在這裡完成。

### <a name="configuring-ai-with-wad"></a>設定具備 WAD 的 AI

>[!NOTE]
>目前這僅適用於 Windows 叢集。

有兩種主要方式可將資料從 WAD 的傳送至 Azure AI，只要將 AI 接收新增到 WAD 設定中即可，詳細資訊請參閱[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)。

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>在 Azure 入口網站中建立叢集時新增 AI 檢測金鑰

![新增 AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

建立叢集時，如果診斷已 [開啟]，即會顯示輸入 Application Insights 檢測金鑰的選擇性欄位。 如果在此貼上您的 AI IKey，用來部署叢集的 Resource Manager 範本就會自動為您設定 AI 接收。

#### <a name="add-the-ai-sink-to-the-resource-manager-template"></a>將 AI 接收新增至 Resource Manager 範本

在 Resource Manager 範本的 "WadCfg" 中，納入下列兩項變更以新增「接收」：

1. 直接在宣告 `DiagnosticMonitorConfiguration` 完成之後，新增接收設定：

    ```json
    "SinksConfig": {
        "Sink": [
            {
                "name": "applicationInsights",
                "ApplicationInsights": "***ADD INSTRUMENTATION KEY HERE***"
            }
        ]
    }

    ```

2. 在 `DiagnosticMonitorConfiguration` 中包含接收，方法是在 `WadCfg` 的 `DiagnosticMonitorConfiguration` 中新增下列行 (在 `EtwProviders` 宣告之前)：

    ```json
    "sinks": "applicationInsights"
    ```

上面這兩個程式碼片段都使用 "applicationInsights" 名稱來描述接收。 這不是需求，而是只要在「接收」中包含接收的名稱，就可以在任何字串設定該名稱。

目前，叢集中的記錄檔會顯示為 AI 記錄檔檢視器中的追蹤。 由於大部分來自平台的追蹤層級都是「資訊」，您也可以考慮將接收設定變更為僅傳送「重大」或「錯誤」類型的記錄。 只要將「通道」新增至接收器即可，如[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)所示。

>[!NOTE]
>如果您在入口網站或 Resource Manager 範本中使用不正確的 AI IKey，您就必須手動變更金鑰，並更新/重新部署叢集。 

### <a name="configuring-ai-with-eventflow"></a>設定具備 EventFlow 的 AI

如要使用 EventFlow 來彙總事件，請務必匯入 `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 套件。 *eventFlowConfig.json* 的 [輸出] 區段必須包含以下內容：

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace the following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

請務必在您的篩選中進行必要的變更，以及包含任何其他輸入 (以及其個別的 NuGet 套件)。

## <a name="aisdk"></a>AI.SDK

通常建議使用 EventFlow 和 WAD 做為彙總解決方案，因為它們允許以更接近模組化的方法來診斷和監視，亦即，如果您想要變更來自 EventFlow 的輸出，不必變更實際的檢測，只要簡單修改組態檔即可。 但如果決定投資使用 Application Insights，而且不太可能變更到不同的平台，您應該考慮使用 AI 的新 SDK 來彙總事件，並將它們傳送到 AI。 這表示您不必再設定 EventFlow 將資料傳送至 AI，而是改為安裝 ApplicationInsight 的 Service Fabric NuGet 套件。 套件的詳細資訊位於[這裡](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)。

[微服務與容器的 Application Insights 支援](https://azure.microsoft.com/app-insights-microservices/)會顯示一些開發中的新功能 (目前仍為 beta 版)，讓您有更多的 AI 立即可用監視選項。 包括相依性追蹤 (用於建置叢集中所有服務和應用程式的 AppMap 及它們之間的通訊)，以及來自服務的追蹤有更好的相互關聯 (更有助於查明應用程式或服務工作流程中的問題)。

如果您是在 .NET 中進行開發，可能會使用一些 Service Fabric 的程式設計模型，而且是願意使用 AI 做視覺化和分析事件和記錄檔資料的平台，我們建議您在監視和診斷工作流程時透過 AI SDK 路由。 閱讀[本文](../application-insights/app-insights-asp-net-more.md)和[本文](../application-insights/app-insights-asp-net-trace-logs.md)開始使用 AI 來收集和顯示您的記錄檔。

## <a name="navigating-the-ai-resource-in-azure-portal"></a>在 Azure 入口網站中瀏覽 AI 資源

一旦將 AI 設定為事件和記錄檔的輸出，資訊就會在幾分鐘內開始出現在 AI 資源中。 瀏覽至 AI 資源，它會帶您到 AI 資源儀表板。 按一下 AI 工作列的 [搜尋]，可查看它接收到的最新追蹤，並可從中進行篩選。

*計量瀏覽器*是很有用的工具，它可根據應用程式、服務和叢集可能報告的計量，建立自訂的儀表板。 請參閱[在 Application Insights 中探索計量](../application-insights/app-insights-metrics-explorer.md)，根據您所收集的資料自行設定幾個圖表。

按一下 [分析] 會帶您到 Application Insights 的 Analytics 入口網站中，您可以在這裡查詢更大範圍和選擇性的事件和追蹤。 在 [Application Insights 的 Analytics](../application-insights/app-insights-analytics.md) 中了解更多。

## <a name="next-steps"></a>後續步驟

* [在 AI 中設定警示](../application-insights/app-insights-alerts.md)以收到效能或使用方式的變更通知
* [Application Insights 的智慧偵測](../application-insights/app-insights-proactive-diagnostics.md)會對傳送至 AI 的遙測資料執行主動式分析，對可能的效能問題提出警告。