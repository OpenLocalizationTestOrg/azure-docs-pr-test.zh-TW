---
title: "疑難排解 Java Web 專案中的 Application Insights"
description: "疑難排解指南 - 使用 Application Insights 監視即時的 Java 應用程式。"
services: application-insights
documentationcenter: java
author: mrbullwinkle
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: mbullwin
ms.openlocfilehash: 6b1cfa2b52e8e9e2b6a8ab87be6d4269cbe3f1cf
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Application Insights for Java 的疑難排解和問答集
[Java 中的 Azure Application Insights][java] 疑問或問題？ 以下是一些秘訣。

## <a name="build-errors"></a>建置錯誤
**在 Eclipse 中，透過 Maven 或 Gradle 加入 Application Insights SDK 時，我收到建置或總和檢查碼驗證錯誤。**

* 如果相依性 <version> 元素使用具有萬用字元的模式 (例如 (Maven) `<version>[1.0,)</version>` 或 (Gradle) `version:'1.0.+'`)，請嘗試改為指定特定版本 (例如 `1.0.2`)。 請參閱最新版本的 [版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) 。

## <a name="no-data"></a>沒有資料
**我已成功加入 Application Insights 並執行我的應用程式，但在入口網站中從未看到資料。**

* 請稍等片刻，然後按一下 [重新整理]。 圖表會定期自行重新整理，但您也可以手動重新整理。 重新整理間隔取決於圖表的時間範圍。
* 檢查 ApplicationInsights.xml 檔案 (位於專案的 resources 資料夾) 中已定義檢測機碼
* 確認 xml 檔案中沒有 `<DisableTelemetry>true</DisableTelemetry>` 節點。
* 在防火牆中，您可能必須開啟 TCP 連接埠 80 和 443，以允許連出流量送往 dc.services.visualstudio.com。請參閱 [完整的防火牆例外狀況清單](app-insights-ip-addresses.md)
* 在 Microsoft Azure 開始面板中，查看服務狀態對應。 如果看到一些警示指示，請等待它們恢復 [正常]，然後關閉再重新開啟 Application Insights 應用程式刀鋒視窗。
* 在 ApplicationInsights.xml 檔案 (位於專案的 resources 資料夾) 的根節點下加入 `<SDKLogger />` 元素，即可開啟記錄至 IDE 主控台視窗，然後檢查前面加上 [Error] 的項目。
* 藉由查看主控台的輸出訊息「已成功找到組態檔」陳述式，確定 Java SDK 已成功載入正確的 ApplicationInsights.xml 檔案。
* 如果找不到組態檔，請檢查輸出訊息以查看在何處搜尋組態檔，並確定 ApplicationInsights.xml 位在這些搜尋位置中的其中一個位置。 根據經驗法則，您可以將組態檔置於 Application Insights SDK JAR 附近。 例如：在 Tomcat 中，這可能表示 WEB-INF/lib 資料夾。

#### <a name="i-used-to-see-data-but-it-has-stopped"></a>我曾經看到資料，但是已停止
* 檢查 [狀態部落格](http://blogs.msdn.com/b/applicationinsights-status/)。
* 您有達到資料點的每月配額嗎？ 開啟 [設定/配額和定價] 即可查看。若有達到配額，您可以升級您的方案，或付費取得額外容量。 請參閱 [定價配置](https://azure.microsoft.com/pricing/details/application-insights/)。

#### <a name="i-dont-see-all-the-data-im-expecting"></a>我並沒有看到預期的所有資料
* 開啟 [配額和價格] 刀鋒視窗，檢查是否正在進行 [取樣](app-insights-sampling.md) 。 (100% 傳輸表示目前未進行取樣。)Application Insights 服務可以設定為只接受來自您的應用程式的一小部分遙測。 這有助於您維持在每月的遙測配額內。 

## <a name="no-usage-data"></a>沒有使用狀況資料
**我看到要求和回應時間的相關資料，但沒有看到頁面檢視、瀏覽器或使用者資料的相關資料。**

您已成功設定應用程式從伺服器傳送遙測。 現在，您的下一步是[設定網頁，以從網頁瀏覽器傳送遙測][usage]。

或者，如果您的用戶端是[手機或其他裝置][platforms]中的應用程式，則可以從該處傳送遙測。 

使用相同的檢測機碼來設定用戶端和伺服器遙測。 資料會出現在相同的 Application Insights 資源中，而且您可以相互關聯來自用戶端和伺服器的事件。


## <a name="disabling-telemetry"></a>停用遙測
**如何停用遙測收集？**

在程式碼中：

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**或** 

更新 ApplicationInsights.xml (位於專案的 resources 資料夾)。 在根節點下加入下列程式碼：

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

如果使用 XML 方法，則必須在變更值時重新啟動應用程式。

## <a name="changing-the-target"></a>變更目標
**如何變更我的專案將資料傳送到哪一個 Azure 資源？**

* [取得新資源的檢測金鑰。][java]
* 如果您已使用 Azure Toolkit for Eclipse 將 Application Insights 新增到您的專案，請在 Web 專案上按一下滑鼠右鍵，依序選取 [Azure] 和 [設定 Application Insights]，然後變更金鑰。
* 否則，請更新專案之 resources 資料夾的 ApplicationInsights.xml 中的機碼。

## <a name="debug-data-from-the-sdk"></a>從 SDK 進行資料偵錯

**如何找出 SDK 正在做什麼？**

若要取得有關 API 中所進行作業的詳細資訊，請在 ApplicationInsights.xml 組態檔的根節點底下新增 `<SDKLogger/>`。

您也可以指示記錄器輸出至檔案：

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

如果是 Tomcat 伺服器，檔案可以在 `%temp%\javasdklogs` 或 `java.io.tmpdir` 底下找到。


## <a name="the-azure-start-screen"></a>Azure 開始畫面
**我正在查看 [Azure 入口網站](https://portal.azure.com)。地圖是否告知有關我的應用程式的相關資訊？**

否，它會顯示世界各地 Azure 伺服器的健全狀況。

*從 Azure 開始面板 (主畫面) 中，如何找到我應用程式的相關資料？*

假設您已[設定 Application Insights 的應用程式][java]，請按一下 [瀏覽]，選取 [Application Insights]，然後選取您為應用程式建立的應用程式資源。 日後若要更快速地從該處開始，您可以將應用程式釘選至開始面板。

## <a name="intranet-servers"></a>內部網路伺服器
**可以在我的內部網路上監視伺服器嗎？**

是，前提是您的伺服器可以透過公用網際網路將遙測傳送至 Application Insights 入口網站。 

在防火牆中，您可能必須開啟 TCP 連接埠 80 和 443，以允許連出流量送往 dc.services.visualstudio.com 和 f5.services.visualstudio.com。

## <a name="data-retention"></a>資料保留
**資料保留在入口網站多久的時間？是否安全？**

請參閱[資料保留和隱私權][data]。

## <a name="debug-logging"></a>偵錯記錄
Application insights 會使用 `org.apache.http`。 這會重新配置在 Application Insights 核心 Jar 內的 `com.microsoft.applicationinsights.core.dependencies.http` 命名空間底下。 這可讓 Application Insights 處理相同 `org.apache.http` 的不同版本都存在於一個核心程式碼基底中的情況。 

>[!NOTE]
>如果您針對應用程式中的所有命名空間啟用 DEBUG 層級的記錄功能，它將適用於所有執行中的模組，包括已重新命名為 `com.microsoft.applicationinsights.core.dependencies.http` 的 `org.apache.http`。 Application Insights 將無法針對這些呼叫套用篩選，因為正在由 Apache 程式庫發出記錄呼叫。 DEBUG 層級記錄會產生相當大量的記錄資料，因此不建議用於即時生產環境執行個體。


## <a name="next-steps"></a>後續步驟
**設定 Java 伺服器應用程式的 Application Insights。我還可以做什麼？**

* [監視網頁可用性][availability]
* [監視網頁使用狀況][usage]
* [追蹤使用狀況並診斷裝置應用程式中的問題][platforms]
* [撰寫程式碼以追蹤應用程式使用狀況][track]
* [擷取診斷記錄][javalogs]

## <a name="get-help"></a>取得說明
* [堆疊溢位](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

