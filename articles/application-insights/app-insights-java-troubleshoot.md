---
title: "在 Java web 專案中的 Application Insights aaaTroubleshoot"
description: "疑難排解指南 - 使用 Application Insights 監視即時的 Java 應用程式。"
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Application Insights for Java 的疑難排解和問答集
[Java 中的 Azure Application Insights][java] 疑問或問題？ 以下是一些秘訣。

## <a name="build-errors"></a>建置錯誤
**在 Eclipse 中，加入 hello Application Insights SDK，透過 Maven 或 Gradle，我會收到建置或總和檢查碼驗證錯誤。**

* 如果 hello 相依性<version>項目使用具有萬用字元的模式 (例如 (Maven)`<version>[1.0,)</version>`或 (Gradle) `version:'1.0.+'`)，請嘗試指定特定版本來取代像是`1.0.2`。 請參閱 hello[版本資訊](https://github.com/Microsoft/ApplicationInsights-Java#release-notes)hello 最新版本。

## <a name="no-data"></a>沒有資料
**我已成功加入 Application Insights 並執行我的應用程式，但從未 hello 入口網站中的資料。**

* 請稍等片刻，然後按一下 [重新整理]。 hello 圖表定期重新整理本身，但您也可以手動更新。 hello 重新整理間隔取決於 hello 的 hello 圖表的時間範圍。
* 請確認您已在 hello ApplicationInsights.xml 檔 （在專案中的 hello 資源資料夾） 中定義的檢測金鑰
* 確認沒有任何`<DisableTelemetry>true</DisableTelemetry>`hello xml 檔案中的節點。
* 在您的防火牆，您可能必須 tooopen TCP 連接埠 80 和 443 供連出流量 toodc.services.visualstudio.com。請參閱 hello[的防火牆例外狀況的完整清單](app-insights-ip-addresses.md)
* Hello Microsoft Azure 中啟動 面板，請查看 hello 服務狀態對應。 如果有某些警示的指示，請等到它們都傳回 tooOK 然後關閉再重新開啟 Application Insights 的應用程式刀鋒視窗。
* 開啟 記錄 toohello IDE 主控台視窗中，藉由新增`<SDKLogger />`hello hello ApplicationInsights.xml 檔案 （在 hello 資源資料夾在專案中），並檢查 [錯誤] 開頭處的項目中的根節點下的項目。
* 請確定該 hello 正確 ApplicationInsights.xml 檔案已成功載入 hello Java SDK 所查看的 」 組態檔已成功找到"陳述式的 hello 主控台輸出訊息。
* 如果找不到 hello 設定檔，請檢查 hello 輸出訊息 toosee hello 設定檔，要搜尋位置，並確定 ApplicationInsights.xml 位於其中一個這些搜尋位置中的 hello。 根據經驗法則，您可以將附近 hello 應用程式 Insights SDK Jar hello 設定檔。 例如： 在 Tomcat 中，這表示 hello WEB-INF/lib 資料夾。

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>我使用 toosee 資料，但它已停止
* 檢查 hello[狀態部落格](http://blogs.msdn.com/b/applicationinsights-status/)。
* 您有達到資料點的每月配額嗎？ 開啟 設定/配額和定價 toofind 出。若有達到配額，您可以升級您的方案，或付費取得額外容量。 請參閱 hello[定價配置](https://azure.microsoft.com/pricing/details/application-insights/)。

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>我看不到我預期的所有 hello 資料
* 開啟 hello 配額和定價刀鋒視窗，然後檢查是否[取樣](app-insights-sampling.md)在作業。 （100%傳輸表示取樣，即不會在作業中）。hello Application Insights 服務可以設定 tooaccept 只有一小部份 hello 遙測來自您的應用程式。 這有助於您維持在每月的遙測配額內。 

## <a name="no-usage-data"></a>沒有使用狀況資料
**我看到要求和回應時間的相關資料，但沒有看到頁面檢視、瀏覽器或使用者資料的相關資料。**

您已成功設定應用程式 toosend 遙測從 hello 伺服器。 現在您的下一個步驟太[設定 hello 網頁瀏覽器從您網頁 toosend 遙測][usage]。

或者，如果您的用戶端是[手機或其他裝置][platforms]中的應用程式，則可以從該處傳送遙測。 

使用 hello 相同檢測金鑰 tooset 註冊用戶端和伺服器遙測。 hello 相同的 Application Insights 資源，以及您可以從用戶端和伺服器可以 toocorrelate 事件，會出現在 hello 資料。


## <a name="disabling-telemetry"></a>停用遙測
**如何停用遙測收集？**

在程式碼中：

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**或** 

更新 ApplicationInsights.xml （在專案中的 hello 資源資料夾）。 加入 hello hello 根節點下的下列：

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

當您變更 hello 值時，使用 hello XML 方法時，有 toorestart hello 應用程式。

## <a name="changing-hello-target"></a>變更 hello 目標
**如何變更我的專案將資料傳送到哪一個 Azure 資源？**

* [收到 hello hello 新資源的檢測金鑰。][java]
* 如果您加入 Application Insights tooyour 專案使用 hello Azure Toolkit for Eclipse，以滑鼠右鍵按一下您的 web 專案中，選取**Azure**，**設定 Application Insights**，並變更 hello 索引鍵。
* 否則，請更新中 ApplicationInsights.xml hello 資源 資料夾中您的專案中的 hello 索引鍵。

## <a name="debug-data-from-hello-sdk"></a>偵錯 hello SDK 的資料

**如何得知哪些 hello SDK 執行的動作？**

tooget hello API 中的情況的詳細資訊加入`<SDKLogger/>`hello hello ApplicationInsights.xml 組態檔的根節點下。

您也可以指示 hello 記錄器 toooutput tooa 檔案：

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

您可以找到 hello 檔案`%temp%\javasdklogs`或`java.io.tmpdir`發生 Tomcat 伺服器。


## <a name="hello-azure-start-screen"></a>hello Azure 開始 畫面
**我正在尋找在[hello Azure 入口網站](https://portal.azure.com)。沒有 hello 對應告訴我的項目有關我的應用程式嗎？**

否，它會顯示 hello 健全狀況的 Azure 伺服器 hello 世界各地。

*從 hello Azure 開始面板 （主畫面），如何尋找資料我的應用程式？*

假設您[設定您的應用程式的 Application Insights][java]、 按一下 瀏覽、 選取 Application Insights 和選取您建立應用程式的 hello 應用程式資源。 tooget 那里在未來更快，您可以釘選您的應用程式 toohello 開始面板。

## <a name="intranet-servers"></a>內部網路伺服器
**可以在我的內部網路上監視伺服器嗎？**

是，提供您的伺服器可以傳送遙測 toohello Application Insights 入口網站來完成 hello 公用網際網路。 

在您的防火牆，您可能必須 tooopen TCP 連接埠 80 和 443 供連出流量 toodc.services.visualstudio.com 和 f5.services.visualstudio.com。

## <a name="data-retention"></a>資料保留
**資料保留多久 hello 入口網站中？是否安全？**

請參閱[資料保留和隱私權][data]。

## <a name="next-steps"></a>後續步驟
**設定 Java 伺服器應用程式的 Application Insights。我還可以做什麼？**

* [監視網頁可用性][availability]
* [監視網頁使用狀況][usage]
* [追蹤使用狀況並診斷裝置應用程式中的問題][platforms]
* [撰寫您的應用程式的程式碼 tootrack 使用量][track]
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

