---
title: "使用 Azure Application Insights aaaJava web 應用程式分析 |Microsoft 文件"
description: "使用 Application Insights 針對 Java Web 應用程式進行應用程式效能監視。 "
services: application-insights
documentationcenter: java
author: harelbr
manager: carmonm
ms.assetid: 051d4285-f38a-45d8-ad8a-45c3be828d91
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 6555ee53a44f937350e4fa296080f7dce4f45226
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-in-a-java-web-project"></a>在 Java Web 專案中開始使用 Application Insights


[Application Insights](https://azure.microsoft.com/services/application-insights/)是 web 開發人員，可協助您了解 hello 效能和使用即時應用程式的可延伸的分析服務。 它也使用[偵測及診斷效能問題和例外狀況](app-insights-detect-triage-diagnose.md)，和[撰寫程式碼][ api] tootrack 哪些使用者處理您的應用程式。

![範例資料](./media/app-insights-java-get-started/5-results.png)

Application Insights 支援 Linux、Unix 或 Windows 上執行的 Java 應用程式。

您需要：

* Oracle JRE 1.6 或更新版本，或 Zulu JRE 1.6 或更新版本
* 訂用帳戶太[Microsoft Azure](https://azure.microsoft.com/)。

*如果您有已經是即時的 web 應用程式，您可能太遵循 hello 替代程序[hello web 伺服器中執行階段新增 hello SDK](app-insights-java-live.md)。其他的替代方法可避免重建 hello 程式碼，但沒有得到 hello 選項 toowrite 程式碼 tootrack 使用者活動。*

## <a name="1-get-an-application-insights-instrumentation-key"></a>1.取得 Application Insights 檢測金鑰
1. 登入 toohello [Microsoft Azure 入口網站](https://portal.azure.com)。
2. 建立 Application Insights 資源。 設定 hello 應用程式類型 tooJava web 應用程式。

    ![填寫名稱，選擇 [Java Web 應用程式]，然後按一下 [建立]](./media/app-insights-java-get-started/02-create.png)
3. 尋找 hello hello 新資源的檢測金鑰。 您將需要 toopaste 這個機碼到您的程式碼專案很快。

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-get-started/03-key.png)

## <a name="2-add-hello-application-insights-sdk-for-java-tooyour-project"></a>2.新增 hello Application Insights SDK for Java tooyour 專案
*選擇 hello 適當的方式，為您的專案。*

#### <a name="if-youre-using-eclipse-toocreate-a-maven-or-dynamic-web-project-"></a>如果您使用的 Eclipse toocreate Maven 或動態 Web 專案...
使用 hello [Application Insights SDK for Java 外掛程式][eclipse]。

#### <a name="if-youre-using-maven"></a>如果您使用 Maven...
如果您的專案已設定 toouse Maven 組建，合併 hello 下列程式碼 tooyour pom.xml 檔案。

然後，重新整理 hello 專案相依性 tooget hello 二進位檔下載。

```XML

    <repositories>
       <repository>
          <id>central</id>
          <name>Central</name>
          <url>http://repo1.maven.org/maven2</url>
       </repository>
    </repositories>

    <dependencies>
      <dependency>
        <groupId>com.microsoft.azure</groupId>
        <artifactId>applicationinsights-web</artifactId>
        <!-- or applicationinsights-core for bare API -->
        <version>[1.0,)</version>
      </dependency>
    </dependencies>
```

* *建置或總和檢查碼驗證錯誤？* 嘗試使用特定版本，例如：`<version>1.0.n</version>`。 您可以找到 hello 最新版本中 hello [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)或是在我們[Maven 成品](http://search.maven.org/#search%7Cga%7C1%7Capplicationinsights)。
* *需要 tooupdate tooa 新 SDK 嗎？* 請重新整理專案的相依項目。

#### <a name="if-youre-using-gradle"></a>如果您使用 Gradle...
如果您的專案已設定 toouse Gradle 組建，合併 hello 下列程式碼 tooyour build.gradle 檔案。

然後，重新整理 hello 專案相依性 tooget hello 二進位檔下載。

```JSON

    repositories {
      mavenCentral()
    }

    dependencies {
      compile group: 'com.microsoft.azure', name: 'applicationinsights-web', version: '1.+'
      // or applicationinsights-core for bare API
    }
```

* *建置或總和檢查碼驗證錯誤？嘗試使用特定版本，例如：* `version:'1.0.n'`。 *您可以找到 hello 最新版本中 hello [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)。*
* *tooupdate tooa 新的 SDK*
  * 請重新整理專案的相依項目。

#### <a name="otherwise-"></a>否則...
手動新增 hello SDK:

1. 下載 hello [Application Insights SDK for Java](https://aka.ms/aijavasdk)。
2. 從 hello zip 檔案解壓縮 hello 二進位檔，並將它們加入 tooyour 專案。

### <a name="questions"></a>問題...
* *Hello hello 之間的關係為何`-core`和`-web`hello zip 中的元件？*

  * `applicationinsights-core`提供 hello 裸機 API。 您一定需要此元件。
  * `applicationinsights-web` 提供追蹤 HTTP 要求計數和回應時間的度量。 如果您不想自動收集此原則，您可以忽略這個。 例如，如果您想 toowrite 自己。
* *tooupdate hello SDK 當我們發行變更時*

  * 下載最新的 hello [Application Insights SDK for Java](https://aka.ms/qqkaq6)和 hello 舊的取代。
  * 變更詳述於 hello [SDK 版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)。

## <a name="3-add-an-application-insights-xml-file"></a>3.加入 Application Insights .XML 檔案
新增 ApplicationInsights.xml toohello 資源 資料夾在專案中，或請確定它加入 tooyour 專案的部署類別路徑。 複製下列 XML 中的 hello。

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
* 事件相互關聯是加法 toohello HTTP 要求元件。 它會指派 hello 伺服器接收到的識別項 tooeach 要求，並將此識別項的遙測資料的屬性 tooevery 項目為新增為 hello 屬性 'Operation.Id'。 它可讓您藉由設定的篩選條件相關聯的每個要求 toocorrelate hello 遙測[診斷搜尋][diagnostic]。
* hello Application Insights 金鑰可以動態地從傳送 hello Azure 入口網站做為系統屬性 (-DAPPLICATION_INSIGHTS_IKEY = your_ikey)。 如果未定義任何屬性，它會檢查 Azure App 設定中的環境變數 (APPLICATION_INSIGHTS_IKEY)。 如果這兩個 hello 屬性未定義，從 ApplicationInsights.xml 使用 hello 預設 InstrumentationKey。 此順序可協助您 toomanage 不同環境的不同 InstrumentationKeys 動態。

### <a name="alternative-ways-tooset-hello-instrumentation-key"></a>替代方式 tooset hello 檢測金鑰
Application Insights SDK 會尋找此順序中的 hello 機碼：

1. 系統屬性：-DAPPLICATION_INSIGHTS_IKEY=your_ikey
2. 環境變數：APPLICATION_INSIGHTS_IKEY
3. 組態檔︰ApplicationInsights.xml

您也可以 [在程式碼中設定](app-insights-api-custom-events-metrics.md#ikey)：

```Java

    telemetryClient.InstrumentationKey = "...";
```

## <a name="4-add-an-http-filter"></a>4.加入 HTTP 篩選器
最後一個組態步驟 hello 可讓 hello HTTP 要求元件 toolog 每個 web 要求。 （不需如果您只想要 hello 裸機應用程式開發介面）。

找出並開啟您的專案，並合併 hello 下列程式碼 hello web 應用程式 節點下，您的應用程式篩選器設定的位置中的 hello web.xml 檔案。

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

#### <a name="if-youre-using-spring-web-mvc-31-or-later"></a>如果您使用 Spring Web MVC 3.1 或更新版本
編輯這些項目 *-servlet.xml tooinclude hello Application Insights 套件：

```XML

    <context:component-scan base-package=" com.springapp.mvc, com.microsoft.applicationinsights.web.spring"/>

    <mvc:interceptors>
        <mvc:interceptor>
            <mvc:mapping path="/**"/>
            <bean class="com.microsoft.applicationinsights.web.spring.RequestNameHandlerInterceptorAdapter" />
        </mvc:interceptor>
    </mvc:interceptors>
```

#### <a name="if-youre-using-struts-2"></a>如果您使用 Struts 2
加入此項目 toohello Struts 組態檔 （通常是具名的 struts.xml 或 struts default.xml）：

```XML

     <interceptors>
       <interceptor name="ApplicationInsightsRequestNameInterceptor" class="com.microsoft.applicationinsights.web.struts.RequestNameInterceptor" />
     </interceptors>
     <default-interceptor-ref name="ApplicationInsightsRequestNameInterceptor" />
```

（如果有定義預設堆疊中的攔截器，hello 攔截器可以只被加入 toothat 堆疊）。

## <a name="5-run-your-application"></a>5.執行您的應用程式
請在偵錯模式中執行您的開發電腦上或發行 tooyour 伺服器。

## <a name="6-view-your-telemetry-in-application-insights"></a>6.在 Application Insights 中檢視遙測
傳回在 tooyour Application Insights 資源[Microsoft Azure 入口網站](https://portal.azure.com)。

HTTP 要求資料會顯示 hello 概觀刀鋒視窗上。 (如果沒有出現，請稍等片刻，然後按一下重新整理。)

![範例資料](./media/app-insights-java-get-started/5-results.png)

[深入了解度量。][metrics]

按一下任何詳細的圖表 toosee 透過彙總度量資訊。

![](./media/app-insights-java-get-started/6-barchart.png)

> Application Insights 假設 hello 的 MVC 應用程式的 HTTP 要求的格式為： `VERB controller/action`。 例如，`GET Home/Product/f9anuh81`、`GET Home/Product/2dffwrf5` 和 `GET Home/Product/sdf96vws` 會分組至 `GET Home/Product`。 此分組方式可提供要求有意義的彙總，例如要求數量和要求的平均執行時間。
>
>

### <a name="instance-data"></a>執行個體資料
按一下瀏覽特定要求類型 toosee 個別執行個體。

Application Insights 中會顯示兩種類型的資料︰彙總資料 (儲存並顯示為平均值、計數和總和)；以及執行個體資料 (HTTP 要求、例外狀況、頁面檢視或自訂事件的個別報表)。

當檢視要求的 hello 屬性，您可以看到 hello 遙測事件與它相關聯，例如要求和例外狀況。

![](./media/app-insights-java-get-started/7-instance.png)

### <a name="analytics-powerful-query-language"></a>分析︰功能強大的查詢語言
因為您會累積更多資料，您可以在兩個 tooaggregate 資料和 toofind 個別執行個體時執行查詢。  [分析](app-insights-analytics.md) 是一項強大的工具，既可了解效能和使用情況，也可進行診斷。

![分析的範例](./media/app-insights-java-get-started/025.png)

## <a name="7-install-your-app-on-hello-server"></a>7.Hello 伺服器上安裝應用程式
現在來發行您的應用程式 toohello 伺服器，可讓您使用它，並留意 hello 遙測 hello 入口網站上顯示。

* 請確定您的防火牆允許應用程式 toosend 遙測 toothese 連接埠：

  * dc.services.visualstudio.com:443
  * f5.services.visualstudio.com:443

* 如果連出流量必須透過防火牆路由傳送，定義系統屬性 `http.proxyHost` 和 `http.proxyPort`。

* 在 Windows 伺服器上，安裝：

  * [Microsoft Visual C++ 可轉散發套件](http://www.microsoft.com/download/details.aspx?id=40784)

    (此元件會啟用效能計數器。)


## <a name="exceptions-and-request-failures"></a>例外狀況與要求失敗
會自動收集未處理的例外狀況：

![開啟 [設定]、[失敗]](./media/app-insights-java-get-started/21-exceptions.png)

toocollect 資料上的其他例外狀況，您有兩個選項：

* [插入程式碼中呼叫 tootrackException()][apiexceptions]。
* [在伺服器上安裝 hello Java 代理程式](app-insights-java-agent.md)。 您指定您想要 toowatch hello 方法。

## <a name="monitor-method-calls-and-external-dependencies"></a>監視方法呼叫和外部相依性
[安裝 hello Java 代理程式](app-insights-java-agent.md)toolog 指定內部方法與呼叫 JDBC，透過與計時資料。

## <a name="performance-counters"></a>效能計數器
開啟**設定**，**伺服器**，toosee 效能計數器的範圍。

![](./media/app-insights-java-get-started/11-perf-counters.png)

### <a name="customize-performance-counter-collection"></a>自訂效能計數器集合
toodisable hello 組標準的效能計數器集合加入下列程式碼的 hello ApplicationInsights.xml 檔案 hello 根節點下的 hello:

```XML
    <PerformanceCounters>
       <UseBuiltIn>False</UseBuiltIn>
    </PerformanceCounters>
```

### <a name="collect-additional-performance-counters"></a>收集其他效能計數器
您可以指定收集其他效能計數器 toobe。

#### <a name="jmx-counters-exposed-by-hello-java-virtual-machine"></a>JMX 計數器 （由 hello Java 虛擬機器）

```XML
    <PerformanceCounters>
      <Jmx>
        <Add objectName="java.lang:type=ClassLoading" attribute="TotalLoadedClassCount" displayName="Loaded Class Count"/>
        <Add objectName="java.lang:type=Memory" attribute="HeapMemoryUsage.used" displayName="Heap Memory Usage-used" type="composite"/>
      </Jmx>
    </PerformanceCounters>
```

* `displayName`– hello hello Application Insights 入口網站中顯示的名稱。
* `objectName`– hello JMX 物件名稱。
* `attribute`– hello JMX 物件名稱 toofetch hello 屬性
* `type`（選用）-hello JMX 物件屬性的型別：
  * 預設值：簡易類型，例如 int 或 long。
  * `composite`: hello 的效能計數器資料的格式的 'Attribute.Data' hello
  * `tabular`: hello 的效能計數器資料的資料表資料列的 hello 格式

#### <a name="windows-performance-counters"></a>Windows 效能計數器
每個[Windows 效能計數器](https://msdn.microsoft.com/library/windows/desktop/aa373083.aspx)類別目錄的成員 (在 hello 欄位是類別成員一樣)。 類別可以是全域，或可以有一定數量或指定的執行個體。

```XML
    <PerformanceCounters>
      <Windows>
        <Add displayName="Process User Time" categoryName="Process" counterName="%User Time" instanceName="__SELF__" />
        <Add displayName="Bytes Printed per Second" categoryName="Print Queue" counterName="Bytes Printed/sec" instanceName="Fax" />
      </Windows>
    </PerformanceCounters>
```

* displayName-hello hello Application Insights 入口網站中顯示的名稱。
* categoryName – hello 效能計數器分類 （效能物件） 與此效能計數器相關聯。
* counterName – hello hello 效能計數器名稱。
* instanceName – hello hello 效能計數器類別執行個體名稱或空字串 ("")，如果 hello 類別包含單一執行個體。 如果 hello categoryName 是程序，而您想要 toocollect hello 效能計數器從 hello 目前 JVM 程序上執行您的應用程式中，指定`"__SELF__"`。

您的效能計數器會在[計量瀏覽器][metrics]中以自訂度量的形式顯示。

![](./media/app-insights-java-get-started/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix 效能計數器
* [安裝與 hello Application Insights 外掛程式 collectd](app-insights-java-collectd.md) tooget 各種系統和網路的資料。

## <a name="get-user-and-session-data"></a>取得使用者與工作階段資料
好了，您現在正在從 Web 服務傳送遙測資料。 現在 tooget hello 完整 360 度檢視您的應用程式，您可以加入更多監視：

* [將遙測 tooyour web 網頁][ usage] toomonitor 頁面上，檢視和使用者度量。
* [設定 web 測試][ availability] toomake 即時且回應迅速，保持您的應用程式。

## <a name="capture-log-traces"></a>擷取記錄追蹤
您可以使用 Application Insights tooslice 並分析從 Log4J、 Logback 或其他的記錄架構的記錄檔。 您可以將 hello 記錄相互關聯的 HTTP 要求與其他遙測。 [了解作法][javalogs]。

## <a name="send-your-own-telemetry"></a>傳送您自己的遙測
既然您已安裝 hello SDK，您可以使用 hello API toosend 您自己的遙測。

* [追蹤的自訂事件和度量][ api] toolearn 哪些使用者運用您的應用程式。
* [搜尋事件和記錄檔][ diagnostic] toohelp 診斷問題。

## <a name="availability-web-tests"></a>可用性 Web 測試
Application Insights 可以測試您的網站在它已啟動的定期間隔 toocheck 和回應格式。 [向上 tooset][availability]，按一下 Web 測試。

![按一下 [Web 測試]，然後按一下 [新增 Web 測試]](./media/app-insights-java-get-started/31-config-web-test.png)

您將取得回應時間的圖表，以及若網站關閉還會取得電子郵件通知。

![Web 測試範例](./media/app-insights-java-get-started/appinsights-10webtestresult.png)

[深入了解 Web 測試的可用性。][availability]

## <a name="questions-problems"></a>有疑問嗎？ 有問題嗎？
[疑難排解 Java](app-insights-java-troubleshoot.md)

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next-steps"></a>後續步驟
* [監視相依性呼叫](app-insights-java-agent.md)
* [監視 Unix 效能計數器](app-insights-java-collectd.md)
* 新增[監視 tooyour 網頁](app-insights-javascript.md)toomonitor 頁面載入時間，AJAX 呼叫瀏覽器例外狀況。
* 寫入[自訂遙測](app-insights-api-custom-events-metrics.md)tootrack 使用量 hello 瀏覽器中，或是在 hello 伺服器。
* 建立[儀表板](app-insights-dashboards.md)toobring 一起 hello 重要圖表來監視您的系統。
* 使用[分析](app-insights-analytics.md)功能從您的應用程式透過遙測進行強大查詢
* 如需詳細資訊，請瀏覽[適用於 Java 開發人員的 Azure](/java/azure)。

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiexceptions]: app-insights-api-custom-events-metrics.md#trackexception
[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[eclipse]: app-insights-java-eclipse.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[usage]: app-insights-javascript.md
