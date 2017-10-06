---
title: "aaaGet 開始使用 Azure Application Insights 使用 Eclipse 中的 Java |Microsoft 文件"
description: "使用 hello Eclipse 外掛程式 tooadd 效能和使用量監視 tooyour Java 網站使用 Application Insights"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: e88c9f53-cd90-4abc-b097-1f170937908e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/12/2016
ms.author: bwren
ms.openlocfilehash: 3142a26a9e2d14c2c433882e3d337f2a8c8f2247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-application-insights-with-java-in-eclipse"></a>在 Eclipse 中利用 Java 開始使用 Application Insights
hello Application Insights SDK 從 Java web 應用程式傳送遙測，如此您可以分析使用量和效能。 以便讓您取得超出 hello 方塊遙測，加上您可以使用 toowrite 自訂遙測的 API，hello Eclipse 外掛程式的 Application Insights 會自動將 hello SDK 安裝在您的專案中。   

## <a name="prerequisites"></a>必要條件
目前 hello 外掛程式適用於 Maven 專案並在 Eclipse 中的動態 Web 專案。
([加入 Application Insights tooother 類型的 Java 專案][java]。)

您需要：

* Oracle JRE 1.6 或更新版本
* 訂用帳戶太[Microsoft Azure](https://azure.microsoft.com/)。
* [Eclipse IDE for Java EE Developers](http://www.eclipse.org/downloads/)、Indigo 或更新版本。
* Windows 7 或更新版本，或 Windows Server 2008 或更新版本

## <a name="install-hello-sdk-on-eclipse-one-time"></a>在 Eclipse （一次） 上安裝 hello SDK
您只需要 toodo 每台電腦一次。 這個步驟會安裝可接著將新增 hello SDK tooeach 動態 Web 專案的工具組。

1. 在 Eclipse 中，按一下 說明，然後按一下安裝新軟體。

    ![[說明] -> [安裝新軟體]](./media/app-insights-java-eclipse/0-plugin.png)
2. hello SDK 處於 http://dl.microsoft.com/eclipse，在 Azure Toolkit。
3. 取消勾選 **[連絡所有更新網站...]**

    ![針對 Application Insights SDK，請清除 [連絡所有更新網站]](./media/app-insights-java-eclipse/1-plugin.png)

請遵循 hello 剩餘步驟，針對每個 Java 專案。

## <a name="create-an-application-insights-resource-in-azure"></a>在 Azure 中建立 Application Insights 資源
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 建立新 Application Insights 資源。 設定 hello 應用程式類型 tooJava web 應用程式。  

    ![按一下 + 並選擇 [Application Insights]](./media/app-insights-java-eclipse/01-create.png)  

4. 尋找 hello hello 新資源的檢測金鑰。 您將需要 toopaste 此程式碼專案到很快。  

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-eclipse/03-key.png)  

## <a name="add-application-insights-tooyour-project"></a>將 Application Insights tooyour 專案
1. 將 Application Insights 從您的 Java web 專案的 hello 內容功能表。

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-eclipse/02-context-menu.png)
2. 貼上您從 hello Azure 入口網站取得的 hello 檢測金鑰。

    ![在新資源概觀 hello，按一下 內容並複製 hello 檢測金鑰](./media/app-insights-java-eclipse/03-ikey.png)

hello 金鑰會隨每個項目的遙測資料一起傳送，並告知 Application Insights toodisplay 在您的資源。

## <a name="run-hello-application-and-see-metrics"></a>執行 hello 應用程式，並查看度量
執行您的應用程式。

在 Microsoft Azure 中傳回 tooyour Application Insights 資源。

HTTP 要求資料會出現在 hello 概觀刀鋒視窗。 (如果沒有出現，請稍等片刻，然後按一下重新整理。)

![伺服器回應、要求計數和失敗 ](./media/app-insights-java-eclipse/5-results.png)

按一下 透過任何圖表 toosee 度量詳細資訊。

![依名稱的要求計數](./media/app-insights-java-eclipse/6-barchart.png)

[深入了解度量。][metrics]

與檢視之要求的 hello 屬性，您會看見 hello 遙測事件與它相關聯，例如要求和例外狀況。

![此要求的所有追蹤](./media/app-insights-java-eclipse/7-instance.png)

## <a name="client-side-telemetry"></a>用戶端遙測
從 hello 快速入門刀鋒視窗中，按一下 取得程式碼 toomonitor 我的網頁：

![在您的應用程式概觀刀鋒視窗中，選擇 [快速啟動]，取得程式碼 toomonitor 我的網頁。 複製 hello 指令碼。](./media/app-insights-java-eclipse/02-monitor-web-page.png)

中的 HTML 檔案的 hello 開頭插入 hello 程式碼片段。

#### <a name="view-client-side-data"></a>檢視用戶端資料
開啟您已更新的網頁，並使用它們。 等待一兩分鐘，然後再返回 tooApplication Insights 和開啟 hello 使用量刀鋒視窗。 （從 hello 概觀刀鋒視窗中，向下捲動並按一下 使用方式）。

頁面檢視、 使用者和工作階段計量會顯示 hello 使用量刀鋒視窗上：

![工作階段、使用者和頁面檢視](./media/app-insights-java-eclipse/appinsights-47usage-2.png)

[深入了解設定用戶端遙測。][usage]

## <a name="publish-your-application"></a>發佈您的應用程式
現在來發行您的應用程式 toohello 伺服器，可讓您使用它，並留意 hello 遙測 hello 入口網站上顯示。

* 請確定您的防火牆允許應用程式 toosend 遙測 toothese 連接埠：

  * dc.services.visualstudio.com:443
  * dc.services.visualstudio.com:80
  * f5.services.visualstudio.com:443
  * f5.services.visualstudio.com:80
* 在 Windows 伺服器上，安裝：

  * [Microsoft Visual C++ 可轉散發套件](http://www.microsoft.com/download/details.aspx?id=40784)

    (這會啟用效能計數器。)

## <a name="exceptions-and-request-failures"></a>例外狀況與要求失敗
會自動收集未處理的例外狀況：

![](./media/app-insights-java-eclipse/21-exceptions.png)

toocollect 資料上的其他例外狀況，您有兩個選項：

* [插入程式碼中呼叫 tooTrackException](app-insights-api-custom-events-metrics.md#trackexception)。
* [在伺服器上安裝 hello Java 代理程式](app-insights-java-agent.md)。 您指定您想要 toowatch hello 方法。

## <a name="monitor-method-calls-and-external-dependencies"></a>監視方法呼叫和外部相依性
[安裝 hello Java 代理程式](app-insights-java-agent.md)toolog 指定內部方法與呼叫 JDBC，透過與計時資料。

## <a name="performance-counters"></a>效能計數器
在您概觀刀鋒視窗中，向下捲動並按一下 hello**伺服器**磚。 您會看到一些效能計數器。

![捲動 tooclick hello 伺服器 磚](./media/app-insights-java-eclipse/11-perf-counters.png)

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

![](./media/app-insights-java-eclipse/12-custom-perfs.png)

### <a name="unix-performance-counters"></a>Unix 效能計數器
* [安裝與 hello Application Insights 外掛程式 collectd](app-insights-java-collectd.md) tooget 各種系統和網路的資料。

## <a name="availability-web-tests"></a>可用性 Web 測試
Application Insights 可以測試您的網站在它已啟動的定期間隔 toocheck 和回應格式。 [向上 tooset][availability]，捲動 tooclick 可用性。

![向下捲動，並依序按一下 [可用性]、[加入 Web 測試]](./media/app-insights-java-eclipse/31-config-web-test.png)

您將取得回應時間的圖表，以及若網站關閉還會取得電子郵件通知。

![Web 測試範例](./media/app-insights-java-eclipse/appinsights-10webtestresult.png)

[深入了解 Web 測試的可用性。][availability]

## <a name="diagnostic-logs"></a>診斷記錄檔
如果您使用 Logback 或 Log4J （v1.2 或 v2.0） 進行追蹤，您可以將自動傳送 tooApplication Insights，您可以在其中瀏覽並在其上搜尋程式追蹤記錄。

[深入了解診斷記錄][javalogs]

## <a name="custom-telemetry"></a>自訂遙測
在使用者與它的行為時您 Java web 應用程式 toofind 中插入幾行程式碼或 toohelp 診斷問題。

在網頁 JavaScript 和 hello 伺服器端 Java 中，您可以插入程式碼。

[了解自訂遙測][track]

## <a name="next-steps"></a>後續步驟
#### <a name="detect-and-diagnose-issues"></a>偵測並診斷問題
* [新增 web 用戶端遙測][ usage] tooget hello web 用戶端效能遙測資料。
* [設定 web 測試][ availability] toomake 即時且回應迅速，保持您的應用程式。
* [搜尋事件和記錄檔][ diagnostic] toohelp 診斷問題。
* [擷取 Log4J 或 Logback 追蹤][javalogs]

#### <a name="track-usage"></a>追蹤流量
* [新增 web 用戶端遙測][ usage] toomonitor 頁面上，檢視和基本使用者度量。
* [追蹤的自訂事件和度量](app-insights-web-track-usage.md)toolearn 有關您的應用程式使用方式，在 hello 用戶端和伺服器 hello。

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[diagnostic]: app-insights-diagnostic-search.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[metrics]: app-insights-metrics-explorer.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md
