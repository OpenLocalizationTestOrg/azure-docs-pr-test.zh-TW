---
title: "使用 Application Insights 服務網狀架構事件分析 aaaAzure |Microsoft 文件"
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
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 59bb5a409f2951e5b2034049e782dd0da67f933c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="event-analysis-and-visualization-with-application-insights"></a>使用 Application Insights 進行事件分析和視覺效果

Azure Application Insights 是監視和診斷應用程式的擴充式平台。 它包含強大的分析和查詢工具、可自訂的儀表板和視覺效果，以及包括自動化警示的進一步選項。 它是建議的平台監視和診斷 Service Fabric 應用程式和服務的 hello。

## <a name="setting-up-application-insights"></a>設定 Application Insights

### <a name="creating-an-ai-resource"></a>建立 AI 資源

toocreate AI 資源，透過 Azure Marketplace toohello 並搜尋"Application Insights"標頭。 它應顯示為 hello （它是在類別目錄 」 Web + 行動裝置版 」） 的第一個方案。 按一下**建立**您要尋找在 hello 適當的資源 （確認您的路徑符合 hello 圖）。

![新增 Application Insights 資源](media/service-fabric-diagnostics-event-analysis-appinsights/create-new-ai-resource.png)

您將需要某些資訊 tooprovision hello 資源出 toofill 正確。 在 [hello*應用程式類型*欄位中，使用 「 ASP.NET web 應用程式] 如果您將會使用任何 Service Fabric 的程式設計模型或發行的.NET 應用程式 toohello 叢集。 如果您要部署來賓可執行檔和容器，請使用 [一般]。 一般情況下，預設 toousing 「 ASP.NET web 應用程式 」 tookeep 選項在中開啟 hello 未來。 hello 名稱已啟動 tooyour 喜好設定，且 hello 資源群組和訂用帳戶都可以變更部署後的 hello 資源。 我們建議您 AI 資源是否處於 hello 與您的叢集相同的資源群組。 如需詳細資訊，請參閱[建立 Application Insights 資源](../application-insights/app-insights-create-new-resource.md)。

您需要 hello AI 檢測金鑰 tooconfigure AI 與事件彙總工具。 一旦設定 AI 資源之後 （採用 hello 部署會在驗證之後的幾分鐘），瀏覽 tooit，並尋找 hello**屬性**hello 左側的導覽列上一節。 顯示「檢測金鑰」的新刀鋒視窗隨即開啟。 如果您需要 toochange hello 訂用帳戶或資源群組的 hello 資源時，它可以在這裡進行以及。

### <a name="configuring-ai-with-wad"></a>設定具備 WAD 的 AI

有兩種主要的方式從 WAD tooAzure AI，toosend 資料中所述新增需 AI 接收 toohello WAD 組態，達成的[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)。

#### <a name="add-an-ai-instrumentation-key-when-creating-a-cluster-in-azure-portal"></a>在 Azure 入口網站中建立叢集時新增 AI 檢測金鑰

![新增 AIKey](media/service-fabric-diagnostics-event-analysis-appinsights/azure-enable-diagnostics.png)

在建立叢集，如果診斷已 「 開啟 」 時，選擇性欄位 tooenter 應用程式 Insights 檢測金鑰即會顯示。 如果您貼上您的 AI IKey，hello AI 接收將會自動為您所使用的 toodeploy hello Resource Manager 範本在您的叢集的設定。

#### <a name="add-hello-ai-sink-toohello-resource-manager-template"></a>新增 hello AI 接收 toohello Resource Manager 範本

在 hello"WadCfg 」 的 hello Resource Manager 範本，加入 「 接收 」 包含下列兩項變更的 hello:

1. 新增 hello 接收設定：

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

2. 包含在 hello DiagnosticMonitorConfiguration hello 接收器加入 hello"WadCfg"hello"DiagnosticMonitorConfiguration 」 中的行下：

    ```json
    "sinks": "applicationInsights"
    ```

這兩個以上 hello 的 hello 程式碼片段名稱"applicationInsights"是使用的 toodescribe hello 接收。 這就不需要，只要 hello 名稱 hello 接收器會包含 「 接收 」 中，您可以設定 hello 名稱 tooany 字串。

目前，從 hello 叢集記錄檔會顯示為 AI 的記錄檔檢視器中的追蹤。 由於大部分的 hello 追蹤來自 hello 平台的 「 資訊 」 層級，您也可以考慮變更 hello 接收組態 tooonly 傳送記錄檔的"Critical"或"Error"的類型。 作法是藉由新增 「 通道 」 tooyour 接收，如下所示[本文](../monitoring-and-diagnostics/azure-diagnostics-configure-application-insights.md)。

>[!NOTE]
>如果您使用不正確的 AI IKey 入口網站中或資源管理員範本中，您必須 toomanually 變更 hello 金鑰並更新 hello 叢集 / 重新部署它。 

### <a name="configuring-ai-with-eventflow"></a>設定具備 EventFlow 的 AI

如果您使用 EventFlow tooaggregate 事件，請確定 tooimport hello `Microsoft.Diagnostics.EventFlow.Output.ApplicationInsights`NuGet 封裝。 hello 下列已包含在 hello toobe*輸出*區段 hello *eventFlowConfig.json*:

```json
"outputs": [
    {
        "type": "ApplicationInsights",
        // (replace hello following value with your AI resource's instrumentation key)
        "instrumentationKey": "00000000-0000-0000-0000-000000000000"
    }
]
```

在您的篩選條件，請確定 toomake hello 所需的變更，以及包含任何其他輸入 （以及其個別的 NuGet 封裝）。

## <a name="aisdk"></a>AI.SDK

一般會建議 toouse EventFlow 和 WAD 為彙總的解決方案，因為它們允許更模組化的方法 toodiagnostics，也就監視，如果您想 toochange EventFlow 您輸出，需要實際沒有變更 tooyour檢測，只要簡單的修改 tooyour 組態檔。 如果，不過，您決定使用 Application Insights tooinvest，而且不可能 toochange tooa 不同平台，您應該尋找使用的彙總事件，然後將它們傳送 tooAI AI 的新 SDK。 這表示您將不再有 tooconfigure EventFlow toosend 您資料 tooAI，但改為將安裝 hello ApplicationInsight 服務網狀架構 NuGet 套件。 Hello 封裝的詳細資訊可以找到[這裡](https://github.com/Microsoft/ApplicationInsights-ServiceFabric)。

[Application Insights 支援 Microservices 和容器](https://azure.microsoft.com/app-insights-microservices/)顯示部分的 hello 新功能，正在 （目前仍處於 beta 版），可讓您 toohave 更豐富的全新的監視選項與 AI。 其中包括相依性追蹤 （用於建置的所有服務和應用程式在它們之間的叢集與 hello 通訊 AppMap），以及更佳的相互關聯的追蹤來自您的服務 （將有助於更好的查明 hello 的問題工作流程的應用程式或服務）。

如果您正在開發.NET 中，而且可能會使用 Service Fabric 的程式設計模型的一部分，也會為您的平台，以便於檢視和分析事件和記錄資料，則我們建議，您會移透過 hello 做為您的監視 AI SDK 路由願意 toouse AI 和診斷工作流程。 讀取[這](../application-insights/app-insights-asp-net-more.md)和[這](../application-insights/app-insights-asp-net-trace-logs.md)tooget 開始使用 AI toocollect 並顯示您的記錄檔。

## <a name="navigating-hello-ai-resource-in-azure-portal"></a>瀏覽 Azure 入口網站中的 hello AI 資源

一旦您設定了 AI 為輸出，您的事件和記錄檔的資訊應該啟動 tooshow AI 資源中在幾分鐘的時間。 瀏覽 toohello AI 資源，而將採取您 toohello AI 資源儀表板。 按一下**搜尋**hello AI 工作列 toosee hello 最新的追蹤已經接收和 toobe 無法 toofilter 逐一中。

*計量瀏覽器*是很有用的工具，它可根據應用程式、服務和叢集可能報告的計量，建立自訂的儀表板。 請參閱[Application Insights 中的 瀏覽計量](../application-insights/app-insights-metrics-explorer.md)tooset 註冊自己的幾個圖表會根據 hello 您收集的資料。

按一下**分析**forma，obtendrá toohello 應用程式 Insights Analytics 入口網站，您可以在其中查詢事件和追蹤具有更大範圍和選用性。 在 [Application Insights 的 Analytics](../application-insights/app-insights-analytics.md) 中了解更多。

## <a name="next-steps"></a>後續步驟

* [設定警示中 AI](../application-insights/app-insights-alerts.md) toobe 有關效能或使用方式中變更的通知
* [智慧型 Detection in Application Insights](../application-insights/app-insights-proactive-diagnostics.md)執行 hello 遙測傳送 tooAI toowarn 主動式分析您的潛在效能問題
