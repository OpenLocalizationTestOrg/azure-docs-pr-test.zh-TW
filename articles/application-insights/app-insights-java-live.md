---
title: "aaaApplication Insights for Java web 應用程式已即時"
description: "開始監視已在伺服器上執行的 Web 應用程式"
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 12f3dbb9-915f-4087-87c9-807286030b0b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/10/2016
ms.author: bwren
ms.openlocfilehash: 2b01cd61657522ccf1d2d97b2a29cdeb08ec9a18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-for-java-web-apps-that-are-already-live"></a>適用於使用中 Java Web 應用程式的 Application Insights


如果您有已經 J2EE 伺服器執行的 web 應用程式，您可以開始進行監視它與[Application Insights](app-insights-overview.md) hello 不需要 toomake 程式碼變更，或重新編譯您的專案。 使用此選項，您可以取得 HTTP 要求傳送 tooyour 伺服器、 未處理的例外狀況和效能計數器的相關資訊。

您必須訂閱太[Microsoft Azure](https://azure.com)。

> [!NOTE]
> 在此頁面上的 hello 程序會加入 hello SDK tooyour web 應用程式在執行階段。 如果您不想 tooupdate 或重建您的程式碼，此執行階段檢測將很有用。 如果可以的話，我們建議您，但是[新增 hello SDK toohello 原始程式碼](app-insights-java-get-started.md)改為。 可讓您更多的選項，例如撰寫程式碼 tootrack 使用者活動。
> 
> 

## <a name="1-get-an-application-insights-instrumentation-key"></a>1.取得 Application Insights 檢測金鑰
1. 登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)
2. 建立新的 Application Insights 資源，並設定 hello 應用程式類型 tooJava web 應用程式。
   
    ![填寫名稱，選擇 [Java Web 應用程式]，然後按一下 [建立]](./media/app-insights-java-live/02-create.png)

    hello 資源建立在幾秒鐘的時間。

4. 開啟 hello 新的資源，並取得其檢測金鑰。 您將需要 toopaste 這個機碼到您的程式碼專案很快。
   
    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-live/03-key.png)

## <a name="2-download-hello-sdk"></a>2.下載 SDK hello
1. 下載 hello [Application Insights SDK for Java](https://aka.ms/aijavasdk)。 
2. 在伺服器上解壓縮 hello SDK 內容 toohello 目錄載入您的專案二進位檔的。 如果您使用 Tomcat，此目錄通常在 `webapps/<your_app_name>/WEB-INF/lib` 之下

請注意，您需要 toorepeat 這每個伺服器執行個體，而且可用於每個應用程式。

## <a name="3-add-an-application-insights-xml-file"></a>3.加入 Application Insights XML 檔案
建立 ApplicationInsights.xml 新增 hello SDK 中的 hello 資料夾中。 放入它 hello 下列 XML。

替代 hello 所得 hello Azure 入口網站的檢測金鑰。

```XML

    <?xml version="1.0" encoding="utf-8"?>
    <ApplicationInsights xmlns="http://schemas.microsoft.com/ApplicationInsights/2013/Settings" schemaVersion="2014-05-30">


      <!-- hello key from hello portal: -->

      <InstrumentationKey>** Your instrumentation key **</InstrumentationKey>


      <!-- HTTP request component (not required for bare API) -->

      <TelemetryModules>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebRequestTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebSessionTrackingTelemetryModule"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.modules.WebUserTrackingTelemetryModule"/>
      </TelemetryModules>

      <!-- Events correlation (not required for bare API) -->
      <!-- These initializers add context data tooeach event -->

      <TelemetryInitializers>
        <Add   type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationIdTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebOperationNameTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebSessionTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserTelemetryInitializer"/>
        <Add type="com.microsoft.applicationinsights.web.extensibility.initializers.WebUserAgentTelemetryInitializer"/>

      </TelemetryInitializers>
    </ApplicationInsights>
```

* hello 檢測金鑰會隨每個項目的遙測資料一起傳送，並告知 Application Insights toodisplay 在您的資源。
* hello HTTP 要求的元件是選擇性的。 它會自動傳送有關要求和回應時間 toohello 入口網站的遙測。
* 事件相互關聯是加法 toohello HTTP 要求元件。 它會指派 hello 伺服器接收到的識別項 tooeach 要求，並將此識別項的遙測資料的屬性 tooevery 項目為新增為 hello 屬性 'Operation.Id'。 它可讓您藉由設定的篩選條件相關聯的每個要求 toocorrelate hello 遙測[診斷搜尋](app-insights-diagnostic-search.md)。

## <a name="4-add-an-http-filter"></a>4.加入 HTTP 篩選器
找出並開啟您的專案，並遵循您的應用程式篩選器設定的位置的 hello web 應用程式 節點下，程式碼片段合併 hello hello web.xml 檔案。

所有其他篩選條件之前，應該要對應 tooget hello 最精確的結果，hello 篩選。

```XML

    <filter>
      <filter-name>ApplicationInsightsWebFilter</filter-name>
      <filter-class>
        com.microsoft.applicationinsights.web.internal.WebRequestTrackingFilter
      </filter-class>
    </filter>
    <filter-mapping>
       <filter-name>ApplicationInsightsWebFilter</filter-name>
       <url-pattern>/*</url-pattern>
    </filter-mapping>
```

## <a name="5-check-firewall-exceptions"></a>5.檢查防火牆例外狀況
您可能需要[設定例外狀況 toosend 傳出資料](app-insights-ip-addresses.md)。

## <a name="6-restart-your-web-app"></a>6.重新啟動您的 Web 應用程式
## <a name="7-view-your-telemetry-in-application-insights"></a>7.在 Application Insights 中檢視遙測
傳回在 tooyour Application Insights 資源[Microsoft Azure 入口網站](https://portal.azure.com)。

HTTP 要求的相關遙測會顯示 hello 概觀刀鋒視窗上。 (如果沒有出現，請稍等片刻，然後按一下重新整理。)

![範例資料](./media/app-insights-java-live/5-results.png)

按一下 透過任何圖表 toosee 度量詳細資訊。 

![](./media/app-insights-java-live/6-barchart.png)

與檢視之要求的 hello 屬性，您會看見 hello 遙測事件與它相關聯，例如要求和例外狀況。

![](./media/app-insights-java-live/7-instance.png)

[深入了解度量。](app-insights-metrics-explorer.md)

## <a name="next-steps"></a>後續步驟
* [將遙測 tooyour web 網頁](app-insights-javascript.md)toomonitor 頁面上，檢視和使用者度量。
* [設定 web 測試](app-insights-monitor-web-app-availability.md)toomake 即時且回應迅速，保持您的應用程式。
* [擷取記錄追蹤](app-insights-java-trace-logs.md)
* [搜尋事件和記錄檔](app-insights-diagnostic-search.md)toohelp 診斷問題。

