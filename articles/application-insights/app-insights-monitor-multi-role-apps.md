---
title: "aaaAzure Application Insights 支援多個元件、 microservices，以及容器 |Microsoft 文件"
description: "監視由多個元件或角色組成之應用程式的效能和使用方式。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: 6185eedf32ec450d7541603b94de6c3dcdf64a85
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-multi-component-applications-with-application-insights-preview"></a>使用 Application Insights (預覽) 監視多元件應用程式

您可以使用 [Azure Application Insights](app-insights-overview.md)，監視由多個伺服器元件、角色或服務所組成的應用程式。 hello 元件健全狀況 hello 和 hello 兩者間的關聯性會顯示在單一的應用程式對應。 您可以使用自動 HTTP 相互關聯，透過多個元件追蹤個別作業。 容器診斷可以與應用程式遙測整合並相互關聯。 使用單一的 Application Insights 資源的應用程式的所有 hello 元件。 

![多元件應用程式對應](./media/app-insights-monitor-multi-role-apps/app-map.png)

我們會使用 '元件' 這裡 toomean 的大型應用程式的任何正常運作的一部分。 例如，一般商務應用程式可能包含在 web 瀏覽器中，指 tooone 中執行的用戶端程式碼或更多的 web 應用程式服務，接著使用 上一步結束服務。 伺服器元件可能裝載在內部部署上 hello 雲端，或可能是 Azure web 和背景工作角色，或容器，例如 Docker 或 Service Fabric 執行。 

### <a name="sharing-a-single-application-insights-resource"></a>共用單一 Application Insights 資源 

hello 索引鍵的技術是從每個元件的應用程式 toohello toosend 遙測相同的 Application Insights 資源，但使用 hello`cloud_RoleName`屬性 toodistinguish 元件在必要時。 hello Application Insights SDK 加入 hello`cloud_RoleName`屬性 toohello 遙測元件發出。 比方說，hello SDK 會將網站名稱或服務的角色名稱 toohello`cloud_RoleName`屬性。 您可以使用 telemetryinitializer 覆寫這個值。 hello 應用程式對應使用 hello `cloud_RoleName` hello 地圖上的屬性 tooidentify hello 元件。

如需有關如何覆寫 hello`cloud_RoleName`屬性，請參閱[將屬性加入： ITelemetryInitializer](app-insights-api-filtering-sampling.md#add-properties-itelemetryinitializer)。  

在某些情況下，這不是適當，，您可能會想 toouse 不同元件的不同群組的資源。 例如，您可能需要 toouse 不同的資源管理或計費。 使用不同的資源表示您沒有看到所有顯示在單一的應用程式對應; 上的 hello 元件而且您不能跨元件中查詢[分析](app-insights-analytics.md)。 您也可以 tooset hello 個別資源。

與該警告，我們假設在 hello 這份文件其餘部分的 toosend 資料從多個元件 tooone Application Insights 資源。

## <a name="configure-multi-component-applications"></a>設定多元件應用程式

tooget 多元件的應用程式對應，您需要 tooachieve 這些目標：

* **安裝 hello 最新發行前版本**hello 應用程式的每個元件中的 Application Insights 套件。 
* **共用單一的 Application Insights 資源**針對所有 hello 應用程式的元件。
* **啟用多角色應用程式對應**hello 預覽刀鋒視窗中。

設定使用 hello 適當的方法，其類型的應用程式的每個元件。 ([ASP.NET](app-insights-asp-net.md)、[Java](app-insights-java-get-started.md)、[Node.js](app-insights-nodejs.md)、[JavaScript](app-insights-javascript.md))。

### <a name="1-install-hello-latest-pre-release-package"></a>1.安裝最新發行前套件 hello

更新或安裝 hello 正 Insights 套件 hello 專案中為每一個伺服器元件。 如果您使用 Visual Studio：

1. 以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。 
2. 選取 [包括發行前版本]。
3. 如果 Application Insights 套件顯示在 [更新] 中，請加以選取。 

    否則，請瀏覽及安裝 hello 適當套件：
    
    * Microsoft.ApplicationInsights.WindowsServer
    * Microsoft.ApplicationInsights.ServiceFabric - 適用於當做客體可執行檔執行的元件和在 Service Fabric 應用程式中執行的 Docker 容器
    * Microsoft.ApplicationInsights.ServiceFabric.Native - 適用於 ServiceFabric 應用程式中的 Reliable Services
    * Microsoft.ApplicationInsights.Kubernetes - 適用於在 Kubernetes 上的 Docker 中執行的元件

### <a name="2-share-a-single-application-insights-resource"></a>2.共用單一 Application Insights 資源

* 在 Visual Studio 中，以滑鼠右鍵按一下專案，然後選取 [設定 Application Insights]，或 [Application Insights] > [設定]。 Hello 第一個專案中，使用 hello 精靈 toocreate Application Insights 資源。 後續專案中，選取 hello 相同的資源。
* 如果沒有 Application Insights 功能表上，請手動進行設定︰

   1. 在[Azure 入口網站](https://portal,azure.com)，開啟您已為另一個元件所建立的 hello Application Insights 資源。
   2. 在 hello 概觀刀鋒視窗，開啟 hello Essentials 下拉式索引標籤上，複製 hello**檢測金鑰。**
   3. 在您的專案中，開啟 ApplicationInsights.config 並插入︰`<InstrumentationKey>your copied key</InstrumentationKey>`

![複製 hello 檢測金鑰 toohello.config 檔案](./media/app-insights-monitor-multi-role-apps/copy-instrumentation-key.png)


### <a name="3-enable-multi-role-application-map"></a>3.啟動多角色應用程式對應

在 hello Azure 入口網站，開啟您的應用程式的 hello 資源。 在 hello 預覽刀鋒視窗中，啟用*多角色應用程式對應*。

### <a name="4-enable-docker-metrics-optional"></a>4.啟用 Docker 計量 (選擇性) 

如果在裝載 Windows Azure VM 上的 Docker 執行元件，您可以從 hello 容器收集其他度量。 在您的 [Azure 診斷](../monitoring-and-diagnostics/azure-diagnostics.md)組態檔中插入此程式碼︰

```
"DiagnosticMonitorConfiguration": {
        ...
        "sinks": "applicationInsights",
        "DockerSources": {
                "Stats": {
                    "enabled": true,
                    "sampleRate": "PT1M"
                }
            },
        ...
    }
    ...   
    "SinksConfig": {
        "Sink": [{
            "name": "applicationInsights",
            "ApplicationInsights": "<your instrumentation key here>"
        }]
    }
    ...
}

```

## <a name="use-cloudrolename-tooseparate-components"></a>使用 cloud_RoleName tooseparate 元件

hello`cloud_RoleName`屬性是附加的 tooall 遙測。 它會識別 hello 元件-hello 角色或服務-源自 hello 遙測。 （它是不相同 hello 為 cloud_RoleInstance，會以平行方式執行多個伺服器處理序或電腦的相同角色分隔）。

在 hello 入口網站中，您可以篩選或區段您使用這個屬性的遙測。 在此範例中，hello 失敗刀鋒視窗就是篩選的 tooshow 只 hello 前端的 web 服務，篩選出 hello CRM API 後端的失敗資訊：

![依雲端角色名稱區隔的計量圖表](./media/app-insights-monitor-multi-role-apps/cloud-role-name.png)

## <a name="trace-operations-between-components"></a>追蹤元件之間的作業

您可以從一個元件 tooanother，hello 呼叫處理個別的作業時進行追蹤。


![顯示作業的遙測](./media/app-insights-monitor-multi-role-apps/show-telemetry-for-operation.png)

透過這項作業的遙測 tooa 相互關聯清單按一下跨 hello 前端網頁伺服器與 hello 後端應用程式開發介面：

![跨元件搜尋](./media/app-insights-monitor-multi-role-apps/search-across-components.png)


## <a name="next-steps"></a>後續步驟

* [區分開發、測試及生產環境的遙測](app-insights-separate-resources.md)
