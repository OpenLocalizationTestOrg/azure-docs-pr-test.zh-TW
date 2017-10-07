---
title: "在 Azure Application Insights aaaMonitor Docker 應用程式 |Microsoft 文件"
description: "Docker 的效能計數器、 事件和例外狀況可以顯示在 Application Insights 以及 hello hello 容器化應用程式的遙測。"
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 27a3083d-d67f-4a07-8f3c-4edb65a0a685
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 9aaf1076bae25485a396db1bb3dcd13bccd87c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-docker-applications-in-application-insights"></a>在 Application Insights 中監視 Docker 應用程式
[Docker](https://www.docker.com/) 容器的週期事件和效能計數器可以在 Application Insights 上繪製成圖表。 安裝 hello [Application Insights](app-insights-overview.md)映像的容器中您的主機，而且會顯示 hello 主機的效能計數器，如為適合 hello 其他映像。

使用 Docker，您可以在完成所有相依性的輕量級容器中散發應用程式。 它們會在執行 Docker 引擎的任何主機電腦上執行。

當您執行 hello [Application Insights 映像](https://hub.docker.com/r/microsoft/applicationinsights/)上 Docker 主機時，您會獲得下列益處：

* 關於執行所有 hello 容器的生命週期遙測 hello 主機-上啟動、 停止和等等。
* 所有的 hello 容器的效能計數器。 CPU、記憶體、網路使用量等。
* 如果您[安裝 Application Insights SDK for Java](app-insights-java-live.md)在 hello hello 容器中執行應用程式，這些應用程式的所有 hello 遙測會都有識別 hello 容器和主機電腦的其他屬性。 例如，如果您在多部主機上執行某個應用程式的多個執行個體，您可以輕鬆地依主機來篩選應用程式遙測。

![範例](./media/app-insights-docker/00.png)

## <a name="set-up-your-application-insights-resource"></a>設定您的 Application Insights 資源
1. 登入[Microsoft Azure 入口網站](https://azure.com)並開啟您的應用程式; hello Application Insights 資源或[建立一個新](app-insights-create-new-resource.md)。 
   
    *我應該使用哪種資源？* 如果由其他使用者所開發的 hello 您主機執行您的應用程式，則您需要[建立新的 Application Insights 資源](app-insights-create-new-resource.md)。 這是供您檢視及分析 hello 遙測。 （選取 [一般] hello 應用程式類型）。
   
    但如果您是開發人員 hello hello 應用程式，然後我們希望您[加入 Application Insights SDK](app-insights-java-live.md) tooeach 它們。 如果是真正的所有元件的單一商務應用程式，則您可能會設定所有的這些 toosend 遙測 tooone 資源，以及您將使用相同資源 toodisplay hello Docker 生命週期和效能資料。 
   
    第三個案例是您開發了大部分的 hello 應用程式，但您要使用不同的資源 toodisplay 其遙測。 在此情況下，您可能也想 toocreate hello Docker 資料不同的資源。 
2. 新增 hello Docker 磚： 選擇**新增磚**，從 hello 圖庫拖曳 hello Docker 磚，然後按一下**完成**。 
   
    ![範例](./media/app-insights-docker/03.png)
3. 按一下 hello **Essentials**下拉式清單，並將複製 hello 檢測金鑰。 使用此 tootell hello SDK 其中 toosend 其遙測。

    ![範例](./media/app-insights-docker/02-props.png)

該瀏覽器視窗保持方便使用，您再回來 tooit 推出 toolook 在您的遙測。

## <a name="run-hello-application-insights-monitor-on-your-host"></a>在主機上執行 hello Application Insights 監視
現在，您有某處 toodisplay hello 遙測，您可以設定，將會收集並傳送的 hello 進行容器化應用程式。

1. 連接 tooyour Docker 主機。 
2. 在這個命令中編輯您的檢測金鑰，然後執行命令：
   
   ```
   
   docker run -v /var/run/docker.sock:/docker.sock -d microsoft/applicationinsights ikey=000000-1111-2222-3333-444444444
   ```

每部 Docker 主機只需要一個 Application Insights 映像。 如果您的應用程式部署在多部 Docker 主機，然後重複每一部主機的 hello 命令。

## <a name="update-your-app"></a>更新應用程式
若您的應用程式設有 hello [Application Insights SDK for Java](app-insights-java-get-started.md)，新增到在專案中，在 hello hello ApplicationInsights.xml 檔案下列行 hello`<TelemetryInitializers>`項目：

```xml

    <Add type="com.microsoft.applicationinsights.extensibility.initializer.docker.DockerContextInitializer"/> 
```

如此會將 Docker 例如容器與主機識別碼 tooevery 遙測項目從您的應用程式傳送的資訊。

## <a name="view-your-telemetry"></a>檢視遙測
返回 tooyour hello Azure 入口網站中的 Application Insights 資源。

按一下瀏覽 hello Docker 磚。

您很快就會看到資料抵達 hello Docker 應用程式，尤其是如果您在 Docker 引擎上執行的其他容器。

以下是一些您可以取得 hello 檢視。

### <a name="perf-counters-by-host-activity-by-image"></a>依據主機的效能計數器，依據映像的活動
![範例](./media/app-insights-docker/10.png)

![範例](./media/app-insights-docker/11.png)

按一下任何主機或映像名稱以取得更多詳細資料。

toocustomize hello] 檢視中，按一下任何圖、 標題，hello 方格，或使用 [新增圖表。 

[深入了解計量瀏覽器](app-insights-metrics-explorer.md)。

### <a name="docker-container-events"></a>Docker 容器事件
![範例](./media/app-insights-docker/13.png)

tooinvestigate 個別事件，按一下[搜尋](app-insights-diagnostic-search.md)。 搜尋和篩選您想要的 toofind hello 事件。 按一下任何事件 tooget 更多詳細資料。

### <a name="exceptions-by-container-name"></a>依據容器名稱的例外狀況
![範例](./media/app-insights-docker/14.png)

### <a name="docker-context-added-tooapp-telemetry"></a>Docker 內容加入 tooapp 遙測
從 hello AI SDK，增添 Docker 內容使用檢測的應用程式傳送要求遙測：

![範例](./media/app-insights-docker/16.png)

處理器時間和可用記憶體效能計數器，並依 Docker 容器名稱擴充和分組：

![範例](./media/app-insights-docker/15.png)

## <a name="q--a"></a>問答集
*Application Insights 可以給我哪些無法從 Docker 取得的功能？*

* 依據容器和映像的效能計數器的詳細分解圖。
* 將容器和應用程式資料整合在一個儀表板中。
* [匯出遙測](app-insights-export-telemetry.md)進一步分析 tooa 資料庫、 Power BI 或其他儀表板。

*如何取得的 hello 應用程式本身的遙測？*

* 安裝 Application Insights SDK hello hello 應用程式中。 針對下列項目深入了解：[Java Web 應用程式](app-insights-java-get-started.md)、[Windows Web 應用程式](app-insights-asp-net.md)。

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>後續步驟

* [適用於 Java 的 Application Insights](app-insights-java-get-started.md)
* [適用於 Node.js 的 Application Insights](app-insights-nodejs.md)
* [適用於 ASP.NET 的 Application Insights](app-insights-asp-net.md)
