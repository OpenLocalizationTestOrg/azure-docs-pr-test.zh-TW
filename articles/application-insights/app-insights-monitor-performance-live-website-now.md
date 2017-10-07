---
title: "aaaMonitor 即時的 ASP.NET web 應用程式與 Azure Application Insights |Microsoft 文件"
description: "監視網站的效能而不重新部署網站。 使用裝載於內部部署、VM 中或 Azure 上的 ASP.NET Web 應用程式。"
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 769a5ea4-a8c6-4c18-b46c-657e864e24de
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: bwren
ms.openlocfilehash: 0d53f0a59974f40767fae681bafc4f358d1283a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="instrument-web-apps-at-runtime-with-application-insights"></a>在執行階段使用 Application Insights 檢測 Web 應用程式


您可以檢測即時 web 應用程式使用 Azure Application Insights，而不需要 toomodify 或重新部署您的程式碼。 如果您的應用程式是由內部部署 IIS 伺服器裝載，請安裝狀態監視器。 如果它們是 Azure web 應用程式，或在 Azure VM 中執行，您可以切換 hello Azure 控制台中的 Application Insights 監視。 (我們還提供有關檢測[即時 J2EE Web 應用程式](app-insights-java-live.md)和 [Azure 雲端服務](app-insights-cloudservices.md)的個別文章)。您需要 [Microsoft Azure](http://azure.com) 訂用帳戶。

![範例圖表](./media/app-insights-monitor-performance-live-website-now/10-intro.png)

您可以選擇三個路由 tooapply Application Insights tooyour.NET web 應用程式：

* **建置時間：** [新增 hello Application Insights SDK] [ greenbrown] tooyour web 應用程式程式碼。
* **執行階段：**檢測 hello 伺服器上的 web 應用程式，如下所述，而不需要重建並重新部署 hello 程式碼。
* **兩者：** hello SDK 建置成 web 應用程式程式碼，以及也適用於 hello 執行階段擴充。 取得兩個選項的最佳 hello。

以下是您可在每種途徑中取得的優勢摘要︰

|  | 建置階段 | 執行階段 |
| --- | --- | --- |
| 要求和例外狀況 |是 |是 |
| [更詳細的例外狀況](app-insights-asp-net-exceptions.md) | |是 |
| [相依性診斷](app-insights-asp-net-dependencies.md) |在 .Net 4.6 + 上，但較少細節 |是，完整詳細資料︰結果碼、SQL 命令文字、HTTP 指令動詞|
| [系統效能計數器](app-insights-performance-counters.md) |是 |是 |
| [自訂遙測的 API][api] |是 |否 |
| [追蹤記錄檔整合](app-insights-asp-net-trace-logs.md) |是 |否 |
| [頁面檢視和使用者資料](app-insights-javascript.md) |是 |否 |
| 需要 toorebuild 程式碼 |是 | 否 |


## <a name="monitor-a-live-azure-web-app"></a>監視即時 Azure Web 應用程式

如果您的應用程式正在執行做為 Azure web 服務，這裡的方式，來監視 tooswitch:

* 在 Azure 中的 hello 應用程式的控制面板上選取 Application Insights。

    ![針對 Azure Web 應用程式設定 Application Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-setup.png)
* Hello Application Insights 摘要 頁面開啟時，按一下 hello hello 底部 tooopen hello 完整的 Application Insights 資源連結。

    ![按一下 透過 tooApplication Insights](./media/app-insights-monitor-performance-live-website-now/azure-web-view-more.png)

[監視雲端和 VM 應用程式](app-insights-azure.md)。

### <a name="enable-client-side-monitoring-in-azure"></a>在 Azure 中啟用用戶端監視

如果您已在 Azure 中啟用 Application Insights，即可新增頁面檢視和使用者遙測。

1. 選取 [設定] > [應用程式設定]
2.  在 [應用程式設定] 之下，新增索引鍵值組︰ 
   
    索引鍵︰`APPINSIGHTS_JAVASCRIPT_ENABLED` 
    
    值: `true`
3. **儲存**hello 設定和**重新啟動**您的應用程式。

hello Application Insights JavaScript SDK 現在插入每個網頁。

## <a name="monitor-a-live-iis-web-app"></a>監視即時 IIS Web 應用程式

如果您的應用程式裝載於 IIS 伺服器上，請使用狀態監視器來啟用 Application Insights。

1. 在 IIS Web 伺服器上，以系統管理員認證登入。
2. 如果尚未安裝 Application Insights 狀態監視器，下載並執行 hello[狀態監視安裝程式](http://go.microsoft.com/fwlink/?LinkId=506648)(或執行[Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx) ，並在其中搜尋應用程式 Insights 狀態監視）。
3. 在狀態監視器中，選取 hello 安裝 web 應用程式或您想 toomonitor 的網站。 利用您的 Azure 認證登入。

    設定您想要 toosee hello 結果 hello Application Insights 入口網站中的 hello 資源。 （通常是最佳 toocreate 新的資源。 如果您已經為此應用程式設定 [Web 測試][availability]或[用戶端監視][client]，請選取現有的資源。) 

    ![選擇應用程式和資源。](./media/app-insights-monitor-performance-live-website-now/appinsights-036-configAIC.png)

4. 重新啟動 IIS。

    ![選擇在 hello hello 對話方塊頂端的重新啟動。](./media/app-insights-monitor-performance-live-website-now/appinsights-036-restart.png)

    您的 Web 服務會中斷一小段時間。

## <a name="customize-monitoring-options"></a>自訂監視選項

啟用 Application Insights 加入 Dll 和 ApplicationInsights.config tooyour web 應用程式。 您可以[編輯 hello.config 檔案](app-insights-configuration-with-applicationinsights-config.md)toochange 部份 hello 選項。

## <a name="when-you-re-publish-your-app-re-enable-application-insights"></a>當您重新發佈您的應用程式時，請重新啟用 Application Insights。

在重新發行應用程式之前，請考慮[Visual Studio 中加入 Application Insights toohello 程式碼][greenbrown]。 您會取得更詳細的遙測和 hello 能力 toowrite 自訂遙測。

如果您想 toore-發行，而不加入 Application Insights toohello 程式碼，請注意，hello 部署程序可能會刪除 hello Dll 並從 hello ApplicationInsights.config 發行網站。 因此：

1. 如果您已編輯 ApplicationInsights.config，請在重新發佈應用程式前複製一份。
2. 重新發佈您的應用程式。
3. 重新啟用 Application Insights 監視功能。 (使用 hello 適當的方法： hello Azure web 應用程式控制項面板或 IIS 主機上的 hello 狀態監視器。)
4. 恢復所有您在 hello.config 檔案執行的編輯。


## <a name="troubleshooting-runtime-configuration-of-application-insights"></a>針對 Application Insights 的執行階段組態進行疑難排解

### <a name="cant-connect-no-telemetry"></a>無法連接？ 沒有遙測資料？

* 開啟[hello 必要的外寄連接埠](app-insights-ip-addresses.md#outgoing-ports)中伺服器的防火牆 tooallow 狀態監視器 toowork。

* 開啟狀態監視器，然後選取左窗格中的應用程式。 檢查是否有此應用程式在 hello [設定通知] 區段中的任何診斷訊息：

  ![開啟 hello 效能刀鋒視窗 toosee 要求、 回應時間、 相依性和其他資料](./media/app-insights-monitor-performance-live-website-now/appinsights-status-monitor-diagnostics-message.png)
* Hello 在伺服器上，如果您看到有關 「 權限不足 」 的訊息，請嘗試 hello 下列：
  * 在 [IIS 管理員] 中，選取您應用程式集區中，開啟**進階設定**，然後在**處理序模型**請注意 hello 身分識別。
  * 在電腦管理控制台中，新增此身分識別 toohello Performance Monitor Users 群組。
* 如果您的伺服器上已安裝 MMA/SCOM (Microsoft Operations Management Suite)，某些版本可能會發生衝突。 解除安裝 SCOM 和狀態監視，並重新安裝 hello 最新版本。
* 請參閱[疑難排解][qna]。

## <a name="system-requirements"></a>系統需求
支援伺服器上 Application Insights 狀態監視器的作業系統：

* Windows Server 2008
* Windows Server 2008 R2
* Windows Server 2012
* Windows Server 2012 R2
* Windows Server 2016

(含最新版 SP 和 .NET Framework 4.5)

Hello 用戶端上： Windows 7、 8、 8.1 和 10，一次使用.NET Framework 4.5

IIS 支援：IIS 7、7.5、8、8.5 (需要有 IIS)

## <a name="automation-with-powershell"></a>使用 PowerShell 進行自動化
您可以在 IIS 伺服器上使用 PowerShell 啟動和停止監視。

第一次匯入 hello Application Insights 模組：

`Import-Module 'C:\Program Files\Microsoft Application Insights\Status Monitor\PowerShell\Microsoft.Diagnostics.Agent.StatusMonitor.PowerShell.dll'`

找出受監視的應用程式︰

`Get-ApplicationInsightsMonitoringStatus [-Name appName]`

* `-Name`（選擇性） hello 的 web 應用程式的名稱。
* 顯示 hello 這個 IIS 伺服器中的 Application Insights 監視狀態，每個 web 應用程式 （或 hello 名為應用程式）。
* 傳回每個應用程式的 `ApplicationInsightsApplication`︰

  * `SdkState==EnabledAfterDeployment`： 應用程式正受到監視，與 hello 狀態監視工具，或藉由已檢測執行階段`Start-ApplicationInsightsMonitoring`。
  * `SdkState==Disabled`: hello 應用程式則不會檢測 Application Insights。 它永遠不會檢測，或是使用 hello 狀態監視工具，或使用執行階段監視已停用`Stop-ApplicationInsightsMonitoring`。
  * `SdkState==EnabledByCodeInstrumentation`: hello 應用程式已檢測加入 hello SDK toohello 來源的程式碼。 其 SDK 無法更新或停止。
  * `SdkVersion`顯示 hello 版本中用來監視此應用程式。
  * `LatestAvailableSdkVersion`顯示目前可用的 hello 版本 hello NuGet gallery 上。 tooupgrade hello 應用程式 toothis 版本，使用`Update-ApplicationInsightsMonitoring`。

`Start-ApplicationInsightsMonitoring -Name appName -InstrumentationKey 00000000-000-000-000-0000000`

* `-Name`hello 在 IIS 中的 hello 應用程式名稱
* `-InstrumentationKey`hello ikey 的 hello 您想要顯示 hello 結果 toobe Application Insights 資源。
* 這個 Cmdlet 只會影響尚未檢測的應用程式，也就是 SdkState==NotInstrumented。

    hello cmdlet 不會影響已檢測的應用程式。 它不不管 hello 應用程式已在建置階段檢測將 hello SDK toohello 程式碼，或在執行階段的先前使用這個 cmdlet。

    hello SDK 版本使用 tooinstrument hello 應用程式是最近的 hello 版本 toothis 伺服器。

    toodownload hello 最新版本，使用 Update ApplicationInsightsVersion。
* 成功時會傳回 `ApplicationInsightsApplication` 。 如果失敗，就會記錄追蹤 toostderr。

          Name                      : Default Web Site/WebApp1
          InstrumentationKey        : 00000000-0000-0000-0000-000000000000
          ProfilerState             : ApplicationInsights
          SdkState                  : EnabledAfterDeployment
          SdkVersion                : 1.2.1
          LatestAvailableSdkVersion : 1.2.3

`Stop-ApplicationInsightsMonitoring [-Name appName | -All]`

* `-Name`hello 在 IIS 中的應用程式名稱
* `-All` 停止監視此 IIS 伺服器中所有 `SdkState==EnabledAfterDeployment` 的應用程式
* 停止監視 hello 指定應用程式，並移除檢測。 僅適用於在執行階段使用已檢測的應用程式 hello 狀態監視工具或開始 ApplicationInsightsApplication 的。 (`SdkState==EnabledAfterDeployment`)
* 傳回 ApplicationInsightsApplication。

`Update-ApplicationInsightsMonitoring -Name appName [-InstrumentationKey "0000000-0000-000-000-0000"`]

* `-Name`: hello 的 web 應用程式在 IIS 中的名稱。
* `-InstrumentationKey` (選擇性)。使用此 toochange hello 資源 toowhich hello 應用程式的遙測傳送。
* 此 Cmdlet：
  * 名為應用程式 toohello 版的 hello SDK 升級 hello 最近下載 toothis 機器。 (僅適用於 `SdkState==EnabledAfterDeployment`時)
  * 如果您提供的檢測金鑰時，名為應用程式的 hello 是重新設定的 toosend 遙測 toohello 資源與該索引鍵。 (適用於 `SdkState != Disabled`時)

`Update-ApplicationInsightsVersion`

* 下載最新版 Application Insights SDK toohello 伺服器 hello。

## <a name="questions"></a>狀態監視器的相關問題

### <a name="what-is-status-monitor"></a>什麼是狀態監視器？

您在 IIS Web 伺服器中安裝的桌面應用程式。 它可協助您檢測和設定 Web 應用程式。 

### <a name="when-do-i-use-status-monitor"></a>如何使用狀態監視器？

* tooinstrument 任何 web 應用程式執行您的 IIS 伺服器-即使已在執行。
* web 應用程式已 tooenable 其他遙測[hello Application Insights SDK 以建置](app-insights-asp-net.md)在編譯時間。 

### <a name="can-i-close-it-after-it-runs"></a>是否可以在執行之後將它關閉？

是。 它也已檢測您選取的 hello 網站之後，您可以將它關閉。

它本身不會收集遙測資料。 它只會設定 hello web 應用程式，並設定某些權限。

### <a name="what-does-status-monitor-do"></a>狀態監視器有何作用？

當您選取狀態監視 tooinstrument web 應用的程式：

* 下載並置於 hello web 應用程式的二進位檔案的資料夾中的 hello Application Insights 組件和.config 檔案。
* 修改`web.config`tooadd hello 應用程式 Insights HTTP 追蹤模組。
* 啟用 CLR 程式碼分析 toocollect 相依性呼叫。

### <a name="do-i-need-toorun-status-monitor-whenever-i-update-hello-app"></a>每當更新 hello 應用程式是否需要 toorun 狀態監視器？

如果您是以累加方式重新部署，則不需要。 

如果您選取 hello '刪除現有檔案' 選項在 hello 發佈程序，您需要 toore 執行狀態監視器 tooconfigure Application Insights。

### <a name="what-telemetry-is-collected"></a>會收集哪些遙測資料？

對於只會在執行階段使用狀態監視器檢測的應用程式︰

* HTTP 要求
* 呼叫 toodependencies
* 例外狀況
* 效能計數器

對於在編譯階段已經過檢測的應用程式︰

 * 處理程序計數器。
 * 相依性呼叫 (.NET 4.5)；在相依性呼叫中傳回值 (.NET 4.6)。
 * 例外狀況堆疊追蹤值。

[深入了解](http://apmtips.com/blog/2016/11/18/how-application-insights-status-monitor-not-monitors-dependencies/)

## <a name="video"></a>影片

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/100/player]

## <a name="next"></a>接續步驟

檢視遙測：

* [瀏覽度量](app-insights-metrics-explorer.md)toomonitor 效能和使用方式
* [搜尋事件和記錄檔][ diagnostic] toodiagnose 問題
* 更多進階查詢的[分析](app-insights-analytics.md)
* [建立儀表板](app-insights-dashboards.md)

新增更多遙測：

* [建立 web 測試][ availability] toomake 網站保持即時。
* [新增 web 用戶端遙測][ usage]從網頁程式碼和您插入的 toolet toosee 例外狀況追蹤呼叫。
* [將 Application Insights SDK tooyour 程式碼加入][ greenbrown] ，讓您可以插入追蹤和記錄的呼叫

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[availability]: app-insights-monitor-web-app-availability.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[greenbrown]: app-insights-asp-net.md
[qna]: app-insights-troubleshoot-faq.md
[roles]: app-insights-resources-roles-access-control.md
[usage]: app-insights-javascript.md
